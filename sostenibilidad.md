# 4. Sostenibilidad

## Sostenibilidad y eficiencia energética

Alineados con nuestros valores empresariales y los Objetivos de Desarrollo Sostenible (ODS), es fundamental que el proyecto se diseñe con un enfoque claro de sostenibilidad. Buscamos optimizar el uso de energía y utilizar soluciones que reduzcan el impacto ambiental de nuestras operaciones. Queremos explorar el uso de fuentes de energía renovable, así como implementar prácticas de eficiencia energética dentro del Centro de Procesamiento de Datos (CPD).

### Cálculo de la huella ecológica del proyecto realizado
#### Identificación de recursos utilizados:

Servicios desplegados: ¿Qué tipo de máquinas, servicios en la nube y protocolos se están utilizando?

TIPOS DE MÁQUINAS (AWS EC2):
1x t2.xlarge (4 vCPU, 16GB RAM) - Server 1 Monitorización

2x t3.small (2 vCPU, 2GB RAM) - Server 2 Streaming + Server 5 Backups

1x t2.micro (1 vCPU, 1GB RAM) - Server 3 DNS+FTP

1x t3.micro (2 vCPU, 1GB RAM) - Server 4 Base Datos

SERVICIOS EN LA NUBE (AWS):
EC2 - 5 instancias Ubuntu 24.04 LTS

EBS - 6 volúmenes (5×8GB + 1×100GB)

VPC - Red privada virtual

Security Groups - Firewall de red

Internet Gateway - Conectividad externa

PROTOCOLOS UTILIZADOS:
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

CPU:
Server 1 (t2.xlarge): 4 vCPU - Uso promedio 60-80% (Elasticsearch + Nagios + Kibana)
Server 2 (t3.small): 2 vCPU - Uso promedio 70-90% (FFmpeg encoding + Icecast + Darkice)
Server 3 (t2.micro): 1 vCPU - Uso promedio 30-50% (BIND9 + vsftpd)
Server 4 (t3.micro): 2 vCPU - Uso promedio 50-70% (PostgreSQL + consultas)
Server 5 (t3.small): 2 vCPU - Uso promedio 40-60% (rsync + backups)
TOTAL: 11 vCPU utilizadas

RAM:
Server 1: 16GB - Uso 12-14GB (Elasticsearch buffer pool + cache)
Server 2: 2GB - Uso 1.5-1.8GB (streaming buffers + transcoding)
Server 3: 1GB - Uso 600-800MB (DNS cache + FTP connections)
Server 4: 1GB - Uso 800-950MB (PostgreSQL + connections)
Server 5: 2GB - Uso 1-1.5GB (backup processes + file cache)
TOTAL: 22GB RAM - Uso efectivo ~18GB

ALMACENAMIENTO:
Server 1: 8GB EBS - Uso 6GB (SO + logs + índices Elasticsearch)
Server 2: 8GB EBS - Uso 5GB (SO + archivos multimedia temporales)
Server 3: 8GB EBS - Uso 4GB (SO + archivos FTP)
Server 4: 8GB EBS - Uso 6GB (SO + bases de datos PostgreSQL)
Server 5: 8GB + 100GB EBS - Uso 6GB + 60GB (SO + backups históricos)
TOTAL: 132GB EBS - Uso efectivo ~87GB

ANCHO DE BANDA:
Tráfico de entrada: ~500GB/mes (uploads FTP + datos monitorización)
Tráfico de salida: ~2TB/mes (streaming audio/video + web + descargas)
Tráfico interno: ~200GB/mes (backups + sincronización entre servers)
Picos streaming: 50Mbps durante eventos (Server 2)
Transferencias FTP: 20Mbps promedio (Server 3)
Consultas BD: 5Mbps constante (Server 4)
TOTAL: ~2.7TB/mes transferencia total

Previsión de uso: ¿Cuántas horas de funcionamiento, ¿cuántos usuarios y tráfico estimado se prevé?

HORAS DE FUNCIONAMIENTO:
Server 1 (Monitorización): 24/7 = 8.760 horas/año (crítico, nunca se apaga)
Server 2 (Streaming): 24/7 = 8.760 horas/año (servicio continuo streaming)
Server 3 (DNS+FTP): 24/7 = 8.760 horas/año (DNS siempre activo)
Server 4 (Base Datos): 24/7 = 8.760 horas/año (BD siempre disponible)
Server 5 (Backups): 20h/día = 7.300 horas/año (4h standby nocturno)

USUARIOS
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
#### Recursos
#### Propuesta de medidas de reducción u optimización

