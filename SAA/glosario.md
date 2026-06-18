[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](./README.md)

# Glosario — vocabulario de examen (EN → ES)

> Inglés y jerga cloud que aparece en los enunciados del SAA. El término va en inglés; la explicación en español + una definición breve en inglés para **interiorizar el concepto, no solo traducirlo**. Búscalo con Ctrl+F durante el repaso.

## Jerga cloud / AWS

| Término | Español (contexto AWS) | In English |
|---|---|---|
| **Backtrack** | (Aurora) rebobinar la BD a un instante anterior sin restaurar backup | rewind an Aurora MySQL DB to an earlier point in time, in place |
| **boot / reboot** | arrancar / reiniciar | start up / restart a machine |
| **bootstrap / bootstrapping** | script de arranque que auto-configura la instancia | scripts run at first boot to configure a machine — EC2 user data |
| **bump-in-the-wire** | dispositivo insertado en línea, transparente a la topología | an appliance placed inline in the traffic path — Gateway Load Balancer |
| **burstable** | con capacidad de ráfaga (baseline + créditos) | can "burst" above a baseline using credits — T-family EC2, gp2/gp3 EBS |
| **bursting** | funcionar en ráfaga, superar el baseline temporalmente | temporarily exceeding baseline performance by spending accumulated credits |
| **concurrency spikes** | picos de concurrencia (ejecuciones simultáneas) | sudden surges of simultaneous executions — Lambda concurrency |
| **connection pooler** | agrupador de conexiones reutilizables a la BD | manages/reuses DB connections to avoid exhaustion — RDS Proxy |
| **cooldown period** | periodo de enfriamiento tras un escalado | a pause after a scaling action before the next one — Auto Scaling |
| **failover** | conmutación por error al recurso de respaldo | automatic switch to a backup when the primary fails |
| **fleet** | flota: conjunto de instancias gestionadas juntas | a group of instances managed as one — Spot Fleet, EC2 Fleet |
| **idle** | inactivo, ocioso | not in use, sitting without activity |
| **idle timeout** | tiempo de espera por inactividad antes de cerrar la conexión | how long a connection stays open with no traffic — ELB default 60s |
| **multi-tier / three-tier** | arquitectura de varias / tres capas | split into layers — classic 3-tier: web, app, DB |
| **outage** | caída / interrupción del servicio | a period when a service is down or unavailable |
| **passthrough** | paso directo sin terminar/descifrar el tráfico | forwarding traffic without terminating it — TLS passthrough on NLB |
| **scratch storage / scratch data** | almacenamiento temporal de trabajo, alto rendimiento, sin durabilidad | temporary high-speed working storage, not durable — FSx for Lustre, instance store |
| **spoofed / spoofing** | suplantado / falsificado (identidad o IP falsa) | faking a source identity — IP/email spoofing |
| **standby** | recurso en espera, listo para el relevo | a ready, waiting replica that takes over on failure — Multi-AZ |
| **stripe / striping** | distribuir datos entre varios volúmenes para sumar rendimiento (RAID 0) | spreading data across multiple EBS volumes to combine IOPS — "stripe on EC2" = RAID 0 |
| **swap space** | espacio de intercambio en disco usado como memoria de overflow | disk space used as overflow when RAM is full |
| **synchronous standby** | réplica en espera con replicación síncrona | standby kept in sync in real time — RDS Multi-AZ |
| **tape backup** | copia de seguridad en cinta (virtual en AWS) | backup to (virtual) tape — Storage Gateway Tape Gateway / VTL |
| **threshold** | umbral que dispara una acción | a value that triggers an action when crossed — CloudWatch alarm |
| **throttling** | limitación del ritmo de peticiones | deliberately capping the request rate — API Gateway, Lambda, DynamoDB |
| **throughput** | rendimiento; caudal de datos por unidad de tiempo | amount of data processed per unit of time — EBS MB/s, Kinesis shard, network |
| **tier** | capa / nivel de una arquitectura | a layer of an architecture — web / app / database tier |
| **traffic dials** | (Global Accelerator) % de tráfico enviado a un grupo de endpoints | a knob to control the % of traffic to an endpoint group |

## Inglés de enunciado (vocabulario general)

| Término | Español | In English |
|---|---|---|
| **assess** | evaluar, valorar | to evaluate or judge |
| **beyond** | más allá de; además de | further than; in addition to |
| **gotchas** | trampas, detalles que sorprenden | tricky details that catch you out |
| **hence** | por eso, por lo tanto | therefore, for that reason |
| **knobs** | controles / perillas ajustables de configuración | adjustable settings — "tuning knobs" |
| **leverage** | aprovechar, hacer uso de | to make use of something to your advantage |
| **seamless / seamlessly** | sin interrupciones, transparente para el usuario | smooth, without disruption |
| **streamline** | optimizar, simplificar un proceso | to make a process simpler / more efficient |
| **suffice** | bastar, ser suficiente | to be enough |
| **surcharge** | recargo, sobrecoste | an extra charge added on top |
| **trade-off(s)** | compensación (ganas algo a cambio de perder otra cosa) | a balance between two things you can't both maximize |
| **under the hood** | internamente, por debajo (cómo funciona por dentro) | how something works internally |
| **undertaken** | emprendido, llevado a cabo | started or carried out (a task) |
| **uneven** | desigual, irregular | not balanced or equal — "uneven WCU consumption" |
| **workaround** | solución alternativa, apaño | a way around a problem without fixing the root cause |
| **yield** | rendir, producir, dar | to produce/return — "datasets that yield low profit" = produce little profit |

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](./README.md)
