[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# Recta Final (16-22 junio) — Cierre de gaps + Simulacros + EXAMEN

> **Foco:** temario cerrado al 100%. Ya hay **2 simulacros hechos**. La fase ahora es **cerrar los gaps temáticos detectados + 2 simulacros más + consolidación**.
> **Hito al cierre:** 4 simulacros revisados + los 4 frentes débiles cerrados + llegar fresco al examen.
> **🎯 EXAMEN: lunes 22 de junio (AM)** — Inglés + 30 min ESL.

## 📍 Punto de partida real (martes 16 de junio)

- ✅ **Temario al 100%** (todas las secciones cerradas, incluido VPC y DR).
- ✅ Flashcards del repo completas (bloques 01-16).
- ✅ **Simulacro #1** (dom 15): **70%** (46/65). **Simulacro #2** (mar 16 AM): **64%** (42/65). Promedio **67%**.
- 🎯 Examen reagendado al **lunes 22** → **+6 días** que dan margen real para cerrar gaps con holgura (justo lo que faltaba).
- 🛌 **Domingo 21 NO es día de estudio:** descanso total antes del examen.

> **Lectura honesta:** el método funciona — High-Performing subió de 65% a 87% en cuanto estudiaste dirigido. El problema no es capacidad, es **amplitud**: Resilient sigue crónico (<50% en ambos simulacros) y aparecieron **2 frentes nuevos** (networking/Route 53 e identidad/gobierno). Estos días son para **cerrar esos frentes**, no para acumular simulacros a ciegas.

## ⏱️ Disponibilidad restante

| Día | Misión |
|---|---|
| **Mar 16** (hoy) | Simulacro #2 ✅ (AM). **PM:** repaso de los 23 errores → `errors/doc-maestro.md` + `review.md` |
| **Mié 17** | **Refuerzo dirigido** (sin simulacro): Frente 1 Resilient/DR + Frente 2 Networking/Route 53 |
| **Jue 18** | **Simulacro #3** (exam mode, AM) + repaso de errores PM |
| **Vie 19** | **Refuerzo dirigido**: Frente 3 Identidad/Gobierno + Frente 4 Cost + gaps de #3 |
| **Sáb 20** | **Simulacro #4** (exam mode, AM) + cierre ligero PM. **Último día de estudio** |
| **Dom 21** | 🛌 **Descanso total — sin estudio** |
| **Lun 22** | 🎯 **EXAMEN** |

> Ritmo: **simulacro → día de refuerzo → simulacro → cierre**. Alternar evita el agotamiento y deja que el repaso dirigido (no el test) cierre los gaps.

---

## 🎯 Los 4 frentes débiles (del Dojo #2)

### Frente 1 — Resilient / DR 🔴 (crónico: peor dominio en ambos simulacros)
- **Failover RDS Multi-AZ = el CNAME (DNS) se repunta al standby**, la IP no cambia. (Q54)
- **Failover de IP privada = ENI secundaria** que se mueve a otra instancia (NO Elastic IP, que es pública). (Q31)
- **Redundancia de Direct Connect = 2º DX al mismo VPC + VPN site-to-site de respaldo** (la redundancia apunta al VPC correcto, no a otro). (Q30)
- **Automatizar snapshots EBS, simple = Data Lifecycle Manager (DLM)** (no AWS Backup). (Q28)
- **Sincronización continua on-prem→AWS = DMS full load + CDC** (+SSL con certificado CA). (Q58)
- Repasar otra vez: **Multi-AZ vs Read Replica vs Aurora Global** (gap recurrente del Dojo #1).
- Cards: [03 · ASG](../cards/03-elb-asg/05-asg.md) · [04 · RDS](../cards/04-rds-aurora/01-rds.md) · [04 · Aurora Advanced](../cards/04-rds-aurora/04-aurora-advanced.md)

### Frente 2 — Networking & Route 53 🟠 (área nueva, no estaba en el repaso)
- **Route 53 routing policies:** Geoproximity (sesgar % de tráfico por geografía, con bias) vs Geolocation (mapear ubicación→endpoint) vs Weighted vs Latency. (Q42)
- **Sitio estático S3 + Route 53:** el nombre del bucket debe ser igual al dominio + dominio registrado (no hay regla de "misma región"). (Q21)
- **Clientes que necesitan IP estática para whitelist = NLB** (ALB no tiene IP estática). (Q32)
- **Acceso privado a DynamoDB/S3 desde VPC = gateway endpoint** (no interface, no NACL). (Q50)
- **Agotamiento de IPv4 + escalar = subnet IPv6-only** con CIDR amplio. (Q57)
- **Contenido estático global barato = CloudFront + S3** (no Global Accelerator). (Q56)
- Cards: [05 · Routing Policies 1](../cards/05-route53/02-routing-policies-1.md) · [05 · Routing Policies 2](../cards/05-route53/03-routing-policies-2.md) · [07 · CloudFront](../cards/07-cdn/01-cloudfront.md)

### Frente 3 — Identidad & gobierno multi-cuenta 🟠 (área nueva)
- **SSO con directorio corporativo existente en Organizations = IAM Identity Center + AD Connector** (+ SCP). (Q26, Q41)
- **Crear cuentas con baselines/guardrails preaprobados, menor esfuerzo = Control Tower Landing Zone** (no RAM, no Config). (Q62)
- Conecta con el gap de Dojo #1: AD Connector vs Simple AD.
- Cards: [13 · Federation](../cards/13-iam-advanced/02-federation.md) + bloque de Organizations/Control Tower.

### Frente 4 — Cost & fundamentos 🟡 (Cost cayó a 50%)
- **Rastrear costo por departamento = Cost Allocation Tags** (Budgets = alertas). ⚠️ Mismo concepto que fallaste en el CCP. (Q16)
- **Datos de archivo on-prem → escribir directo a Glacier Deep Archive** vía DataSync (no escalar en Standard + lifecycle). (Q13)
- **TB sobre línea lenta = transferencia offline/física** (Snowball / Data Transfer Terminal), no Transfer Acceleration. (Q45)
- **"key-value store" = DynamoDB** (no Aurora). (Q64)
- **Header SSE-S3/SSE-KMS = `x-amz-server-side-encryption`** (los `-customer-*` son solo SSE-C). (Q63)

### Frente transversal — Técnica de examen 🧠
- **Multi-select ("Select TWO"):** tu patrón es acertar una y picar **un** distractor plausible (Glue, GraphQL/AppSync, SES, VPC equivocado). Antes de avanzar: valida **cada** opción marcada por separado, no por "suena bien".
- Gestión de tiempo: ~2 min/pregunta. Marcar dudas y seguir.

---

## 📅 Plan día por día

### 🟦 Martes 16 — Repaso de errores del Simulacro #2 (PM)

- [ ] Revisar las **23 preguntas erróneas** pregunta por pregunta → volcar a [`errors/doc-maestro.md`](../errors/doc-maestro.md).
- [ ] Actualizar [`errors/review.md`](../errors/review.md) con la sección del Dojo #2.
- [ ] Confirmar los **4 frentes** y qué cards/comparativas tocar mañana.

### 🟦 Miércoles 17 — Refuerzo dirigido: Resilient/DR + Networking (sin simulacro)

- [ ] **AM — Frente 1 (Resilient/DR):** cards de RDS/Aurora + ASG. Fijar Multi-AZ failover (CNAME), ENI failover, redundancia DX+VPN, DLM, DMS CDC.
- [ ] **PM — Frente 2 (Networking/Route 53):** routing policies (Geoproximity vs Geolocation), NLB vs ALB IP estática, gateway endpoints, IPv6, CloudFront vs Global Accelerator.
- [ ] 15-20 preguntas topic-based por frente (practice mode, feedback inmediato).

> Hoy NO hay simulacro. Es día de **aprender**, no de medir.

### 🟦 Jueves 18 — Simulacro #3 (exam mode, AM) + repaso

- [ ] **AM — Simulacro #3** (90 min cronometrados, inglés, sin pausas). Aplicar regla "select N" y validar cada marca.
- [ ] **PM —** repaso completo pregunta por pregunta → doc-maestro. ¿Subieron Resilient y los frentes trabajados ayer?

### 🟦 Viernes 19 — Refuerzo dirigido: Identidad/Gobierno + Cost + gaps de #3

- [ ] **AM — Frente 3 (Identidad/Gobierno):** IAM Identity Center + AD Connector, Control Tower, Organizations + SCP.
- [ ] **PM — Frente 4 (Cost) + gaps de #3:** Cost Allocation Tags vs Budgets, DataSync→Glacier, transferencia offline, SSE headers, DynamoDB vs Aurora. Cerrar lo que haya fallado en el Simulacro #3.

### 🟦 Sábado 20 — Simulacro #4 (exam mode, AM) + cierre ligero — ÚLTIMO día de estudio

- [ ] **AM — Simulacro #4** (90 min, exam mode). Es tu **número de confianza** final.
- [ ] **PM — cierre ligero:** lectura tranquila de `tips/`, comparativas y `errors/review.md` front-to-back. ❌ Nada de contenido nuevo.
- [ ] **Logística:** confirmar hora del examen, +30 min ESL activo, documento de identidad, conexión/llegada con margen.
- [ ] Cerrar el estudio temprano. El domingo es descanso.

### 🟦 Domingo 21 — 🛌 Descanso total

- [ ] **Sin estudio.** Desconectar. Dormir bien. Llegar fresco vale más que un repaso extra.

### 🟦 Lunes 22 — 🎯 EXAMEN

- ✅ Buen desayuno, llegar fresco (tus mejores Dojo fueron AM y descansado).
- ✅ Regla "select N": validar cada marca antes de avanzar.
- ✅ Marcar dudas y seguir; ~2 min/pregunta.
- ✅ Frases gatillo: cost-effective, highly available, lowest latency, decouple, least privilege, synchronous→Multi-AZ.

---

## 🧭 Checkpoint de progreso (sábado 20, tras Simulacro #4)

Promedio de los simulacros **#3 y #4** (los que reflejan el estudio dirigido):

| Promedio #3+#4 | Lectura |
|---|---|
| ≥ 78% | Listo con holgura. Domingo a descansar sin culpa. |
| 72-77% | GO sólido. El examen real es más benévolo que TutorialsDojo. |
| 68-71% | GO ajustado. Repasa los frentes aún flojos en el cierre del sábado. |
| < 68% | Señal de que un frente no cerró. Foco total en él el sábado; el examen ya está el lunes. |

> El SAA-C03 se aprueba con **720/1000 (~72%)**. Los Dojo son más duros que el examen real: un 70% sostenido en Dojo suele traducirse en aprobado. La meta de estos días es subir el piso, sobre todo en Resilient.

## 🚨 Señales de alarma

- **Si #3 o #4 dan < 60%:** no entres en pánico; el repaso de la tarde pasa a ser obligatorio y 100% enfocado en el dominio más débil.
- **Si llegas agotado:** prioriza el simulacro de la mañana y dormir. El domingo de descanso es innegociable.
- **Tentación de estudiar el domingo:** no. El descanso la víspera es parte del plan, no un lujo.

## ✅ Checklist final (sábado 20 noche)

- [ ] 4 simulacros hechos y revisados; errores en doc-maestro + review.
- [ ] Los 4 frentes trabajados (Resilient/DR, Networking, Identidad/Gobierno, Cost).
- [ ] Promedio #3+#4 ≥ 72% (o foco claro para el cierre).
- [ ] Resilient por encima de 60% en el último simulacro.
- [ ] Logística del examen confirmada (+30 min ESL, identidad, hora).
- [ ] Recursos AWS apagados/eliminados.
- [ ] Estudio cerrado. Domingo libre.

---

*Actualizado el 16 de junio de 2026. Examen reagendado al **lunes 22 de junio** (AM). Recta final: 2 simulacros ya hechos (67% promedio), cierre de los 4 frentes débiles detectados en el Dojo #2, 2 simulacros más (jue + sáb), domingo de descanso, examen el lunes.*

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
