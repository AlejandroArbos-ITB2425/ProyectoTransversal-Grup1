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
| 1 | ElasticSearch, Kibana, Nagios | t3.small |
| 2 | Web, Audio, Streaming | t3.small |
| 3 | DNS, FTP | t2.micro |
| 4 | Base de Datos (PGSQL) | t3.small |
| 5 | Copias de Seguridad | t2.micro |

## Configuración de Servidor 1
#### ElasticSearch + Kibana
### Nagios

## Configuración de Servidor 2
#### Web (Nginx)
#### Audio
#### Streaming

## Configuración de Servidor 3
#### DNS
#### FTP

## Configuración de Servidor 4
#### Base Datos

## Configuración de Servidor 5
#### Copias seguridad


