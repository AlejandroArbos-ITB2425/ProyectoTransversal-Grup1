# 2. Implantación de los servicios

## Preparación máquinas
| Name VPC | IP VPC | Subnet | Gateway | Routes | ID Cuenta | ID VPC | Server |
| ----------- | ----------- | ----------- | ----------- | ----------- | ----------- |----------- |----------- |
| VPC-Eduard | 10.2.0.0/16 | 10.2.1.0/24 | IGW-Eduard | RT-Eduard | 884365647459 | vpc-099d2ee5027493805 | srv1 |
| VPC-Alejandro | 10.0.0.0/16 | 10.0.1.0/24 | IGW-Alejandro | RT-Alejandro | 138706074330 | vpc-0d684a2cca2a773db | srv2 |
| VPC-Linyi | 10.1.0.0/16 | 10.1.1.0/24 | IGW-Linyi | RT-Linyi | 058264113592 | vpc-0e802896fad67ad98 | srv3 |
| VPC-Carlos | 10.3.0.0/16 | 10.3.1.0/24 | IGW-Carlos | RT-Carlos | 946111168272 | vpc-069ea527c0d5e8f0e | srv4 |

| Servidor | Servicios | Tipo EC2 |
| ----------- | ----------- | ----------- | 
| 1 | ElasticSearch, Kibana, Nagios | t2.large |
| 2 | Web, Audio, Streaming | t3.small |
| 3 | DNS, FTP | t2.micro |
| 4 | Base de Datos (PGSQL) | t3.small |
| 5 | Copias de Seguridad | t2.micro |

## Configuración de Servidor 1

#### ElasticSearch + Kibana
### Nagios

## Configuración de Servidor 2
Primero se crea una instancia dentro de AWS (Amazon Web Service) que tendrá el sistema operativo Ubuntu Server 24.04 LTS, se asigna t3.small como tipo de instancia dado que nos permitirá gestionar los servidores web, audio y streaming.

![image](./img/servicios/srv2/1.1.png)

Seguidamente, se asigna una IP elástica, que es una dirección IP pública fija que se puede reasignar entre distintos servidores para mantener accesible el servicio incluso si cambia la infraestructura.

![image](./img/servicios/srv2/1.2.png)

![image](./img/servicios/srv2/1.3.png)

![image](./img/servicios/srv2/1.4.png)

Después de la creación de la instancia, se hacen pruebas de conectividad con los otros servidores.

![image](./img/servicios/srv2/1.5.png)

Se cambia el nombre de la instancia.

![image](./img/servicios/srv2/1.6.png)

![image](./img/servicios/srv2/1.7.png)

#### Web (Nginx)
Nginx es un servidor web de alto rendimiento que también puede funcionar como proxy inverso y servidor de medios. Se utiliza para servir páginas web, redirigir tráfico y gestionar transmisiones de audio o vídeo.

Para poder instalar este servicio se debe  de ejecutar el comando “sudo apt install nginx” y “systemctl status nginx” para comprobar su estado.

![image](./img/servicios/srv2/2.1.png)

Se ha creado una carpeta dedicada donde almacenaremos los archivos relacionados con nuestra página principal. Además, se ha instalado la plantilla Massively con “wget”.

![image](./img/servicios/srv2/2.2.png)

![image](./img/servicios/srv2/2.3.png)

Para garantizar la seguridad de nuestra página web, se han generado tres archivos clave utilizando la herramienta OpenSSL. Estos archivos se utilizan para configurar un certificado SSL en nuestro servidor Nginx, asegurando que las comunicaciones con la página sean seguras y cifradas.

![image](./img/servicios/srv2/2.4.png)

Se crea y configura el host virtual dentro del directorio /etc/nginx/sites-available con los siguientes parámetros:

![image](./img/servicios/srv2/2.5.png)

> Al recibir una petición por el puerto 80, redirige automáticamente al puerto 443 (HTTPS), nuestro servidor escucha por todas las interfaces, por ende, se puede ver tanto con su IP privada y pública. Se añaden los certificados creados anteriormente, ruta de archivos, index.html y un return 404 para otros errores. 

> Para acceder a la página web: https://18.204.111.82/

![image](./img/servicios/srv2/2.6.png)

![image](./img/servicios/srv2/2.7.png)

**WEB FTP**

Además de la página anterior, se ha configurado el servicio FTP para poder usarlo a través de nuestra web. 

Se crea un nuevo directorio “ftp” dentro de “/var/www/html/pprincipal” en el cual se añade el archivo descomprimido de monsta_ftp.

![image](./img/servicios/srv2/2.8.png)

Lo más probable es que ocurra el siguiente error:

> “2025-05-21T09:46:43.211693+00:00 srv3 sshd[10412]: Unable to negotiate with 34.234.116.252 port 44862: no matching host key type found. Their offer: ssh-rsa,ssh-dss [preauth]”

Este error significa que el cliente (en la dirección IP 34.234.116.252, puerto 44862) intentó conectarse al servidor, pero no se pudo negociar una conexión SSH porque el cliente ofreció tipos de claves de host (ssh-rsa, ssh-dss) que el servidor no acepta. 

Para solucionar el error, se debe agregar las siguientes 2 líneas dentro del archivo
/etc/ssh/sshd_config

![image](./img/servicios/srv2/2.9.png)

Se modifica nuestro host virtual para poder acceder a la nueva localización /ftp y activar el uso de php-8.3.

![image](./img/servicios/srv2/2.10.png)

Para poder acceder a Monsta FTP, debemos navegar por “http://URLweb/ftp”. Una vez dentro, se puede autentificar el usuario tanto por FTP como SFTP/SCP.

![image](./img/servicios/srv2/2.11.png)

![image](./img/servicios/srv2/2.12.png)

![image](./img/servicios/srv2/2.13.png)

![image](./img/servicios/srv2/2.14.png)

Se crea un host virtual que hará de proxy para poder mostrar una página del servidor 4 que tiene la tablas sobre Auditoría de Empleados por Convenio. Para hacer esto, se debe añadir al archivo de configuración bind9 que contiene las zonas directas un nuevo CNAME para que haga referencia al proxy y poder buscarlo como bbddweb.grup1.pt.

Estos cambios y búsqueda/resolución de nombre solo se pueden ver desde dentro de la red virtual privada.

![image](./img/servicios/srv2/2.15.png)

![image](./img/servicios/srv2/2.16.png)

Se crea un enlace simbólico del fichero “bbdd” que está dentro del directorio /etc/nginx/sites-available/ hasta /etc/nginx/sites-enabled/ para activar el host virtual que actúa como proxy.

![image](./img/servicios/srv2/2.17.png)

![image](./img/servicios/srv2/2.18.png)

#### Audio
Icecast es un servicio de streaming de audio en tiempo real que permite transmitir contenido multimedia a múltiples usuarios simultáneamente. Se utiliza principalmente para crear emisoras de radio por internet o para enviar audio en directo a través de la red.

Para poder instalar este servicio se ejecuta el comando “apt install icecast2 -y”. Durante el proceso de instalación pide 3 tipos de contraseña (sourcepassword, relaypassword y admin password).

![image](./img/servicios/srv2/3.1.png)

![image](./img/servicios/srv2/3.2.png)

![image](./img/servicios/srv2/3.3.png)

![image](./img/servicios/srv2/3.4.png)

![image](./img/servicios/srv2/3.5.png)

![image](./img/servicios/srv2/3.6.png)

Seguidamente se instala DarkIce, que es una herramienta de captura y codificación de audio en tiempo real. Su función principal es tomar audio desde una fuente y enviarlo a un servidor de streaming como Icecast.

Para instalar darkice se ejecuta el comando “apt install darkice -y”.

![image](./img/servicios/srv2/3.7.png)

Se edita el fichero de configuración de darkice “/etc/darkice.cfg”.

![image](./img/servicios/srv2/3.8.png)

Al estar usando una instancia de Amazon Web Service (AWS) no se dispone de tarjetas de sonido, por ende, se instala una imagen genérica de linux con el siguiente comando “apt install linux-generic-image”ç

![image](./img/servicios/srv2/3.9.png)

Se comprueba la imagen de la cual se dispone para poder copiar el menuentry seleccionado en la siguiente foto. Esto nos servirá para configurar el grub por defecto.

![image](./img/servicios/srv2/3.10.png)

Accedemos a “/etc/default/grub” y en la línea GRUB_DEFAULT= se añade el texto copiado anteriormente, el nombre de la imagen (Ubuntu, with Linux 6.8.0-60-generic).

![image](./img/servicios/srv2/3.11.png)

Se ejecuta el comando sudo update-grub, que actualiza la configuración del gestor de arranque GRUB, y luego sudo reboot para aplicar los cambios.

![image](./img/servicios/srv2/3.12.png)

Se ejecuta el comando aplay -l, que muestra la lista de dispositivos de audio disponibles en el sistema. Sirve para identificar la tarjeta y el dispositivo de salida que se usarán en la configuración de audio.

![image](./img/servicios/srv2/3.13.png)

Se ejecuta echo “snd-aloop | sudo tee -a /etc/modules” para añadir el módulo snd-aloop (dispositivo de loopback de audio) al archivo /etc/modules, asegurando que se cargue automáticamente en cada arranque del sistema.

![image](./img/servicios/srv2/3.14.png)

Se abre “/etc/asound.conf” para editar el archivo de configuración global de ALSA, donde se define el comportamiento del sistema de sonido. Usaremos un dispositivo loopback dado que no disponemos de tarjeta de sonido.

![image](./img/servicios/srv2/3.15.png)

Se ejecuta apt install alsa-utils para instalar el paquete alsa-utils, que incluye herramientas esenciales para gestionar el sonido en Linux, como aplay, amixer y utilidades para configurar y probar dispositivos de audio.

![image](./img/servicios/srv2/3.16.png)


systemctl restart alsa reinicia el servicio de sonido ALSA para aplicar los cambios realizados en la configuración sin necesidad de reiniciar todo el sistema. Una vez hecha las anteriores configuraciones se reinicia el sistema.

Se ejecuta “sudo darkice -c /etc/darkice.cfg” que  inicia DarkIce usando el archivo de configuración especificado.

![image](./img/servicios/srv2/3.17.png)

Para poder acceder a Icecast2, debemos de entrar via URL, con nuestra IP pública y el puerto 8000.

![image](./img/servicios/srv2/3.18.png)

#### Streaming

## Configuración de Servidor 3
Para el servidor DNS y FTP se crea una instancia de tipo t2.micro con SO Ubuntu Server 24.04. 


Se asigna una IP elástica, quiere decir que es una  dirección IP pública estática que no cambia, incluso si la instancia se reinicia o se detiene.

Se accede a la instancia mediante la clave privada por ssh. Cambiar los permisos a solo lectura para la clave privada. 
ssh -i key_LZ.pem ubuntu@98.83.123.40

#### DNS
#### FTP

## Configuración de Servidor 4
#### Base Datos

## Configuración de Servidor 5
#### Copias seguridad


