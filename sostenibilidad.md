# 4. Sostenibilidad

## Sostenibilidad y eficiencia energética

Alineados con nuestros valores empresariales y los Objetivos de Desarrollo Sostenible (ODS), es fundamental que el proyecto se diseñe con un enfoque claro de sostenibilidad. Buscamos optimizar el uso de energía y utilizar soluciones que reduzcan el impacto ambiental de nuestras operaciones. Queremos explorar el uso de fuentes de energía renovable, así como implementar prácticas de eficiencia energética dentro del Centro de Procesamiento de Datos (CPD).

### Cálculo de la huella ecológica del proyecto realizado
#### Identificación de recursos utilizados:

Servicios desplegados: ¿Qué tipo de máquinas, servicios en la nube y protocolos se están utilizando?

**TIPOS DE MÁQUINAS (AWS EC2):**

1x t2.xlarge (4 vCPU, 16GB RAM) - Server 1 Monitorización

2x t3.small (2 vCPU, 2GB RAM) - Server 2 Streaming + Server 5 Backups

1x t2.micro (1 vCPU, 1GB RAM) - Server 3 DNS+FTP

1x t3.micro (2 vCPU, 1GB RAM) - Server 4 Base Datos


**SERVICIOS EN LA NUBE (AWS):**

EC2 - 5 instancias Ubuntu 24.04 LTS

EBS - 6 volúmenes (5×8GB + 1×100GB)

VPC - Red privada virtual

Security Groups - Firewall de red

Internet Gateway - Conectividad externa


**PROTOCOLOS UTILIZADOS:**

HTTP/HTTPS - Web y APIs (puertos 80/443)

SSH - Administración remota (puerto 22)

PostgreSQL - Base de datos (puerto 5432)

DNS - Resolución nombres (puerto 53)

FTP/SFTP - Transferencia archivos (puertos 21/22)

Icecast - Streaming audio (puerto 8000)

RTMP - Streaming video FFmpeg (puerto 1935)

HLS/DASH - Streaming adaptativo (HTTP)

Darkice - Captura audio streaming

SNMP - Monitorización Nagios (puerto 161)

Elasticsearch - Logs y búsqueda (puerto 9200)

Kibana - Visualización datos (puerto 5601)

ICMP - Diagnósticos red

NTP - Sincronización tiempo (puerto 123)

RTP - 5002 y 5004 UDP

Recursos consumidos: ¿Cuánto consumen en términos de CPU, RAM, almacenamiento, ancho de banda?


**CPU:**

Server 1 (t2.xlarge): 4 vCPU - Uso promedio 60-80% (Elasticsearch + Nagios + Kibana)

Server 2 (t3.small): 2 vCPU - Uso promedio 70-90% (FFmpeg encoding + Icecast + Darkice)

Server 3 (t2.micro): 1 vCPU - Uso promedio 30-50% (BIND9 + vsftpd)

Server 4 (t3.micro): 2 vCPU - Uso promedio 50-70% (PostgreSQL + consultas)

Server 5 (t3.small): 2 vCPU - Uso promedio 40-60% (rsync + backups)
TOTAL: 11 vCPU utilizadas


**RAM**:

Server 1: 16GB - Uso 12-14GB (Elasticsearch buffer pool + cache)

Server 2: 2GB - Uso 1.5-1.8GB (streaming buffers + transcoding)

Server 3: 1GB - Uso 600-800MB (DNS cache + FTP connections)

Server 4: 1GB - Uso 800-950MB (PostgreSQL + connections)

Server 5: 2GB - Uso 1-1.5GB (backup processes + file cache)

TOTAL: 22GB RAM - Uso efectivo ~18GB


**ALMACENAMIENTO:**

Server 1: 8GB EBS - Uso 6GB (SO + logs + índices Elasticsearch)

Server 2: 8GB EBS - Uso 5GB (SO + archivos multimedia temporales)

Server 3: 8GB EBS - Uso 4GB (SO + archivos FTP)

Server 4: 8GB EBS - Uso 6GB (SO + bases de datos PostgreSQL)

Server 5: 8GB + 100GB EBS - Uso 6GB + 60GB (SO + backups históricos)

TOTAL: 132GB EBS - Uso efectivo ~87GB


**ANCHO DE BANDA:**

Tráfico de entrada: ~500GB/mes (uploads FTP + datos monitorización)

Tráfico de salida: ~2TB/mes (streaming audio/video + web + descargas)

Tráfico interno: ~200GB/mes (backups + sincronización entre servers)

Picos streaming: 50Mbps durante eventos (Server 2)

Transferencias FTP: 20Mbps promedio (Server 3)

Consultas BD: 5Mbps constante (Server 4)

TOTAL: ~2.7TB/mes transferencia total

Previsión de uso: ¿Cuántas horas de funcionamiento, ¿cuántos usuarios y tráfico estimado se prevé?


**HORAS DE FUNCIONAMIENTO:**

Server 1 (Monitorización): 24/7 = 8.760 horas/año (crítico, nunca se apaga)

Server 2 (Streaming): 24/7 = 8.760 horas/año (servicio continuo streaming)

Server 3 (DNS+FTP): 24/7 = 8.760 horas/año (DNS siempre activo)

Server 4 (Base Datos): 24/7 = 8.760 horas/año (BD siempre disponible)

Server 5 (Backups): 20h/día = 7.300 horas/año (4h standby nocturno)


**USUARIOS**

Fase Actual (Año 1):

Usuarios registrados: 2.500 usuarios

Usuarios activos diarios: 500-800 usuarios

Usuarios concurrentes pico: 200-300 usuarios

Streaming simultáneo: 50-100 streams

Fase Crecimiento (Año 2-3):

Usuarios registrados: 5.000 usuarios

Usuarios activos diarios: 1.000-1.500 usuarios

Usuarios concurrentes pico: 400-600 usuarios

Streaming simultáneo: 100-200 streams

Tráfico Mensual Actual:

## **TABLA DE CÁLCULO DE TRÁFICO DETALLADA**

| **Servicio** | **Server** | **Usuarios/Día** | **Uso por Usuario** | **Frecuencia** | **Tamaño Promedio** | **Cálculo Mensual** | **Tráfico/Mes** |
|--------------|------------|------------------|---------------------|----------------|-------------------|------------------|------------------|
| **Streaming Audio** | Server 2 | 200 | 1.5h/día | Diario | 128kbps = 57MB/h | 200×1.5h×57MB×30d | **513 GB** |
| **Streaming Video** | Server 2 | 80 | 45min/día | Diario | 720p = 337MB/h | 80×0.75h×337MB×30d | **608 GB** |
| **Páginas Web** | Server 2 | 500 | 15 páginas/día | Diario | 800KB/página | 500×15×0.8MB×30d | **180 GB** |
| **APIs REST** | Server 2 | 500 | 100 llamadas/día | Diario | 8KB/respuesta | 500×100×8KB×30d | **12 GB** |
| **Recursos Web** | Server 2 | 500 | 1 vez/día | Diario | 3MB (CSS/JS/img) | 500×3MB×30d | **45 GB** |
| **FTP Upload** | Server 3 | 50 | 2 archivos/sem | Semanal | 25MB/archivo | 50×2×25MB×4w | **10 GB** |
| **FTP Download** | Server 3 | 80 | 3 archivos/sem | Semanal | 15MB/archivo | 80×3×15MB×4w | **14.4 GB** |
| **Consultas DNS** | Server 3 | 2500 | 150 consultas/día | Diario | 512 bytes/consulta | 2500×150×0.5KB×30d | **5.6 GB** |
| **Backup Incremental** | Server 5 | - | 1 vez/día | Diario | 200MB/backup | 1×200MB×30d | **6 GB** |
| **Backup Completo** | Server 5 | - | 1 vez/semana | Semanal | 1.5GB/backup | 1×1.5GB×4w | **6 GB** |
| **Logs Sistema** | Server 1 | - | Continuo | Diario | 80MB/día | 80MB×30d | **2.4 GB** |
| **Métricas Nagios** | Server 1 | - | Cada 5min | Continuo | 2KB/métrica | 288×2KB×30d | **17.3 MB** |
| **Consultas PostgreSQL** | Server 4 | 500 | 50 queries/día | Diario | 1.5KB/query | 500×50×1.5KB×30d | **1.1 GB** |
| **Sincronización BD** | Server 4 | - | 1 vez/hora | Continuo | 5MB/sync | 24×5MB×30d | **3.6 GB** |

#### Identificación de recursos utilizados
#### Estimación del consumo energético y huella de carbono

Instancias de la nube: Estimar el consumo energético de las instancias de la nube (puedes utilizar valores aproximados o herramientas del proveedor como el Carbon Footprint Calculator de AWS, o similares de GCP/Azure).

### **CONSUMO ENERGÉTICO POR INSTANCIA**
| **Server** | **Tipo Instancia** | **vCPU** | **RAM (GB)** | **Consumo Base (W)** | **Factor Carga** | **Consumo Real (W)** | **kWh/día** | **kWh/mes** |
|------------|-------------------|----------|--------------|---------------------|------------------|-------------------|-------------|-------------|
| Server 1 | t2.xlarge | 4 | 16 | 45W | 70% | 31.5W | 0.756 | 22.68 |
| Server 2 | t3.small | 2 | 2 | 15W | 80% | 12W | 0.288 | 8.64 |
| Server 3 | t2.micro | 1 | 1 | 8W | 40% | 3.2W | 0.077 | 2.31 |
| Server 4 | t3.micro | 2 | 1 | 10W | 60% | 6W | 0.144 | 4.32 |
| Server 5 | t3.small | 2 | 2 | 15W | 50% | 7.5W | 0.180 | 5.40 |

**TOTAL CONSUMO: 60.2W → 1.445 kWh/mes → 17.34 kWh/año**

### **HUELLA DE CARBONO AWS (Región eu-west-1)**
**Factor de emisión eu-west-1 (Irlanda): 0.316 kg CO₂/kWh**
| **Server** | **kWh/año** | **Factor CO₂** | **kg CO₂/año** |
|------------|-------------|----------------|----------------|
| Server 1 | 272.16 | 0.316 | 86 kg |
| Server 2 | 103.68 | 0.316 | 33 kg |
| Server 3 | 27.72 | 0.316 | 9 kg |
| Server 4 | 51.84 | 0.316 | 16 kg |
| Server 5 | 64.80 | 0.316 | 20 kg |

**TOTAL HUELLA CARBONO: 164 kg CO₂/año**


### **FÓRMULA DE CÁLCULO AWS**
> Emisiones CO₂ = (vCPU × Factor_CPU + RAM × Factor_RAM + Storage × Factor_Storage) 
                × Horas_Uso × Factor_Región × PUE_Datacenter

Tráfico generado por el streaming: Estimar el consumo energético en función de watts por GB transferido.

### Tráfico de Streaming 
**Del cálculo anterior:**
- **Streaming Audio:** 513 GB/mes
- **Streaming Video:** 608 GB/mes
- **TOTAL STREAMING:** 1.121 GB/mes = 13.452 GB/año

### Consumo Energético por GB Transferido
**Factores de Consumo AWS:**
- **Transferencia de datos:** 0.006 kWh/GB (incluye red + procesamiento)
- **Encoding/Transcoding:** 0.012 kWh/GB (FFmpeg + CPU intensivo)
- **Storage I/O:** 0.002 kWh/GB (lectura desde EBS)

**TOTAL: 0.020 kWh/GB para streaming**

### Cálculo Consumo por Tipo de Streaming
| **Tipo Streaming** | **GB/mes** | **GB/año** | **kWh/GB** | **kWh/mes** | **kWh/año** |
|-------------------|------------|------------|------------|-------------|-------------|
| **Audio (Icecast)** | 513 | 6.156 | 0.015 | 7.70 | 92.34 |
| **Video (FFmpeg)** | 608 | 7.296 | 0.025 | 15.20 | 182.40 |
| **TOTAL** | 1.121 | 13.452 | - | 22.90 | 274.74 |

### Fórmulas de Cálculo
```
Consumo Audio = GB_transferidos × 0.015 kWh/GB
Consumo Video = GB_transferidos × 0.025 kWh/GB

Ejemplo:
Consumo Audio = 513 GB/mes × 0.015 kWh/GB = 7.70 kWh/mes
Consumo Video = 608 GB/mes × 0.025 kWh/GB = 15.20 kWh/mes

Total Streaming = 22.90 kWh/mes × 12 meses = 274.74 kWh/año

Consumo de servidores virtuales o servicios en funcionamiento continuo.
```
### Instancias EC2 en Operación

| **Server** | **Tipo Instancia** | **Consumo (W)** | **Horas/año** | **kWh/año** |
|------------|-------------------|-----------------|---------------|-------------|
| Server 1 (Monitorización) | t2.xlarge | 31.5 | 8760 | 276.1 |
| Server 2 (Streaming) | t3.small | 12.0 | 8760 | 105.1 |
| Server 3 (DNS+FTP) | t2.micro | 3.2 | 8760 | 28.0 |
| Server 4 (Base Datos) | t3.micro | 6.0 | 8760 | 52.6 |
| Server 5 (Backups) | t3.small | 7.5 | 7300 | 54.8 |

**TOTAL: 516.6 kWh/año**

### Fórmula de Cálculo


Consumo_Anual = Potencia_Base × Factor_Carga × Horas_Funcionamiento ÷ 1000

Donde:
- Potencia_Base: Watts nominales de la instancia
- Factor_Carga: % utilización promedio (0.4 - 0.8)
- Horas_Funcionamiento: 8760h/año (24/7) o 7300h/año (20h/día)

Ejemplo Server 1:
Consumo = 45W × 0.7 × 8760h ÷ 1000 = 276.12 kWh/año
``` ```
Conversión de energía (kWh) a emisiones (kg CO₂ eq.): Utiliza factores de equivalencia para convertir el consumo energético en emisiones de carbono.

Se ha usado la calculadora de CeroCO2.org.

## Conversión de Energía a Emisiones de CO₂
### Factor de Equivalencia CeroCO2.org
**Fuente:** https://www.ceroco2.org/calculadoras/

**Factor España:** 0.256 kg CO₂/kWh (mix energético español)

  ### Cálculo de Emisiones del Proyecto

**Consumo total:** 516.6 kWh/año  
**Factor CeroCO2:** 0.256 kg CO₂/kWh  

 Emisiones CO₂ = Consumo_kWh × Factor_CeroCO2

Emisiones = 516.6 kWh/año × 0.256 kg CO₂/kWh = 132.2 kg CO₂/año


### Fórmula General
```
Emisiones_CO₂ = kWh_consumidos × 0.256

Donde:
- kWh_consumidos: Consumo energético anual
- 0.256: Factor emisión España (kg CO₂/kWh) según CeroCO2.org
```

#### Recursos

Carbon Trust

Factores de emisiones medias globales o por región del proveedor de nube.






Propuesta de medidas de reducción u optimización:

¿Reducir las horas de funcionamiento de los servicios?

Servicios que SÍ se pueden optimizar:
Server 5 (Backups): De 20h/día a 12h/día = -20% consumo (10.9 kg CO₂e/año menos)
Server 2 (Streaming): Modo standby en horario valle (02:00-07:00) = -15% consumo
Servicios no críticos: Apagar dashboards/reportes durante madrugada

Servicios que NO se pueden reducir:
Server 1 (Monitorización): Debe estar 24/7 para detectar fallos
Server 3 (DNS): Crítico, debe resolver nombres siempre
Server 4 (Base Datos): Aplicaciones dependen 24/7

Impacto estimado: -25% consumo total = -40.8 kg CO₂e/año

¿Utilizar energía renovable para los servicios?
Cambio de región: Migrar a us-west-2 (Oregon) con 95% renovable
Factor actual: 0.316 vs Oregon: 0.025 kg CO₂e/kWh
Reducción: 163.2 → 12.9 kg CO₂e/año (-92%)
 
#### Propuesta de medidas de reducción u optimización

