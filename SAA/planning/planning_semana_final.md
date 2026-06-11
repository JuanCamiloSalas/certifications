# Semana Final (8-15 junio) — Security + VPC + Cierre + Simulacros + EXAMEN

> **Foco:** cerrar el 100% del temario (Sec 27-34, con VPC como prioridad absoluta) y entrar en fase intensiva de simulacros.
> **Hito al cierre:** curso completo + 2 Dojo SAA finales revisados + decisión GO/NO-GO.
> **🎯 EXAMEN: lunes 15 de junio (AM)** — Inglés + 30 min ESL.

## 📍 Punto de partida real (lunes 8 de junio)

- ✅ Completado: Sec 6-11, 13-26 (incluye Monitoring y IAM avanzado).
- 🔄 **Hoy arranca:** Sec 27 — Seguridad y cifrado en AWS.
- 📅 Pendiente de temario: **Sec 27, 28 (VPC), 29 (DR), 30-34 (cierre)** ≈ 7h de video / ~10h reales.

> **Lectura honesta:** vas con el temario algo apretado para la fecha, pero el margen alcanza. La clave de esta semana: **terminar contenido lunes-jueves sin excepción** para liberar viernes y sábado a simulacros. VPC (Sec 28) es el bloque que más pesa en el SAA — no se recorta.

## ⏱️ Disponibilidad esta semana

| Día | Horas |
|---|---|
| Lun 8 - Vie 12 | 4-5h |
| Sáb 13 | 6-8h |
| Dom 14 | Descanso + repaso ligero (día previo al examen) |
| Lun 15 | **EXAMEN** 🎯 |

**Total disponible:** ~32-38h · **Necesario:** ~10h contenido + simulacros → holgado **si no se desliza el contenido**.

## 🎯 Objetivos de la semana

- ✅ Cerrar Sec 27, 28, 29, 30-34 → **100% del curso** a más tardar el **jueves 11**.
- ✅ Dominar VPC a nivel escenario (NACL vs SG, NAT, endpoints, peering, DX vs VPN).
- ✅ Hacer **2 Dojo SAA completos** (vie + sáb) + topic-based de los temas nuevos.
- ✅ Comparativas críticas de seguridad y networking en `comparativas/`.
- ✅ Decisión **GO/NO-GO** el sábado por la noche.

---

## 📅 Plan día por día

### 🟦 Lunes 8 — Sec 27: Seguridad y cifrado (4-5h)

**Contenido:**
- [ ] Sección 27 completa: KMS, envelope encryption, CloudHSM, SSM Parameter Store, Secrets Manager, ACM, WAF, Shield, GuardDuty, Inspector, Macie, Firewall Manager, encryption in-transit/at-rest.

**Hands-on (1-1.5h):**
- [ ] Crear una KMS key (symmetric) y cifrar/descifrar con CLI.
- [ ] Guardar un secreto en Secrets Manager y otro en SSM Parameter Store (SecureString).
- [ ] (Opcional) Solicitar un certificado en ACM.

**Apuntes — `cards/14-security-cifrado` + `comparativas/`:**
- Comparativa CRÍTICA: **KMS vs CloudHSM** (multi-tenant vs single-tenant, FIPS 140-2 L3).
- Comparativa CRÍTICA: **Secrets Manager vs SSM Parameter Store** (rotación automática, costo).
- Tabla servicios de detección: **GuardDuty vs Inspector vs Macie vs Detective** (¿qué detecta cada uno?).
- Tabla protección perímetro: **WAF vs Shield (Std/Advanced) vs Firewall Manager**.
- Tips para `tips/`:
  - "rotación automática de credenciales de BD" → Secrets Manager.
  - "almacenar config/parámetros gratis" → SSM Parameter Store.
  - "detectar PII en S3" → Macie.
  - "detección de amenazas con análisis de logs (VPC/DNS/CloudTrail)" → GuardDuty.
  - "vulnerabilidades en EC2/ECR/Lambda" → Inspector.
  - "DDoS L7 + reglas" → WAF; "DDoS gestionado avanzado" → Shield Advanced.
  - "single-tenant hardware, control total de keys" → CloudHSM.

**Dojo topic-based (15-20 preg — Security):** anotar errores en `errors/doc-maestro.md`.

---

### 🟦 Martes 9 — Sec 28: VPC PARTE 1 (4-5h) 🚨 *bloque más crítico*

**Contenido:**
- [ ] Sec 28 (mitad 1): CIDR/IP, subnets públicas vs privadas, IGW, route tables, NAT Gateway vs NAT Instance, **NACL vs Security Groups**, Bastion Host.

**Hands-on (1.5h):**
- [ ] Construir una VPC desde cero: 2 subnets (1 pública + 1 privada), IGW, route tables.
- [ ] Lanzar EC2 en la pública (con IP) y otra en la privada.
- [ ] Configurar NAT Gateway y verificar salida a internet de la privada.

**Apuntes — `cards/15-vpc` + `comparativas/`:**
- Comparativa CRÍTICA: **NACL (stateless, subnet) vs Security Group (stateful, ENI)**.
- Comparativa: **NAT Gateway vs NAT Instance** (gestionado, HA por AZ, ancho de banda).
- Patrón: **arquitectura pública/privada con bastion + NAT**.
- Tips para `tips/`:
  - "stateful / a nivel de instancia" → Security Group; "stateless / a nivel de subnet" → NACL.
  - "instancias privadas necesitan salida a internet sin recibir conexiones" → NAT Gateway.
  - "bloquear una IP específica" → NACL (SG no permite deny).

---

### 🟦 Miércoles 10 — Sec 28: VPC PARTE 2 + cierre VPC (4-5h)

**Contenido:**
- [ ] Sec 28 (mitad 2): **VPC Peering, VPC Endpoints (Gateway vs Interface/PrivateLink), Site-to-Site VPN, Direct Connect, Transit Gateway, VPC Flow Logs**.

**Hands-on (1h):**
- [ ] Crear un **Gateway Endpoint a S3** y acceder desde la EC2 privada sin pasar por NAT.
- [ ] Habilitar **VPC Flow Logs** hacia CloudWatch Logs o S3.

**Apuntes — `comparativas/`:**
- Comparativa CRÍTICA: **Gateway Endpoint (S3/DynamoDB) vs Interface Endpoint/PrivateLink** (resto de servicios, ENI, costo).
- Comparativa CRÍTICA: **Direct Connect vs Site-to-Site VPN** (latencia, costo, tiempo de provisión, cifrado).
- Tabla: **VPC Peering vs Transit Gateway** (no transitivo vs hub-and-traffic a escala).
- Tips para `tips/`:
  - "acceso privado a S3/DynamoDB sin internet" → Gateway Endpoint.
  - "acceso privado a otros servicios AWS / SaaS" → Interface Endpoint (PrivateLink).
  - "conexión dedicada, baja latencia, ancho de banda consistente" → Direct Connect.
  - "conectar cientos de VPCs y on-prem" → Transit Gateway.
  - "no transitivo, A↔B y B↔C no implica A↔C" → VPC Peering.

**Dojo topic-based (20 preg — Networking):** anotar errores. **Este es el set que más debes acertar.**

> ⚠️ Si VPC no quedó sólido hoy, recórtalo del repaso del domingo, no del jueves.

---

### 🟦 Jueves 11 — Sec 29 (DR) + Sec 30-34 (cierre) → **100% del curso** (4-5h)

**Contenido:**
- [ ] Sección 29: Disaster Recovery y Migraciones (Backup/Restore, Pilot Light, Warm Standby, Multi-Site; DMS, SMS, DataSync, Snowball, Storage Gateway).
- [ ] Secciones 30-34: cierre (white papers / Well-Architected / temas finales del curso).

**Apuntes — `cards/16-dr-migration` + `comparativas/`:**
- Tabla CRÍTICA: **estrategias DR** (RTO/RPO/costo ascendente): Backup&Restore → Pilot Light → Warm Standby → Multi-Site.
- Tabla: **migración de datos**: DataSync vs DMS vs Snowball/Snowmobile vs Storage Gateway.
- Tips para `tips/`:
  - "RPO/RTO bajísimos, costo no importa" → Multi-Site (active-active).
  - "el más barato, RTO de horas aceptable" → Backup & Restore.
  - "migrar BD con downtime mínimo" → DMS.
  - "transferir TB/PB sin red suficiente" → Snowball.
  - "transferencia continua on-prem ↔ AWS por red" → DataSync.

**Cierre de contenido (30 min):**
- [ ] ✅ Marcar curso al 100%.
- [ ] Lectura horizontal de TODAS las comparativas: detectar las 3 que aún confunden.

> 🎯 **Hito innegociable:** al cerrar el jueves, el temario está COMPLETO. Viernes y sábado son solo simulacros.

---

### 🟦 Viernes 12 — Dojo SAA completo #1 (de la recta final) + repaso (4-5h)

**Mañana — Dojo SAA completo (90 min cronometrados):**
- [ ] Exam mode, en inglés, sin pausas. Aplicar regla "select N".
- [ ] Anotar solo números: DUDAS / ADIVINÉ / SERVICIO DESCONOCIDO.

**Tarde — Revisión (2-2.5h):**
- [ ] Ver puntaje, descansar 5 min, NO leer explicaciones al instante.
- [ ] Revisar TODOS los errores + las DUDAS aunque acertaras → `errors/doc-maestro.md`.
- [ ] Identificar el dominio más débil del desglose.
- [ ] 15-20 preguntas topic-based del dominio más flojo.

---

### 🟦 Sábado 13 — Dojo SAA completo #2 + repaso intensivo (6-8h) + GO/NO-GO

**Mañana — Dojo SAA completo (90 min):** mismo protocolo. Llega descansado (duerme bien el viernes).

**Tarde:**
- [ ] Revisión completa pregunta por pregunta → doc maestro.
- [ ] Repaso profundo de los 2 dominios más débiles de los 2 simulacros.
- [ ] Repasar las comparativas que sigas fallando (sobre todo VPC y Security).

**🌙 Noche — Decisión GO/NO-GO** (ver tabla abajo).

> 🚫 **Regla de oro:** NO hacer 2 simulacros completos el mismo día. Viernes uno, sábado uno. El cansancio cuesta puntos.

---

### 🟦 Domingo 14 — Descanso + repaso ligero (día previo al examen)

- ❌ **CERO simulacros.** ❌ Nada de contenido nuevo.
- ✅ Lectura tranquila de `tips/tips-examen.md`, comparativas y doc maestro de errores.
- ✅ Repasar VPC y Security una última vez si quedaron dudas (solo notas, no videos).
- ✅ **Cerrar el estudio a las 5-6 PM.** Cena ligera, dormir temprano.
- ✅ Logística: confirmar hora del examen, +30 min ESL activo, documento de identidad, llegar/conectar con margen.

---

### 🟦 Lunes 15 — 🎯 EXAMEN

- ✅ Desayuno bueno, llegar fresco (tus mejores Dojo fueron AM y descansado).
- ✅ Regla "select N": contar marcas antes de avanzar.
- ✅ Marcar para revisión las dudas y seguir; gestionar el tiempo (~2 min/pregunta).
- ✅ Frases gatillo en mente: cost-effective, highly available, lowest latency, decouple, least privilege.

---

## 🧭 Decisión GO / NO-GO (sábado 13 por la noche)

Promedio de los **2 Dojo completos** del vie + sáb (más los previos si los tienes):

| Promedio | Decisión |
|---|---|
| ≥ 78% | **GO** el lunes 15 con confianza. |
| 72-77% | **GO** con repaso enfocado el domingo (solo notas, sin agotarte). |
| 65-71% | GO ajustado: el examen perdona ~72%. Refuerza el dominio más flojo el domingo. Reagendar solo si te sientes muy inseguro. |
| < 65% | Considera mover la fecha 1 semana. Hay gap real que un día no cierra. |

> El SAA-C03 se aprueba con **720/1000 (~72%)**. Los Dojo son más duros que el examen real: un 70% sostenido en Dojo suele traducirse en aprobado.

---

## 🚨 Señales de alarma

- **Si el martes 9 no terminaste VPC parte 1:** recorta hands-on del miércoles, no el contenido. VPC primero.
- **Si el jueves 11 no cerraste el temario:** usa el viernes en la mañana para terminarlo y mueve el primer simulacro completo al sábado (harías ambos sáb? no — entonces solo 1 simulacro completo el sábado + topic-based el viernes).
- **Si un Dojo te da < 60%:** no entres en pánico, pero el domingo deja de ser descanso puro y se vuelve repaso del dominio más débil (excepción justificada).
- **Si llegas agotado al sábado:** reduce la tarde, prioriza el simulacro de la mañana y dormir bien. El descanso del domingo es innegociable.

## 📊 Métricas de control (cierre del sábado 13)

| Métrica | Meta |
|---|---|
| Curso completo | ✅ 100% (Sec 27-34 cerradas) |
| Comparativas nuevas (Security + Networking + DR) | +6 tablas |
| Dojo SAA completos esta semana | 2 (vie + sáb) |
| Tips acumulados en `tips/` | 35+ |
| Recursos AWS apagados/eliminados | ✅ (KMS keys, NAT GW, endpoints, EC2) |
| Decisión GO/NO-GO tomada | ✅ |

## ✅ Checklist final (domingo 14 noche)

- [ ] Curso al 100% y comparativas críticas repasadas.
- [ ] 2 Dojo completos hechos y revisados; errores en doc maestro.
- [ ] Promedio Dojo ≥ 72% (o plan de contingencia claro).
- [ ] VPC y Security dominados a nivel escenario.
- [ ] Logística del examen confirmada (+30 min ESL, identidad, hora).
- [ ] Estudio cerrado antes de las 6 PM. A dormir temprano.

---

*Creado el 8 de junio de 2026. Examen el lunes 15 de junio. Esta es la recta final: contenido L-J, simulacros V-S, descanso D, examen L.*
