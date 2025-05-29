# 1. Propuesta de CPD (Centro de Procesamiento de Datos)

## Ubicación Física
#### Situación física de la sala en el edificio
Montar el sistema de CPD dentro del propio edificio, en una sala especializada para su mantenimiento y rendimiento estable. ej: alejado de las ventanas y la luz del sol.

Ubicación: Polígono Industrial de Avilés, Asturias

Coordenadas: 43.5563°N, 5.9248°W

Superficie: 360 m² (edificio CPD + oficinas)

![image](./img_ubicacion_fisica/ubicacion.jpg)

Ventajas específicas de Asturias:

Costo energía:  0,12 €/kWh (Asturias) vs. 0,15 €/kWh (Madrid)
Energía renovable: la energía eólica local tiene un coste marginal muy bajo y estable (no depende de combustibles fósiles) y, al ser renovable, reduce drásticamente las emisiones de CO₂, disminuyendo así la huella de carbono.

### Sala CPD

Alejado de ventanas: Sin exposición directa a luz solar (orientación interior)

Proximidad al SAI: Conexión directa con sistema de alimentación ininterrumpida

Acceso controlado: Alejado del tráfico principal de oficinas

Seguridad física: Zona con menos tránsito de personal no autorizado

![image](./img_ubicacion_fisica/planosala.png)


#### Sistemas de climatización
La temperatura se debe mantener entre 18°C – 27°C
La humedad relativa se debe mantener entre el 40% - 60%

Se implanta un esquema de pasillo frío / pasillo caliente:
El aire acondicionado de precisión (CRAC) inyecta aire frío bajo el suelo técnico hacia el pasillo frío.


El aire frío entra por la parte frontal de los racks, enfría los equipos y sale al pasillo caliente por su parte trasera.


El aire caliente del pasillo caliente es succionado por las tomas de retorno del CRAC (mediante rejillas en falso techo o conductos tras la unidad), se enfría y se recircula al pasillo frío.
Beneficios: evita mezcla de corrientes, minimiza puntos calientes y reduce hasta un 30 % el consumo de refrigeración.

#### Medidas para dificultar la identificación de la sala
La sala que alberga los racks y el RACK de servidores se sitúa en el núcleo interior del edificio, lejos de vestíbulos y accesos principales. No tiene ventanas ni puertas acristaladas; en caso de existir una ventanilla, se aplica un film opaco para impedir la visibilidad. Todas las canalizaciones de red y alimentación eléctrica llegan mediante falsos techos y suelos técnicos, de modo que no sea posible reconocer la función de la sala desde el exterior.

El acceso físico está estrictamente solo para personal autorizado, bajo control de cámaras. No se instalan conductos ni ventiladores aparentes: el aire caliente extraído de los pasillos traseros de los racks se canaliza por conductos internos hasta la unidad CRAC.

De este modo, la sala de refrigeración de precisión y los equipos permanecen discretos, discretamente integrados en la infraestructura, cumpliendo requisitos de confidencialidad, seguridad y eficacia térmica.


#### Distribución y gestión del cableado
El objetivo es garantizar una instalación limpia, eficiente, segura y fácilmente escalable, evitando interferencias, sobrecalentamientos o errores humanos.
1. Canalización separada
Eléctrico y datos en trayectorias distintas:

Canaletas eléctricas en canto de falso suelo.

Bandejas de datos en el techo técnico o railes bajo suelo.

Ventaja: minimiza interferencias electromagnéticas y facilita futuras ampliaciones.


2. Etiquetado claro y uniforme
   
Cada cable lleva etiqueta en ambos extremos con formato:
EJ: srv3 — eth0 — switch1 — port5
Se emplea tipografía legible y película termocontraíble para durabilidad.
Beneficio: agiliza la identificación en incidencias y reduce el riesgo de desconexiones erróneas.

4. Tipos, longitudes y colores
Categoría de cable:
Cat 6a para todos los enlaces de datos (hasta 10 Gbps con margen).


Longitud optimizada:
Evitar cables excesivamente cortos (tensión en conectores) o muy largos (enredos).
Longitud recomendada: 1–3 m en pasillos, 5–7 m para enlaces entre salas.


Código de color en funda o cinta:

Azul → Red de administración
Verde → Red interna entre servidores
Rojo → Tráfico de Internet
Naranja → Backups y almacenamiento

Documentación del cableado
Mapa de red físico y lógico actualizado
Inventario de conexiones con fecha y responsables de la instalación
Tener un cableado ordenado y sin obstáculos mejora la ventilación interna de los racks, ayudando a mantener una temperatura más baja y reduciendo el consumo de energía en refrigeración.


#### Suelo técnico y techo técnico
Debemos optimizar la distribución de cableado, ventilación y accesibilidad del CPD mediante estructuras físicas diseñadas específicamente para entornos de servidores.
Suelo técnico (plenum de aire frío)
Función principal: cámara de distribución de aire frío proveniente de las unidades CRAC hacia el pasillo frío.
Altura del suelo: 0,20 m para canalizar la refrigeración y cableado.
Material: paneles metálicos (aluminio o acero con recubrimiento anti-corrosión) desmontables.
Usos complementarios:
Canalización de cableado de datos (Cat 6a) y fibra, separado de la electricidad.


Pasacables y conductos de alimentación de PDUs desde bandejas superiores.

Ventajas:
- Flujo controlado de aire frío al frente de los racks.
- Acceso rápido al cableado para mantenimiento.
- Refuerzo de la estrategia “cold aisle containment”.
- Techo técnico (plenum de retorno)
- Función principal: rejillas y conductos para extraer el aire caliente del pasillo caliente y conducirlo de vuelta a los CRAC.
- Altura libre bajo techo: 0,30 m para bandejas y tuberías.
- Material: perfiles metálicos y placas ligeras (aluminio o chapa galvanizada).
- Usos complementarios:
- Bandejas estructuradas de red y fibra.


Iluminación LED empotrada y sensores de temperatura/humedad.

Ventajas:
- Evacuación limpia del aire caliente, evitando recirculaciones indeseadas.
- Canalización ordenada de cables de red, manteniendo el techo libre de obstáculos.
- Integración de detectores y luminarias sin interferir con el flujo de retorno.
- La combinación de falso suelo como plenum frío y falso techo como plenum caliente, junto al esquema de pasillos frío / caliente y unidades CRAC, reduce la carga de refrigeración, mejora la   eficiencia energética y facilita futuras ampliaciones con mínimo trabajo en obra.

#### Planos, dibujos y diagramas 

![plano_sala_rack_v2.png](img_ubicacion_fisica/plano_sala_rack_v2.png)

**Pasillo frío**

![image](./img_ubicacion_fisica/frio.png)

**Pasillo caliente**

![image](img_ubicacion_fisica/caliente_muy_caliente_papi.png)

## Infraestructura IT 

#### Servidores: número y tipo de modelo

Se montará 5 servidores:

- FTP + DNS 

- Audio + Video + Web

- Monitorización

- Base de datos

- Backups

La idea es empezar tratando a 2500 - 5000 clientes, así que no necesitaremos los servidores más potentes, pero sí necesitaremos que puedan aumentar su potencia y capacidad, por ende, hemos pensado planes de escalabilidad.

Se implementará la siguiente estructura:

3 racks de 19 pulgadas para permitir una mejor organización, separación de funciones y espacio para la expansión futura.

- Rack 1: Equipos de red y seguridad (switches, firewall, patch panels).

- Rack 2: Servidores (principalmente).

4 servidores rack (ej. 1U o 2U) para cubrir los 3 roles principales con redundancia básica para los más críticos

Estos servidores serán de la gama Smart Selection PowerEdge R660 Rack Servidor, en la que podremos personalizar nuestros racks, además de los 3 racks de 19 pulgadas:

![image](./img/rack/1.1.png)



Rack 3: Servidores adicionales, sistemas de almacenamiento, patch panels adicionales, espacio para crecimiento y escalabilidad.

![image](./img/rack/1.2.png)
![image](./img/rack/1.3.png)
![image](./img/rack/1.4.png)
![image](./img/rack/1.5.png)


En resumen, lo más importante:

Cables de red rápidos para gestionar las bases de datos y los servicios de monitorización principalmente.

Fuentes de alimentación redundantes que permitan la manipulación en caliente

3 discos duros SSD de 480 GB para permitir la configuración en RAID 5 (Copias de seguridad en caso de emergencias).

En el caso de necesitar más discos duros por motivos de escalabilidad o exigencia, cambiaríamos a HDD para hacer más leves las consecuencias económicas del proyecto.

Por ejemplo, el rack servidor de streaming es mucho más exigente que los otros 3, por tanto, utilizaremos HDD para ahorrar gastos y suplir las necesidades de un servicio tan demandante:

![image](./img/rack/1.6.png)

Este será el rack servidor para los servicios en streaming

Por último, un procesador potente que nos asegure poder gestionar todos los procesos de forma adecuada.


#### Patch panels

En el rack de red mencionado anteriormente irán los patch pannels, donde se conectan todos los elementos de los servidores:

![image](./img/rack/1.7.png)

Se utilizará este modelo, que proporciona compatibilidad con nuestros cables de red gracias al estándar Cat 6a. Se podría adquirir más si fuera necesario.


#### Switches

Se utilizará este Switch como Switch Core:

![image](./img/rack/1.8.png)

Configurable a nivel de consola y con la velocidad adecuada

Y este como Switch Access:

![image](./img/rack/1.9.png)

En la que la intención es formar una estructura redundante para evitar pérdida de información.

![image](./img/rack/1.10.png)

El precio sube un poco porque ya compramos 4 cables de 10 gigabits por switch, ya que proporciona la cantidad necesaria y un poco de exceso en caso de necesitarlo en futuras ampliaciones 

#### Planos y diagramas

![image](./img/rack/1.11.png)

![image](./img/rack/1.12.png)

![image](./img/rack/1.13.png)


## Infraestructura eléctrica

#### Sistemas de alimentación redundante
Un SAI (Sistema de Alimentación Ininterrumpida) es un dispositivo que proporciona energía de reserva temporal a los servidores cuando existe un corte eléctrico, utilizando baterías internas, y también protege contra fluctuaciones de voltaje (como subidas o bajadas de tensión).
Un SAI es esencial para: 

Evitar pérdidas de datos: Si un servidor se corta repentinamente, se pueden perder datos del stream o configuraciones.
En un sistema redundante, un SAI actúa como capa de protección mientras un generador eléctrico (si lo hubiere) arranca.
Permite que los servidores permanezcan operativos durante un tiempo limitado para cerrar procesos o cambiar a una fuente alternativa.

#### SAIs
```
CÁLCULO DE SAIs
La fórmula que se usa es: Potencia total (VA) = Suma de potencias (W) de todos los dispositivos × 1.6 (factor de conversión W a VA) × 1.3 (margen de seguridad del 30%).

Rack 1 (Red): 300W × 1.6 × 1.3 = 624 VA

Rack 2 (4 Servidores): 1.700W × 1.6 × 1.3 = 3.536 VA

Rack 3 (Server 5): 450W × 1.6 × 1.3 = 936 VA

TOTAL: 2.450W × 1.6 × 1.3 = 5.096 VA

SAIs necesarios:

Rack 1: SAI 1000VA 

Rack 2: SAI 4000VA mínimo (se elige  5000VA para margen)

Rack 3: SAI 1500VA 
```
![image](./img/rack/1.14.png)

Se han seleccionado equipos APC Smart-UPS SRT con tecnología de doble conversión online como solución de alimentación ininterrumpida para el proyecto. Además, se han tenido en cuenta los siguientes criterios:

Autonomía operativa: Se establece un mínimo de 1 hora de funcionamiento continuo.
Tecnología de protección: Se especifica tecnología online de doble conversión.
Gestión remota: Se requiere capacidad de monitorización SNMP integrada.
Escalabilidad: Se contempla la posibilidad de expansión mediante baterías externas.
Soporte técnico: Se exige disponibilidad de soporte profesional 24/7.

Como resumen, APC Smart-UPS SRT constituye la opción técnica y económicamente más adecuada para los requerimientos del proyecto

**Presupuesto**

![image](./img/rack/1.15.png)

![image](./img/rack/1.16.png)

![image](./img/rack/1.17.png)

![image](./img/rack/1.18.png)

![image](./img/rack/1.19.png)

![image](./img/rack/1.20.png)


## Seguridad física
#### Elementos de control de acceso a incorporar en el CPD
__Acceso con datos biométricos (huellas)__ 
Se utilizará el método de autenticación con datos biométricos. Permite asegurar que solo el personal autorizado pueda acceder a las instalaciones del CPD. La autenticación biométrica mediante huellas dactilares es una medida segura y evitamos el uso indebido de tarjetas o claves compartidas. Con esta tecnología garantiza que el acceso sea individual. Registro automatizado de accesos (logs con fecha, hora y usuario).

__Llave de emergencia__ 
En caso de corte de suministro eléctrico, los sistemas biométricos pueden quedar inoperativos. Por ello, se dispondrá de una llave de emergencia que permite el acceso físico al CPD. Almacenarlo en una caja de seguridad con acceso restringido a personal de alto rango. 

#### Videovigilancia
Se instalan cámaras de videovigilancia en la sala y en el entorno donde se sitúa el CPD (entradas, pasillos, salas de servidores) que cuentan con visión nocturna. Esto garantiza una supervisión continua las 24 horas del día, incluso con baja iluminación o en condiciones nocturnas. Las grabaciones se almacenan y se revisan en caso de incidentes.
Almacenamiento en servidores locales con cifrado y copias en la nube, con retención de registros por al menos 90 días.

#### Sistemas de prevención, detección y extinción de incendios

__Prevención__

- Instalación eléctrica certificada y protegida 
Todo el sistema eléctrico del CPD debe cumplir con la normativa vigente y contar con protección contra sobrecargas, cortocircuitos y sobretensiones. 

- Detectores térmicos (Control de temperatura y humedad) 
El CPD está equipado con sensores que miden temperatura y humedad en tiempo real. Estos sensores generan alertas automáticas cuando los valores superan los umbrales establecidos,* lo que permite actuar rápidamente para evitar daños en los equipos. 

*Temperatura: 18 °C a 27 °C

*Humedad: 40 % a 60 % HR

- Mantenimiento periódico de equipos
Para garantizar la operatividad y seguridad del CPD, se realiza un mantenimiento preventivo regular. 
Limpieza mensual de servidores y conductos de aire, para evitar la acumulación de polvo.
Una revisión trimestral de cableados y conexiones eléctricas.

__Detección__

- Detectores de humo sensibles  
Se utilizarán diferentes tecnologías según el tipo de incendio:
Ionización: ideales para detectar incendios rápidos con poca cantidad de humo.
Fotoeléctricos (ópticos): eficaces en la detección de incendios con humo denso y lento desarrollo.
Detectores de chispas o llamas (IR/UV): detectan radiación emitida por llamas o chispas y actúan en milisegundos.

- Sistema automático de alarma contra incendios (PCI) 
El CPD cuenta con un sistema de alarma conectado a los sensores de humo, temperatura y llama. Ante cualquier anomalía, se activa una alarma sonora y visual, se notifica automáticamente al personal de seguridad y, si se configura, a servicios de emergencia externos. 

- Monitorización 24/7 
Se utilizará Nagios como sistema de monitorización continua de todos los equipos y servicios del CPD. Este software de código abierto permite detectar fallos o anomalías en tiempo real y enviar alertas inmediatas al equipo técnico.

__Extinción__

- Sistemas de supresión automática
Ante un incendio, se activan sistemas de extinción que no dañan los equipos electrónicos. Se utilizará agentes limpios como los gases inertes Novec 1230 y FM-200. Actúan desplazando el oxígeno en la zona del fuego, extinguiéndolo sin dejar residuos.

- Extintores por tipo de fuego
Clase C: especiales para fuegos en equipos eléctricos o electrónicos.
Clase A: para combustibles sólidos como papel, plásticos o textiles (poco frecuentes en CPD, pero necesarios por si acaso).

- Puertas y paredes cortafuegos
Estos elementos están diseñados para contener el fuego en caso de incendio durante un tiempo determinado (habitualmente 60 o 120 minutos).

#### Vías de evacuación
Se deben elaborar planos independientes por cada planta del edificio, o por zonas si son demasiado amplias. Los aspectos que hay que tener en cuenta son:
- Realizar un plano de los diferentes espacios, donde se vean claramente las paredes, las escaleras, las puertas, etc. Hay que indicar el nombre de cada espacio.
- Indicar el sentido de la vía de evacuación, mediante flechas que señalen hacia las salidas de emergencia.
- Dibujar los diferentes símbolos como podrían ser los de riesgo, la ubicación de los extintores de incendios y de los pulsadores de alarma, las bocas de incendio equipadas y los avisadores de alarma.
- Indicar el punto de encuentro exterior de concentración, en caso de evacuación.
- Indicar las salidas al exterior del edificio del centro de trabajo. También se debe dibujar mediante flechas el recorrido de evacuación.
Ancho mínimo de 1.2 metros en pasillos y puertas para facilitar el flujo de personas.
Señalización luminiscente (fotoluminiscentes o con energía de respaldo) que indique la dirección de salidas.
Iluminación de emergencia automática (con baterías) en caso de cortes de energía.
Alarmas sonoras y visuales sincronizadas con sistemas de detección de incendios.

#### Diagramas, planos y fotografías

![image](./img_ubicacion_fisica/planE.png)

## Seguridad lógica
#### Restricción de acceso mediante autorización
La restricción de acceso mediante autorización es una medida clave en la seguridad lógica del CPD, garantiza que solo los usuarios que tengan los permisos adecuados puedan acceder a los recursos y servicios del CPD.

__Principio de menor privilegio__

Este principio establece que a cada usuario o sistema se le debe otorgar el mínimo nivel de acceso necesario para cumplir con sus tareas

__Control de acceso basado en roles (RBAC)__

Asigna permisos según los roles de los usuarios. Por ejemplo, solo los administradores del CPD tendrán acceso a configuraciones críticas de los servidores y los usuarios normales solo podrán interactuar con los servicios autorizados.

__Autenticación multifactor (MFA)__

Implementa autenticación multifactor para el acceso a sistemas críticos (servidores, bases de datos, paneles de control).

__Gestión de sesiones__

Asegurarse de que las sesiones de los usuarios que acceden al sistema tengan un tiempo limitado y que el acceso se cierre automáticamente si no se detecta actividad por un periodo de tiempo.

#### Firewalls
El uso de firewalls en el contexto de la seguridad lógica de un CPD (Centro de Procesamiento de Datos) es fundamental para proteger la infraestructura contra accesos no autorizados y ataques externos.

__Firewall de red (hardware)__

Es un dispositivo dedicado que se coloca entre la red interna del CPD y el exterior (internet). Estos firewalls son más robustos y están diseñados para manejar grandes volúmenes de tráfico.

__Firewall de host (software)__   

Un firewall instalado en cada servidor o máquina del CPD. Actúa sobre el sistema operativo de la máquina y filtra el tráfico a nivel de la propia máquina.
En nuestro caso, se utilizará un firewall de red para filtrar el tráfico entre la infraestructura interna y las redes externas, garantizando que solo las conexiones necesarias sean permitidas. Además, se implementará  un firewall de host en cada servidor para protegerlos a nivel individual, controlando qué aplicaciones pueden comunicarse entre sí.

#### Monitorización
Se implementará un sistema de monitorización centralizada que nos permitirá supervisar el estado y rendimiento de todos los servidores, servicios y recursos críticos del CPD. Se utilizará herramientas como Nagios para el control de disponibilidad, alertas en tiempo real y análisis de eventos, y ElasticSearch + Kibana para la visualización y análisis de logs. Esto nos ayudará a detectar fallos rápidamente, anticiparnos a problemas y asegurar la continuidad del servicio.

Se configurarán los servicios mencionados dentro de un mismo servidor, el cual estará especializado para la monitorización de otros servicios y análisis en tiempo de eventos en tiempo real. 

#### Copias de seguridad / Backups
Al ofrecer servicios a clientes y operar con sus datos, debemos disponer de integridad y disponibilidad de los datos, para eso, se implementará un sistema de copias de seguridad automatizadas. Se realizarán backups diarios incrementales y semanales completos, almacenados en una ubicación externa segura.

#### RAIDs
Para reforzar la disponibilidad y la tolerancia a fallos del sistema, en nuestro CPD se utilizarán configuraciones RAID. Estas permiten combinar varios discos duros físicos en una sola unidad lógica para mejorar la seguridad de los datos y rendimiento.

Se implementará RAID 5 en nuestro CPD, dado que ofrece un buen equilibrio entre rendimiento, capacidad y tolerancia a fallos. Esta configuración distribuye los datos y la paridad entre varios discos, permitiendo que el sistema siga funcionando aunque uno falle.

## Prevención de riesgos laborales 

#### Medidas aplicadas en materia de prevención de riesgos laborales en el CPD

En un CPD (Centro de Procesamiento de Datos), hay diversos riesgos que pueden comprometer la seguridad, disponibilidad e integridad de los datos y sistemas.

**Riesgos Físicos o Ambientales**

Incendios: por fallos eléctricos, cortocircuitos o materiales inflamables.

Inundaciones: por rotura de tuberías, lluvias intensas o fallos en el sistema de climatización.

Temperaturas extremas: fallo del aire acondicionado puede provocar sobrecalentamiento.

Cortes de energía: afectan directamente a los servidores si no hay SAIs o generadores.

Vibraciones o movimientos estructurales: afectan al hardware delicado.

**Riesgos Técnicos o de Infraestructura**

Fallo de hardware: discos duros, fuentes de alimentación, tarjetas de red, etc.

Fallo de software: errores del sistema operativo, aplicaciones o firmware.

Fallo en el sistema de refrigeración: puede llevar a un sobrecalentamiento.

**Riesgos de Seguridad Lógica (Ciberseguridad)**

Ataques externos: malware, ransomware, phishing, DDoS, etc.

Intrusiones: accesos no autorizados a redes, servidores o bases de datos.

Fugas de información: por malware, vulnerabilidades o mala configuración.

### Riesgos laborales 

**Riesgos Ergonómicos**

Posturas forzadas o repetitivas: por trabajar muchas horas sentado frente al ordenador.

Pantallas de visualización: fatiga visual, dolores cervicales y de espalda.

Movimientos repetitivos: uso continuo de teclado y ratón.

Espacios reducidos: puede dificultar la movilidad y causar incomodidad.

**Medidas preventivas:**

Instalación de mobiliario ergonómico (sillas regulables, reposapiés, soportes de monitor)

Pausas programadas cada 2 horas para descanso visual y corporal

Formación sobre higiene postural y ejercicios de estiramiento

Iluminación adecuada para reducir reflejos y fatiga visual

**Riesgos Eléctricos**

Contacto con cables o equipos eléctricos defectuosos.

Sobrecargas o chispazos al manipular hardware.

Riesgo de electrocución si no se siguen protocolos de seguridad.

**Medidas preventivas:**

Uso obligatorio de equipos de protección individual (EPI) dieléctricos

Inspecciones periódicas de instalaciones eléctricas

Formación específica en seguridad eléctrica para el personal técnico

Sistemas de protección diferencial y tomas de tierra verificadas

**Riesgos Ambientales**

Temperaturas extremas: si el sistema de refrigeración falla o hay zonas mal ventiladas.

Riesgo acústico: por ventiladores, servidores o sistemas de refrigeración 

**Medidas preventivas:**

Sistemas de climatización redundantes con alarmas de temperatura

Monitorización continua de condiciones ambientales

Protección auditiva obligatoria en zonas de alto ruido

**Riesgos Mecánicos o Técnicos**

Caídas o golpes: al moverse entre racks o manipular equipos pesados.

Cortes: al abrir o manejar hardware 

Carga física: levantar servidores o equipos pesados. 

**Medidas preventivas:**

Pasillos amplios y libres de obstáculos entre racks

Iluminación de emergencia y señalización clara

Equipos de elevación mecánica para cargas pesadas

Formación en técnicas de manipulación manual de cargas

Uso de guantes de protección y herramientas adecuadas

**Riesgos de Incendio** 

Espacios cerrados con alta densidad de equipos eléctricos: riesgo elevado de incendio.

**Medidas preventivas:**

Sistema de detección de incendios con sensores de humo y temperatura

Sistema de extinción automática con gas inerte (no dañino para equipos)

Extintores específicos para fuegos eléctricos distribuidos estratégicamente

Plan de evacuación específico y simulacros periódicos

Mantenimiento preventivo de instalaciones eléctricas

**Riesgos Psicosociales**

Estrés laboral: por la necesidad de mantener la disponibilidad 24/7 de los sistemas.

Trabajo en turnos nocturnos o guardias: puede afectar el descanso y la salud mental.

Aislamiento: si el trabajo se realiza en solitario o en zonas sin interacción frecuente.

Medidas preventivas:

Rotación de turnos para distribuir la carga de trabajo nocturno

Evaluación periódica del clima laboral y nivel de estrés

Formación en gestión del estrés y técnicas de relajación

Espacios de descanso adecuados para personal de guardia

## Sostenibilidad

#### Cómo optimizar el consumo de energía
Para optimizar el consumo de energía en nuestro CPD utilizaremos servidores con eficiencia energética, discos SSD en lugar de HDD siempre y cuando se pueda. Configuraciones RAID que reduzcan el consumo sin disminuir la seguridad. Además, implementar políticas de apagado o suspensión para aquellos equipos que estén activos durante un tiempo predeterminado, un sistema de climatización eficiente, aire acondicionado con gas y control del uso energético en tiempo real con herramientas de monitorización. Finalmente, sustituir las luces convencionales por luces LED, aprovechando su mayor durabilidad y eficiencia energética, lo que se traduce en un ahorro significativo en costes eléctricos.

#### Uso de energía verde en el CPD
Para minimizar el impacto ambiental del CPD, proponemos utilizar fuentes de energía renovable, como la energía solar, para alimentar las instalaciones. Esto no solo reduce las emisiones de carbono, sino que también contribuye a una operación más sostenible a largo plazo. Para eso, se deben seleccionar proveedores de electricidad que garanticen el uso de energías limpias certificadas, asegurando así un compromiso real con la sostenibilidad energética. 

#### Ahorro en longitud de cableado
Reducir la longitud del cableado dentro del CPD contribuye a minimizar pérdidas energéticas y mejorar la eficiencia del sistema. Para ello, se ha diseñado una distribución optimizada de los equipos y racks, ubicándolos lo más cerca posible para reducir la distancia entre conexiones. Además, se emplearán cables de alta calidad que permiten mantener un buen rendimiento incluso con longitudes reducidas, lo que favorece tanto el ahorro energético como la reducción del desorden y la mejora en el mantenimiento.

#### Sistemas de circulación de aire que aprovechen condiciones naturales
Implementar sistemas de ventilación que aprovechen las condiciones naturales del entorno puede reducir significativamente el consumo de energía del CPD. Esto incluye el uso de ventilación cruzada, la incorporación de tomas de aire exterior frescas y la utilización de sistemas de enfriamiento pasivo cuando las condiciones climáticas lo permitan. Teniendo en cuenta todo lo mencionado anteriormente se llegará a minimizar el uso de aire acondicionado, contribuyendo a una gestión más sostenible.

#### Parada automática de equipos de comunicaciones cuando no haya carga
Implementaremos sistemas que detecten la ausencia de tráfico o actividad en los equipos de comunicaciones y que permitan su apagado automático contribuye a un uso más eficiente de la energía. Esta medida evita el consumo innecesario de electricidad durante periodos de baja demanda, reduciendo la huella energética del CPD y optimizando el rendimiento global de la infraestructura tecnológica.

#### Uso de equipos de bajo consumo energético
Se selecciona y se hace uso de hardware y dispositivos que estén diseñados para consumir menos energía, es muy importante para reducir el impacto ambiental del CPD. Se usarán equipos con certificaciones de eficiencia energética (Energy Star) para poder mantener un alto rendimiento mientras se minimiza el gasto eléctrico, gracias a esto contribuimos a la sostenibilidad y al ahorro económico a largo plazo

## Implementación del CPD en la nube (AWS)


| SRV1          | SRV2      | SRV3 | SRV4       | SRV5             | 
|---------------|-----------|------|------------|------------------|
| Nagios        | Web       | DNS  | Base Datos | Copias Seguridad |
| Kibana        | Audio     | FTP  |
| ElasticSearch | Streaming | 

Habrá 4 servidores que ofrecerán 8 servicios. 

**SRV1**

ElasticSearch:se utiliza como motor de búsqueda y análisis para centralizar los logs generados por los diferentes servidores y servicios.  

Kibana:proporciona una interfaz web para visualizar y analizar los datos almacenados en ElasticSearch. Se usarán dashboards para identificar errores o problemas en tiempo real.

Nagios:monitoriza el estado de la infraestructura de red (discos, CPU, RAM, estado de servicios, conectividad, etc.). Envía alerta

**SRV2**

Servidor dedicado a servicios públicos o multimedia accesibles por los usuarios.

Servicio Web:se aloja un servidor web Nginx con información de los servicios que se implementa. 

Servicio de audio y video:se usará Icecast para transmisión de audio en tiempo real. Darkice para capturar y enviar audio al servidor Icecast. Protocolo RTP para transmisión de medios y FFmpeg para codificación, decodificación de audio/vídeo. 


**SRV**3

Servicios de red fundamentales para el funcionamiento interno y la transferencia de archivos.

DNS (Bind9):resuelve nombres de dominio en direcciones IP dentro de la red local o como proxy externo.  

FTP (ProFTPd):permite la transferencia de archivos entre clientes y el servidor, con autenticación segura y control de permisos.

**SRV4**

Servidor dedicado al almacenamiento estructurado de datos.

Motor de base de datos con PostgreSQL. 

Se encarga de almacenar información de los empleados.

**SRV5**

Encargado de la protección de los datos ante pérdidas o fallos.

Copia incremental diaria: guarda los archivos que han cambiado desde la última copia.  
Copia completa semanal: se guarda todo el contenido seleccionado, garantizando una recuperación completa si es necesario.

Se desarrolla un script automatizado que utiliza rsync para sincronizar datos de forma eficiente entre servidores.


## Investigación y comparación de eficiencia energética

#### Investigar y comparar la eficiencia energética con otros proveedores de nube

### **Comparación de Proveedores de Nube - Eficiencia Energética**

| **Proveedor** | **PUE Promedio** | **% Energía Renovable** | **Compromiso Net Zero** | **Regiones Eficientes** |
|---------------|------------------|-------------------------|-------------------------|-------------------------|
| **AWS** | 1.15 | 100% (2025) | 2040 | us-west-2, eu-north-1 |
| **Google Cloud** | 1.10 | 100% (2017) | 2030 | europe-north1, us-central1 |
| **Microsoft Azure** | 1.18 | 100% (2025) | 2030 | North Europe, West US 2 |
| **Promedio Industria** | 1.84 | 30% | 2050 | N/A |

#### Cómo los distintos proveedores ofrecen soluciones de CPD gestionadas por estas empresas

### **Soluciones de CPD Gestionadas por Proveedor**

#### **AWS**
**Servicios CPD gestionados:**
- **EC2 Dedicated Hosts:** Hardware físico dedicado
- **AWS Outposts:** Infraestructura AWS on-premise
- **Local Zones:** Edge computing de baja latencia
- **Wavelength:** 5G edge computing

**Características sostenibles:**
- Customer Carbon Footprint Tool integrado
- Instancias Graviton2 (20% más eficientes)
- Refrigeración líquida directa en servidores
- Backup generators con HVO (aceite vegetal)

#### **Google Cloud Platform**
**Servicios CPD gestionados:**
- **Anthos:** Plataforma híbrida on-premise/cloud
- **Google Distributed Cloud:** Edge locations
- **Dedicated Cloud Interconnect:** Conexión privada

**Características sostenibles:**
- Carbon-free energy matching 24/7 (objetivo 2030)
- Predicción AI para optimización cooling
- Custom TPUs 10x más eficientes que GPUs
- Programa de carbono negativo

#### **Microsoft Azure**
**Servicios CPD gestionados:**
- **Azure Stack:** Infraestructura híbrida
- **Azure Edge Zones:** Computing distribuído
- **Azure Arc:** Gestión multi-cloud

**Características sostenibles:**
- Underwater datacenters (Project Natick)
- Fuel cells de hidrógeno para backup power
- Cooling por aire exterior (free cooling)
- Compromiso water positive 2030

#### Cómo cubren los requerimientos previamente expuestos
