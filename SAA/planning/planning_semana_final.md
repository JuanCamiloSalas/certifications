# Semana Final (12-16 junio) — Cierre de contenido + Simulacros + EXAMEN

> **Foco:** cerrar el 100% del temario (Sec 29 DR + 30-34) HOY y entrar en fase intensiva de simulacros.
> **Hito al cierre:** curso completo + 2 Dojo SAA completos revisados + decisión GO/NO-GO.
> **🎯 EXAMEN: martes 16 de junio (AM)** — Inglés + 30 min ESL.

## 📍 Punto de partida real (viernes 12 de junio)

- ✅ Completado: Sec 6-11, 13-28 — **incluido VPC (Sec 28), el bloque más pesado del SAA**.
- ❌ **Pendiente de temario:** Sec 29 (DR/Migraciones) + Sec 30-34 (cierre) ≈ 2-3h de video / ~3-4h reales.
- ❌ Aún sin Dojo SAA completo esta semana.

> **Lectura honesta:** el contenido se deslizó (debías cerrar el curso el jueves 11), PERO pasaron dos cosas a tu favor: (1) ya tienes VPC dominado, que es lo que de verdad pesa, y (2) el examen se movió al **martes 16**, lo que te da un día extra que absorbe casi exacto el atraso. El plan vuelve a estar holgado **si cierras el temario hoy sin excepción**.

## ⏱️ Disponibilidad restante

| Día | Horas | Misión |
|---|---|---|
| Vie 12 | 4-5h | Cerrar contenido (Sec 29 + 30-34) → **100% del curso** |
| Sáb 13 | 6-8h | Dojo SAA completo #1 + revisión |
| Dom 14 | 4-5h | Dojo SAA completo #2 + revisión enfocada |
| Lun 15 | Descanso + repaso ligero (día previo al examen) | |
| Mar 16 | **EXAMEN** 🎯 | |

**Necesario:** ~3-4h de contenido + 2 simulacros → **holgado si cierras el temario hoy**.

## 🎯 Objetivos de la semana

- ✅ Cerrar Sec 29 + 30-34 → **100% del curso** HOY viernes 12.
- ✅ Hacer **2 Dojo SAA completos** (sáb + dom) + topic-based de DR.
- ✅ Comparativas críticas de DR y migración de datos en `comparativas/`.
- ✅ Decisión **GO/NO-GO** el domingo por la noche.

---

## 📅 Plan día por día

### 🟦 Viernes 12 — Sec 29 (DR) + Sec 30-34 (cierre) → **100% del curso** (4-5h)

**Contenido (prioridad absoluta — no se recorta):**
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
- [ ] Lectura horizontal de TODAS las comparativas: detectar las 3 que aún confunden (apuntar para repaso de Lun).

**Si sobra tiempo (no obligatorio):**
- [ ] Dojo topic-based (15-20 preg — DR/Migración) → anotar errores en `errors/doc-maestro.md`.

> 🎯 **Hito innegociable:** al cerrar hoy, el temario está COMPLETO. Sábado y domingo son solo simulacros.

---

### 🟦 Sábado 13 — Dojo SAA completo #1 + repaso (6-8h)

**Mañana — Dojo SAA completo (90 min cronometrados):**
- [ ] Exam mode, en inglés, sin pausas. Aplicar regla "select N".
- [ ] Anotar solo números: DUDAS / ADIVINÉ / SERVICIO DESCONOCIDO.

**Tarde — Revisión (2.5-3h):**
- [ ] Ver puntaje, descansar 5 min, NO leer explicaciones al instante.
- [ ] Revisar TODOS los errores + las DUDAS aunque acertaras → `errors/doc-maestro.md`.
- [ ] Identificar el dominio más débil del desglose.
- [ ] 15-20 preguntas topic-based del dominio más flojo.

> Llega descansado: duerme bien el viernes. Tus mejores Dojo del CCP fueron AM y descansado.

---

### 🟦 Domingo 14 — Dojo SAA completo #2 + repaso intensivo (4-5h) + GO/NO-GO

**Mañana — Dojo SAA completo (90 min):** mismo protocolo.

**Tarde:**
- [ ] Revisión completa pregunta por pregunta → doc maestro.
- [ ] Repaso profundo de los 2 dominios más débiles de los 2 simulacros.
- [ ] Repasar las comparativas que sigas fallando (sobre todo VPC, Security y DR).

**🌙 Noche — Decisión GO/NO-GO** (ver tabla abajo).

> 🚫 **Regla de oro:** un solo simulacro completo por día. Sábado uno, domingo uno. El cansancio cuesta puntos.

---

### 🟦 Lunes 15 — Descanso + repaso ligero (día previo al examen)

- ❌ **CERO simulacros.** ❌ Nada de contenido nuevo.
- ✅ Lectura tranquila de `tips/tips-examen.md`, comparativas y doc maestro de errores.
- ✅ Repasar VPC, Security y DR una última vez si quedaron dudas (solo notas, no videos).
- ✅ **Cerrar el estudio a las 5-6 PM.** Cena ligera, dormir temprano.
- ✅ Logística: confirmar hora del examen, +30 min ESL activo, documento de identidad, llegar/conectar con margen.

---

### 🟦 Martes 16 — 🎯 EXAMEN

- ✅ Desayuno bueno, llegar fresco (tus mejores Dojo fueron AM y descansado).
- ✅ Regla "select N": contar marcas antes de avanzar.
- ✅ Marcar para revisión las dudas y seguir; gestionar el tiempo (~2 min/pregunta).
- ✅ Frases gatillo en mente: cost-effective, highly available, lowest latency, decouple, least privilege.

---

## 🧭 Decisión GO / NO-GO (domingo 14 por la noche)

Promedio de los **2 Dojo completos** del sáb + dom (más los previos si los tienes):

| Promedio | Decisión |
|---|---|
| ≥ 78% | **GO** el martes 16 con confianza. |
| 72-77% | **GO** con repaso enfocado el lunes (solo notas, sin agotarte). |
| 65-71% | GO ajustado: el examen perdona ~72%. Refuerza el dominio más flojo el lunes. Reagendar solo si te sientes muy inseguro. |
| < 65% | Considera mover la fecha. Hay gap real que un día no cierra. |

> El SAA-C03 se aprueba con **720/1000 (~72%)**. Los Dojo son más duros que el examen real: un 70% sostenido en Dojo suele traducirse en aprobado.

---

## 🚨 Señales de alarma

- **Si hoy viernes 12 no cierras el temario:** usa la mañana del sábado para terminarlo y mueve el primer simulacro completo a la tarde del sábado. NO sacrifiques tener el contenido al 100%.
- **Si un Dojo te da < 60%:** no entres en pánico, pero el lunes deja de ser descanso puro y se vuelve repaso del dominio más débil (excepción justificada).
- **Si llegas agotado al domingo:** prioriza el simulacro de la mañana y dormir bien. El descanso del lunes es innegociable.

## 📊 Métricas de control (cierre del domingo 14)

| Métrica | Meta |
|---|---|
| Curso completo | ✅ 100% (Sec 29-34 cerradas) |
| Comparativas nuevas (DR + Migración) | +2 tablas |
| Dojo SAA completos esta semana | 2 (sáb + dom) |
| Tips acumulados en `tips/` | 35+ |
| Recursos AWS apagados/eliminados | ✅ |
| Decisión GO/NO-GO tomada | ✅ |

## ✅ Checklist final (lunes 15 noche)

- [ ] Curso al 100% y comparativas críticas repasadas.
- [ ] 2 Dojo completos hechos y revisados; errores en doc maestro.
- [ ] Promedio Dojo ≥ 72% (o plan de contingencia claro).
- [ ] VPC, Security y DR dominados a nivel escenario.
- [ ] Logística del examen confirmada (+30 min ESL, identidad, hora).
- [ ] Estudio cerrado antes de las 6 PM. A dormir temprano.

---

*Actualizado el 12 de junio de 2026. Examen el martes 16 de junio. Recta final: cierre de contenido viernes, simulacros sáb-dom, descanso lunes, examen martes.*
