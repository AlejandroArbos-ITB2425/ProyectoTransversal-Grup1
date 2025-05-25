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
![image](./img/servicios/srv3/1.1.png)

Se asigna una IP elástica, quiere decir que es una  dirección IP pública estática que no cambia, incluso si la instancia se reinicia o se detiene.
![image](./img/servicios/srv3/1.2.png)
Se accede a la instancia mediante la clave privada por ssh. Cambiar los permisos a solo lectura para la clave privada. 
ssh -i key_LZ.pem ubuntu@98.83.123.40
![image](./img/servicios/srv3/1.3.png)

#### DNS (Domain Name System)

El servicio DNS traduce nombres de dominio a direcciones IP y también la resolución inversa. Para ello hay que instalar el software principal que actuará como servidor DNS (bind9).

Para instalar bind9 hay que ejecutar la siguiente comanda: _sudo apt install bind9_ 
![image](./img/servicios/srv3/2.1.png)

Cambiar el nombre del sistema modificando el archivo /etc/hostname para una mejor  identificación del servidor dentro de la red. 
![image](./img/servicios/srv3/2.2.png)

En el archivo /etc/hosts hay que asociar manualmente direcciones IP con nombres de dominio, permitiendo que el sistema resuelva esos nombres sin consultar un servidor DNS externo.

![image](./img/servicios/srv3/2.3.png)

Se tiene que configurar la resolución DNS y el dominio de búsqueda modificando el archivo /etc/netplan/50-cloud-init.yaml
![image](./img/servicios/srv3/2.4.png)

Añadir en el archivo _/etc/systemd/resolved.conf_ la dirección IP del server y el dominio

![image](./img/servicios/srv3/2.5.png)

Hay que modificar el enlace del archivo _/etc/resolv.conf_. 
Ejecutar _rm-f /etc/resolv.conf_ y volver a crear un enlace simbólico, 
_ln -s /run/systemd/resolve/resolv.conf /etc/resolv.conf_ 

![image](./img/servicios/srv3/2.6.png)
![image](./img/servicios/srv3/2.7.png)

Hacer una copia de la plantilla de los archivos que contienen la configuración de la zona directa y la zona inversa. En nuestro caso, se decide guardar estas configuraciones en un directorio llamado zonas dentro de _/etc/bind_. (_/etc/bind/zonas_)
La función de la zona directa es traducir nombres de dominio a direcciones IP y la inversa traducir direcciones IP a nombres de dominio. 

![image](./img/servicios/srv3/2.8.png)
![image](./img/servicios/srv3/2.9.png)

Configurar el archivo _/etc/bind/named.conf.local_ para declarar las zonas directas e inversas asociadas con el dominio.

![image](./img/servicios/srv3/2.10.png)

Modificar el archivo _/etc/bind/named.conf.options_ 
El servidor DNS utilizará los servidores DNS externos con las direcciones IP 8.8.8.8 y 8.8.4.4 como reenviadores para resolver consultas de nombres de dominio que no estén en las zonas que el servidor gestiona directamente. 
- Recursion yes; Habilita la resolución recursiva, permitiendo que el servidor DNS resuelva consultas para dominios que no gestiona directamente (por ejemplo, google.com) consultando otros servidores DNS en la jerarquía. 
- Allow-recursion {10.0.0.0/8;}; Restringe la resolución recursiva a un rango específico de direcciones IP, en nuestro caso, la red 10.0.0.0/8. Solo los dispositivos en esta red pueden usar el servidor DNS para consultas recursivas.

![image](./img/servicios/srv3/2.11.png)

Modificar y añadir el parámetro -4 para que solo escuche peticiones del protocolo IPv4 en el archivo /etc/default/named, donde se configura parámetros de inicio del servicio Bind9. 

![image](./img/servicios/srv3/2.12.png)

Modificar el archivo _/etc/bind/zonas/db.grup1.pt_ para configurar la zona directa. 
- @: Representa la zona grup1.pt.
- IN SOA: Indica que es un registro de tipo SOA, que define la autoridad de la zona.
- grup1.pt.: Nombre del servidor primario de nombres
- @ IN NS ns.grupi.pt.: Define ns.grup1.pt como el servidor de nombres autorizativo para la zona.
- ns IN A 10.1.1.96: Asigna la dirección IP 10.1.1.96 a ns.grup1.pt, que corresponde a SRV3 

- IN A: asocia un nombre de host (como srv1.grup1.pt) a una dirección IP (como 10.2.1.49) para que los dispositivos puedan encontrar el servidor en la red.
- IN CNAME: crea un alias (como nagios.grup1.pt) que apunta a otro nombre de host (como srv1.grup1.pt), para facilitar el acceso a servicios específicos sin duplicar IPs.

![image](./img/servicios/srv3/2.13.png)

En el archivo de configuración para la zona inversa. 

SOA y NS: Al igual que en la zona directa, definen la autoridad (SRV3 como servidor DNS).
PTR: Asocia una IP a un nombre. 
La parte inversa, la IP sólo incluye los bytes relevantes dentro de la subred.

![image](./img/servicios/srv3/2.14.png)

![image](./img/servicios/srv3/2.15.png)

![image](./img/servicios/srv3/2.16.png)
![image](./img/servicios/srv3/2.17.png)
![image](./img/servicios/srv3/2.18.png)

![image](./img/servicios/srv3/2.19.png) ![image](./img/servicios/srv3/2.20.png)

![image](./img/servicios/srv3/2.21.png) ![image](./img/servicios/srv3/2.22.png)


#### FTP

FTP es un protocolo de la capa de aplicación del modelo TCP/IP que facilita la transferencia de archivos entre un cliente y un servidor. Utiliza los puertos 21 (para comandos) y 20 (para datos) por defecto. Pero FTP no es un protocolo seguro, existen mecanismos para asegurar las conexiones entre clientes y servidores FTP como son; FTPS o enviar el protocolo FTP a través de un túnel SSH(SFTP).

SFTP es un protocolo que proporciona transferencia segura de archivos sobre una conexión SSH. A diferencia del FTP, SFTP encripta tanto las credenciales de autenticación como los datos transferidos, proporcionando mayor seguridad.

Para instalar el servicio proFTPD  se ejecuta la siguiente comanda: _sudo apt install proftpd_

![image](./img/servicios/srv3/3.1.png)


Se decide implementar SFTP como método principal de transferencia de archivos 
por la necesidad de garantizar la seguridad de los datos sensibles que se transmiten, especialmente teniendo en cuenta la presencia de información como la base de datos. 
Por este motivo se instala el servicio ssh que permite una transferencia segura. 

Comando para instalar SSH: _sudo apt install openssh-server_

![image](./img/servicios/srv3/3.2.png)


Editar el archivo principal _/etc/ssh/ssh_config_ donde la guarda la configuración del servicio SSH.

Match Group sftpgroup: se aplica esta configuración sólo a los usuarios del grupo sftpgroup (se creará un grupo en el siguiente apartado)

ChrootDirectory %h: esta configuración sirve para restringir a los usuarios a su directorio personal (%h directorio home del usuario), evitando que puedan navegar fuera de ese directorio.

ForceCommand internal-sftp: fuerza de que los usuarios sólo puedan utilizar SFTP, no una shell completa (no pueden ejecutar bash).

AllowTcpForwarding no y X11Forwarding no: desactiva funcionalidades innecesarias para SFTP, reduciendo riesgos.

![image](./img/servicios/srv3/3.3.png)

Para poder utilizar SFTP hay que activar el módulo LoadModule mod_sftp.c e instalar proftpd-mod-crypto.

![image](./img/servicios/srv3/3.4.png)
![image](./img/servicios/srv3/3.5.png)

Se crea un directorio principal "_mkdir -p /ftp/sftpuser_" , esto sirve como base para alojar los directorios de los usuarios que utilizarán SFTP en el servidor, y un grupo "groupadd sftpgroup", este grupo identifica a los usuarios autorizados a acceder a SFTP.

Los usuarios que se crean, son asignados al grupo y al directorio creado. 
Y además de establecer una contraseña para los usuarios con la comanda passwd. 
Se configura la shell en /sbin/nologin para limitarlos a SFTP, evitando que puedan acceder a una shell completa.

![image](./img/servicios/srv3/3.6.png)

A continuación, el directorio /ftp/sftpuser es cambiado a root:root con comanda, "chown root:root /ftp/sftpuser". Esto garantiza que sólo el administrador tenga control sobre la carpeta principal.
Se añade permisos de lectura y ejecución al grupo sftpgroup con "chmod g+rx /ftp/sftpuser". Esto permite a los usuarios del grupo acceder a sus directorios, pero no modificar la estructura principal.

![image](./img/servicios/srv3/3.7.png)

![image](./img/servicios/srv3/3.8.png)

Se crean directorios individuales dentro de _/ftp/sftpuser_ para cada usuario. Estos directorios sirven como espacio privado para cada usuario dentro del sistema SFTP.
Además se crean subdirectorios llamados data dentro de cada directorio de usuario. 

![image](./img/servicios/srv3/3.9.png)




## Configuración de Servidor 4
Para nuestro caso de base de datos tenemos un Ubuntu Server 22.04 con conectividad al resto de máquinas y PostgreSQL instalado:
![img.png](img.png)
![img_2.png](img_2.png)
Previo a la creación de cualquier consulta, es necesaria la creación de un modelo entidad-relación, que será el siguiente:
![img_1.png](img_1.png)
##### Con las siguientes relaciones:
### Relaciones 1:N (Uno a Muchos):
CONVENIO_COLECTIVO - NIVEL_CONVENIO.

NIVEL_CONVENIO - COMPONENTE_SALARIAL_CONVENIO 

NIVEL_CONVENIO - HISTORIAL_NIVEL_EMPLEADO.

DEPARTAMENTO - EMPLEADO.

ROL_EMPRESA - EMPLEADO.

EMPLEADO - (HISTORIAL_NIVEL_EMPLEADO).

EMPLEADO - (HISTORIAL_SALARIO_EMPLEADO).

### Relaciones N:1 (Muchos a Uno):
ROL_EMPRESA-NIVEL_CONVENIO 
### Relaciones N:M (Muchos a Muchos):
REGLAS_ANTIGUEDAD - COMPONENTE_SALARIAL_CONVENIO.

REGLAS_PERIODO_PRUEBA_CONVENIO - NIVEL_CONVENIO.

##### Cada tabla tendrá una función importante en la base de datos y su precisión en los datos:

### Funciones de cada tabla:                       
CONVENIO_COLECTIVO: Información básica de los convenios (Nombre, vigencia..)

NIVEL_CONVENIO: Almacena las diferentes áreas y grupos por los que separa el sector, el convenio colectivo.

COMPONENTE_SALARIAL_CONVENIO: Guarda los salarios base y totales mínimos anuales para cada nivel de convenio y año.

REGLAS_ANTIGUEDAD: Detalla los porcentajes de incremento salarial por trienios para calcular la antigüedad.

REGLAS_PERIODO_PRUEBA_CONVENIO: Define las duraciones estándar de los periodos de prueba por área y tipo de contrato.

ROL_EMPRESA: Contiene la definición de los roles internos de la empresa y su mapeo a niveles de convenio.

DEPARTAMENTO: Lista los departamentos de la empresa para organizar a los empleados.

EMPLEADO: Es la tabla central con la información personal y contractual básica de cada trabajador.

HISTORIAL_NIVEL_EMPLEADO: Registra los cambios de nivel de convenio de un empleado a lo largo del tiempo.

HISTORIAL_SALARIO_EMPLEADO: Guarda el historial de los componentes salariales de cada empleado en diferentes momentos.

Hecho el modelo, pasamos a los ajustes de seguridad:

La base de datos aceptará entradas de todas las direcciones IP:
![BBDD_4.png](img/servicios/SRV4/BBDD_4.png) 
![BBDD_5.png](img/servicios/SRV4/BBDD_5.png)
Y en este archivo especificamos quién puede conectarse. En este caso se decide añadir las redes de todas las máquinas presentes en este proyecto
![BBDD_6.png](img/servicios/SRV4/BBDD_6.png)

Procedemos a la creación de la base de datos y de un usuario (Se adjunta prueba de la existencia de ambos objetos):
![BBDD_7.png](img/servicios/SRV4/BBDD_7.png)

Y la creación de la base de datos:
![BBDD_8.png](img/servicios/SRV4/BBDD_8.png)
#### Base Datos
La base de datos ya está creada, y ahora es necesario darle una interfaz gráfica. Utilizaremos Flask, que permite crear webs rápidas a partir de Python y HTML:
![BBDD_9.png](img/servicios/SRV4/BBDD_9.png)
Crearemos dos archivos:
-Un app.py que permita ejecutarse para iniciar el servicio.
-Un HTML con el template básico.
Y con esto ya tenemos una base de datos funcional.

## Configuración de Servidor 5
#### Copias seguridad


