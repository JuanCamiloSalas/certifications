# Vocabulario inglés del CCP

Listado de **palabras y frases en inglés** que aparecen en preguntas del simulacro/examen y que **no son triggers directos de un servicio**, pero conviene entender para no quedarse atascado en la traducción.

[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Trigger_words-175074?style=for-the-badge)](./TRIGGERS.md)

> [!TIP]
> Si una palabra apunta directamente a un servicio AWS (ej. "**high-frequency trading**" → NLB), está en **TRIGGERS.md**. Aquí van las palabras que solo necesitas para **entender la pregunta**.

---

## A

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **address** *(verbo)* | abordar, tratar, resolver | "to **address** security concerns" = abordar inquietudes de seguridad |
| **adhering to** | cumplir con, ajustarse a | "**adhering to** compliance standards" = cumpliendo con estándares de cumplimiento |
| **accurately** | con precisión, certeramente | Aparece con Forecast / Cost Explorer ("**accurately** forecast costs") |
| **agility** | agilidad | Beneficio del Cloud — provisionar recursos en minutos. **NO es un pilar** del Well-Architected |
| **aim** *(sust./verbo)* | objetivo / apuntar a | "the **aim** of this approach is…" = el objetivo de este enfoque es… |
| **AWS environment** | entorno / infraestructura AWS del cliente | Frase genérica para referirse al conjunto de cuentas, VPCs, recursos del cliente |

## B

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **be trusted** | ser de confianza, generar confianza | "data must **be trusted**" = los datos deben ser confiables |
| **below** | por debajo de | "**below** the threshold" = por debajo del umbral (CloudWatch) |
| **boost** | impulsar, aumentar | "**boost** performance" = mejorar el rendimiento |
| **burden** | carga, peso | "regulatory **burden**" = carga regulatoria |

## C

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **close coupling** *(= tight coupling)* | acoplamiento estrecho | Anti-patrón. Lo opuesto y deseable: **loose coupling** (decouple → SQS/SNS/EventBridge) |
| **complying** *(con compliance)* | cumpliendo (con normativa) | "**complying** with HIPAA" = cumpliendo con HIPAA |
| **comprises** | comprende, consta de | "the framework **comprises** seven pillars" = el framework consta de siete pilares |
| **couple / decouple** | acoplar / desacoplar | Arquitectura: tightly coupled (mal) vs loosely coupled (bien) |
| **coverage** | cobertura | "test **coverage**", "Trusted Advisor **coverage**" |

## D

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **disposal** | eliminación, descarte | "data **disposal** policy" = política de eliminación de datos (S3 lifecycle) |
| **durable / durability** | duradero / durabilidad | S3 ofrece 11 nueves de **durability** |

## E

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **elasticity** | elasticidad | Característica del Cloud — auto-escalar según demanda. **NO es un pilar** del Well-Architected |
| **enhance** | mejorar, potenciar | "**enhance** performance" = mejorar el rendimiento |
| **entail** | implicar, conllevar | "this approach will **entail** higher costs" = este enfoque implicará mayores costos |
| **exchange results** | intercambiar resultados / hacer trade-off | Compromiso entre opciones (no es un servicio) |
| **expenditures** | gastos, desembolsos | "over-**expenditures**" = sobre-gastos; CAPEX vs OPEX |

## F

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **fall under** | pertenecer a, estar dentro de | "this **falls under** the customer's responsibility" = esto cae bajo la responsabilidad del cliente |
| **fixing flaws** | arreglar fallos / defectos | "**fixing flaws** in the code" = arreglando fallos en el código |
| **flexibility** | flexibilidad | Beneficio cloud genérico (resize, change services). No es pilar |
| **forecast** *(verbo/sustantivo)* | predecir / pronóstico | Ojo: si es **costos** → Cost Explorer; si es **demanda/series temporales** → Amazon Forecast |

## G

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **gain insight on** | obtener información sobre | "**gain insight on** usage patterns" = obtener información sobre patrones de uso |
| **gaps** | huecos, brechas | "security **gaps**" = brechas de seguridad |

## I

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **idle** | inactivo, ocioso | "**idle** resources" = recursos sin uso (Compute Optimizer / Sustainability) |

## L

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **lessons** *(learned)* | lecciones (aprendidas) | "**lessons learned**" = lecciones aprendidas (de fallos / proyectos) |
| **leverage** *(verbo)* | aprovechar, sacar partido de | "**leverage** AWS services" = aprovechar los servicios de AWS |
| **lie** *(verbo de ubicación)* | encontrarse, estar situado | "they all **lie** within 100 km" = todos se encuentran dentro de 100 km. Aquí *lie* NO significa "mentir", significa **estar ubicado** |

## M

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **myriad** *(adj./sust.)* | innumerable, infinidad de | "AWS provides a **myriad** of services" = AWS provee una infinidad de servicios |

## O

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **outcome** | resultado, desenlace | "business **outcome**" = resultado de negocio (CAF Business perspective) |
| **overhead** | sobrecarga, costo adicional | "operational **overhead**" = sobrecarga operativa (managed services / serverless la reducen) |

## P

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **purchasing** | compra, adquisición | "EC2 **purchasing** options" = opciones de compra de EC2 |

## R

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **regarding** | con respecto a, en relación con | "**regarding** the support plan…" = con respecto al plan de soporte |
| **regarded** | considerado | "is **regarded** as" = es considerado como |
| **reinforce** | reforzar | "**reinforce** security" = reforzar la seguridad |
| **reliability** *(noun)* | fiabilidad | Pilar del Well-Architected Framework. Sustantivo de "reliable" |
| **rely on** | depender de, apoyarse en | "we **rely on** legacy systems" = dependemos de sistemas heredados (señal de modernización) |
| **resilience / resilient** | resiliencia / resiliente | Capacidad de **recuperarse de fallos** — concepto del pilar **Reliability** |

## S

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **seamlessly** | sin interrupciones, de forma transparente | "scales **seamlessly**" = escala sin fricción (típico de servicios serverless/managed) |
| **shift** | desplazar, mover | Cuidado: si es "**lift and shift**" → migración (Rehost / MGN) |
| **skyrocketed** | se disparó, subió drásticamente | "traffic **skyrocketed**" = el tráfico se disparó (→ Auto Scaling) |
| **sole** | único | Sinónimo de "solely" — elimina las opciones "shared" en preguntas de Responsabilidad Compartida |
| **steady** | constante, estable | "**steady** workload" = carga constante (→ Reserved Instance) |
| **suitable** | adecuado, apropiado | "**suitable** for archival" = adecuado para archivado |

## T

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **tailored** | a la medida, personalizado | "**tailored** solution" = solución a medida |
| **threat** | amenaza | Ojo: "**threat detection**" → GuardDuty; "**threat**" sin más es solo vocabulario |
| **threshold** | umbral, límite | CloudWatch alarms se basan en **thresholds** |
| **tighten** | endurecer, ajustar | "**tighten** security policies" = endurecer las políticas de seguridad |
| **tightly** *(coupled)* | (acoplado) fuertemente | Anti-patrón arquitectónico — opuesto a "loosely coupled" |
| **time-consuming** | que consume mucho tiempo | "manual setup is **time-consuming**" = la configuración manual lleva mucho tiempo |
| **trade** | comercio / intercambio | Si está solo → vocabulario; si es "**high-frequency trading**" → NLB / FSx Lustre |
| **transient** | transitorio, pasajero, momentáneo | "**transient network issues**" = problemas de red transitorios → patrones de **retry / fault tolerance** (Reliability) |

## U

| Palabra / Frase | Significado | Contexto típico en el CCP |
|---|---|---|
| **undergo** | someterse a, pasar por | "the database will **undergo** migration" = la BD pasará por migración |

---

## ⚠️ Falsos amigos / palabras ambiguas

Algunas palabras pueden parecer triggers pero **dependen del contexto** — léelas dos veces:

| Palabra | Si va sola | Si acompaña a… |
|---|---|---|
| **forecast** | Cost Explorer (forecast de costos) | "demand / sales / time-series" → **Amazon Forecast** |
| **trade** | vocabulario (intercambio) | "**high-frequency trading**" → **NLB / FSx Lustre** |
| **shift** | vocabulario (desplazar) | "**lift and shift**" → **MGN** (migración) |
| **threat** | vocabulario (amenaza) | "**threat detection**" → **GuardDuty** |
| **chip / chipset** | vocabulario | + "performance / multi-threading" → **bare-metal** EC2 |
| **forecast accuracy** | vocabulario (precisión) | + ML / time-series → **Amazon Forecast** |

---

[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Trigger_words-175074?style=for-the-badge)](./TRIGGERS.md)
