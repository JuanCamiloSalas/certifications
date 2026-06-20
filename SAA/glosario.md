[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](./README.md)

# Glosario — vocabulario de examen (EN → ES)

> Inglés y jerga cloud que aparece en los enunciados del SAA. El término va en inglés; la explicación en español + una definición breve en inglés para **interiorizar el concepto, no solo traducirlo**. Búscalo con Ctrl+F durante el repaso.

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
