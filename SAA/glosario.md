[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](./README.md)

# Glosario — vocabulario y siglas de examen

> Referencia lingüística única del SAA: **siglas** (para no confundirlas), **jerga cloud** e **inglés de enunciado**. Búscalo con Ctrl+F durante el repaso.

## 🔤 Siglas / Acronyms

### ⚠️ Las que más se confunden (pares clave)

| Sigla A | Sigla B | Diferencia en una línea |
|---|---|---|
| **SG** (Security Group) | **NACL** (Network ACL) | SG = **stateful**, a nivel ENI/instancia, solo ALLOW · NACL = **stateless**, a nivel subred, ALLOW + DENY (abre puertos efímeros) |
| **CRR** (Cross-Region Replication) | **SRR** (Same-Region Replication) | CRR = entre regiones (DR/compliance) · SRR = misma región (agregación de logs) |
| **OAC** (Origin Access Control) | **OAI** (Origin Access Identity) | Ambos restringen S3 a CloudFront · **OAC = el nuevo/recomendado** · OAI = legado |
| **RTO** (Recovery Time Objective) | **RPO** (Recovery Point Objective) | RTO = cuánto **tiempo** tardas en recuperarte · RPO = cuántos **datos** (tiempo) puedes perder |
| **DX** (Direct Connect) | **DXGW** / **TGW** | DX = conexión física dedicada · DXGW = conecta DX a varias VPCs/regiones · TGW = hub-and-spoke entre miles de VPCs (peering transitivo) |
| **CGW** (Customer Gateway) | **VGW** (Virtual Private Gateway) | CGW = lado **on-prem** del VPN · VGW = lado **AWS** del VPN |
| **SSE-S3** / **SSE-KMS** | **SSE-C** | SSE-S3 = claves de S3 (AES-256) · SSE-KMS = claves KMS · SSE-C = claves **del cliente** (header `-customer-*`) |
| **ALB** | **NLB** | ALB = L7 (HTTP, path/host routing) · NLB = L4 (TCP/UDP, **IP estática**, ultra-baja latencia) |
| **Multi-AZ** | **Read Replica** | Multi-AZ = HA (standby síncrono, failover) · Read Replica = escalar lecturas (async) |
| **GSI** | **LSI** | GSI = índice con otra partition key (se crea cuando sea) · LSI = misma partition key, otra sort key (solo al crear la tabla) |

### Networking & VPC

| Sigla | Nombre completo | Qué es |
|---|---|---|
| **VPC** | Virtual Private Cloud | red privada aislada en AWS |
| **CIDR** | Classless Inter-Domain Routing | notación de rangos de IP (/16 → /28 en VPC) |
| **ENI** | Elastic Network Interface | tarjeta de red virtual; la IP privada/secundaria vive aquí |
| **EIP** | Elastic IP | IP pública fija que puedes mover entre instancias |
| **IGW** | Internet Gateway | da acceso a Internet a la VPC |
| **NAT** | Network Address Translation | salida a Internet para subredes privadas (NAT Gateway) |
| **EIGW** | Egress-Only Internet Gateway | salida solo **IPv6** |
| **SNI** | Server Name Indication | permite varios certs TLS en un mismo ALB/listener |
| **TGW** | Transit Gateway | hub central que conecta miles de VPCs (transitivo) |
| **DXGW** | Direct Connect Gateway | conecta un DX a VPCs en varias regiones |

### Seguridad & identidad

| Sigla | Nombre completo | Qué es |
|---|---|---|
| **IAM** | Identity and Access Management | usuarios, grupos, roles, políticas |
| **STS** | Security Token Service | credenciales temporales (assume role, federación) |
| **MFA** | Multi-Factor Authentication | segundo factor de autenticación |
| **SCP** | Service Control Policy | límites de permisos a nivel de Organization/cuenta |
| **KMS** | Key Management Service | gestión de claves de cifrado |
| **CMK** | Customer Master Key | (hoy "KMS key") la clave maestra en KMS |
| **HSM** | Hardware Security Module | CloudHSM — hardware dedicado, FIPS 140-2 L3 |
| **ACM** | AWS Certificate Manager | certificados SSL/TLS gestionados |
| **WAF** | Web Application Firewall | protección L7 (SQLi, XSS, rate limiting) |
| **SAML / OIDC** | — | protocolos de federación de identidad |

### Bases de datos & migración

| Sigla | Nombre completo | Qué es |
|---|---|---|
| **RDS** | Relational Database Service | BD SQL gestionada |
| **DAX** | DynamoDB Accelerator | caché en memoria (microsegundos) para DynamoDB |
| **OLTP / OLAP** | Transaction / Analytical Processing | transaccional (RDS) vs analítico/data warehouse (Redshift) |
| **WCU / RCU** | Write / Read Capacity Units | unidades de capacidad de DynamoDB |
| **DMS** | Database Migration Service | migrar BDs (homogénea/heterogénea) |
| **SCT** | Schema Conversion Tool | convierte el esquema en migración heterogénea |
| **CDC** | Change Data Capture | replicación continua de cambios (DMS) |
| **PITR** | Point-In-Time Recovery | restaurar a un instante exacto |

### Cómputo, storage & DR

| Sigla | Nombre completo | Qué es |
|---|---|---|
| **AMI** | Amazon Machine Image | plantilla para lanzar EC2 |
| **ASG** | Auto Scaling Group | escala instancias y reemplaza las no sanas |
| **RI / SP** | Reserved Instance / Savings Plan | descuento por compromiso 1-3 años |
| **IMDS** | Instance Metadata Service | metadatos de la instancia (usa **IMDSv2**) |
| **EBS / EFS** | Elastic Block Store / File System | disco de bloque (1 AZ) / NFS compartido (multi-AZ) |
| **DLM** | Data Lifecycle Manager | automatiza snapshots de EBS |
| **VTL** | Virtual Tape Library | Tape Gateway — reemplaza cintas físicas |
| **DR** | Disaster Recovery | recuperación ante desastres |
| **MGN / DRS** | Application Migration / Elastic DR | lift-and-shift / replicación continua para DR |
| **IaC / CFN** | Infrastructure as Code / CloudFormation | infraestructura declarativa (JSON/YAML) |
| **TTL** | Time To Live | cuánto se cachea un registro DNS (Route 53) |

## Jerga cloud / AWS

| Término | Español (contexto AWS) | In English |
|---|---|---|
| **Backtrack** | (Aurora) rebobinar la BD a un instante anterior sin restaurar backup | rewind an Aurora MySQL DB to an earlier point in time, in place |
| **Bandwidth** | ancho de banda; capacidad de transferencia de datos | how much data can flow per second — Direct Connect, VPN, EBS throughput |
| **bias traffic / bias dial** | inclinar/sesgar el reparto de tráfico hacia ciertos endpoints | skew the share of traffic sent to a group — Global Accelerator traffic dial / weights |
| **boot / reboot** | arrancar / reiniciar | start up / restart a machine |
| **bootstrap / bootstrapping** | script de arranque que auto-configura la instancia | scripts run at first boot to configure a machine — EC2 user data |
| **bump-in-the-wire** | dispositivo insertado en línea, transparente a la topología | an appliance placed inline in the traffic path — Gateway Load Balancer |
| **burstable** | con capacidad de ráfaga (baseline + créditos) | can "burst" above a baseline using credits — T-family EC2, gp2/gp3 EBS |
| **bursting** | funcionar en ráfaga, superar el baseline temporalmente | temporarily exceeding baseline performance by spending accumulated credits |
| **concurrency spikes** | picos de concurrencia (ejecuciones simultáneas) | sudden surges of simultaneous executions — Lambda concurrency |
| **connection pooler** | agrupador de conexiones reutilizables a la BD | manages/reuses DB connections to avoid exhaustion — RDS Proxy |
| **cooldown period** | periodo de enfriamiento tras un escalado | a pause after a scaling action before the next one — Auto Scaling |
| **Envelope (encryption)** | cifrado de sobre: cifrar la clave de datos con otra clave maestra | encrypting a data key with a master key — KMS envelope encryption |
| **failover** | conmutación por error al recurso de respaldo | automatic switch to a backup when the primary fails |
| **fan-out** | difusión 1→N: un mensaje entregado a muchos consumidores en paralelo | one message delivered to many subscribers at once — SNS → multiple SQS/Lambda |
| **fleet** | flota: conjunto de instancias gestionadas juntas | a group of instances managed as one — Spot Fleet, EC2 Fleet |
| **idle** | inactivo, ocioso | not in use, sitting without activity |
| **idle timeout** | tiempo de espera por inactividad antes de cerrar la conexión | how long a connection stays open with no traffic — ELB default 60s |
| **multi-tier / three-tier** | arquitectura de varias / tres capas | split into layers — classic 3-tier: web, app, DB |
| **outage** | caída / interrupción del servicio | a period when a service is down or unavailable |
| **passthrough** | paso directo sin terminar/descifrar el tráfico | forwarding traffic without terminating it — TLS passthrough on NLB |
| **purge / to purge** | purgar: vaciar/eliminar todo el contenido de golpe | delete everything at once — SQS PurgeQueue, clear a cache |
| **scratch storage / scratch data** | almacenamiento temporal de trabajo, alto rendimiento, sin durabilidad | temporary high-speed working storage, not durable — FSx for Lustre, instance store |
| **shift traffic** | desviar/trasladar el tráfico de un destino a otro | gradually move requests between targets — blue/green, canary, Route 53 |
| **spoofed / spoofing** | suplantado / falsificado (identidad o IP falsa) | faking a source identity — IP/email spoofing |
| **standby** | recurso en espera, listo para el relevo | a ready, waiting replica that takes over on failure — Multi-AZ |
| **stateless / stateful** | sin estado / con estado (no recuerda / sí recuerda la sesión previa) | stateless keeps no session between requests; stateful remembers prior state — NACL (stateless) vs Security Group (stateful) |
| **stripe / striping** | distribuir datos entre varios volúmenes para sumar rendimiento (RAID 0) | spreading data across multiple EBS volumes to combine IOPS — "stripe on EC2" = RAID 0 |
| **swap space** | espacio de intercambio en disco usado como memoria de overflow | disk space used as overflow when RAM is full |
| **switchover** | conmutación planificada y ordenada al standby (a diferencia del failover, que es por fallo) | a planned, graceful switch to the standby — RDS Multi-AZ switchover (vs unplanned failover) |
| **synchronous standby** | réplica en espera con replicación síncrona | standby kept in sync in real time — RDS Multi-AZ |
| **tape backup** | copia de seguridad en cinta (virtual en AWS) | backup to (virtual) tape — Storage Gateway Tape Gateway / VTL |
| **threshold** | umbral que dispara una acción | a value that triggers an action when crossed — CloudWatch alarm |
| **throttled** | limitado/estrangulado: peticiones rechazadas o ralentizadas por superar el límite | requests rejected/slowed for exceeding the rate limit — "you get throttled" |
| **throttling** | limitación del ritmo de peticiones | deliberately capping the request rate — API Gateway, Lambda, DynamoDB |
| **throughput** | rendimiento; caudal de datos por unidad de tiempo | amount of data processed per unit of time — EBS MB/s, Kinesis shard, network |
| **tier** | capa / nivel de una arquitectura | a layer of an architecture — web / app / database tier |
| **traffic dials** | (Global Accelerator) % de tráfico enviado a un grupo de endpoints | a knob to control the % of traffic to an endpoint group |

## Inglés de enunciado (vocabulario general)

| Término | Español | In English |
|---|---|---|
| **assess** | evaluar, valorar | to evaluate or judge |
| **beyond** | más allá de; además de | further than; in addition to |
| **custom-built application** | aplicación hecha a la medida (no comercial / lista para usar) | an app built specifically for a need, not off-the-shelf |
| **forecast** | pronosticar, prever; pronóstico / previsión | to predict future values from data — forecast demand / capacity |
| **gathered** | reunido, recopilado, recogido | collected together — "data gathered from sensors" |
| **gotchas** | trampas, detalles que sorprenden | tricky details that catch you out |
| **hence** | por eso, por lo tanto | therefore, for that reason |
| **knobs** | controles / perillas ajustables de configuración | adjustable settings — "tuning knobs" |
| **lessen** | reducir, disminuir, aminorar | to make something smaller or less |
| **leverage** | aprovechar, hacer uso de | to make use of something to your advantage |
| **seamless / seamlessly** | sin interrupciones, transparente para el usuario | smooth, without disruption |
| **shelves** | estantes (plural de *shelf*); (verbo *to shelve*) aparcar / posponer | shelves = storage racks; to shelve = put aside / postpone |
| **standalone** | independiente, autónomo (funciona por sí solo) | self-contained, works on its own — a standalone instance / service |
| **streamline** | optimizar, simplificar un proceso | to make a process simpler / more efficient |
| **suffice** | bastar, ser suficiente | to be enough |
| **surcharge** | recargo, sobrecoste | an extra charge added on top |
| **trade-off(s)** | compensación (ganas algo a cambio de perder otra cosa) | a balance between two things you can't both maximize |
| **under the hood** | internamente, por debajo (cómo funciona por dentro) | how something works internally |
| **undergo** | someterse a, pasar por (un proceso) | to experience or go through a process — "undergo maintenance" |
| **undertaken** | emprendido, llevado a cabo | started or carried out (a task) |
| **uneven** | desigual, irregular | not balanced or equal — "uneven WCU consumption" |
| **workaround** | solución alternativa, apaño | a way around a problem without fixing the root cause |
| **yield** | rendir, producir, dar | to produce/return — "datasets that yield low profit" = produce little profit |

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](./README.md)
