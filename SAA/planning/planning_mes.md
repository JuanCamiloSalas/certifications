# Plan de Estudio - AWS Solutions Architect Associate (SAA-C03)

> Plan de preparación para presentar el examen el **viernes 5 de junio de 2026**
> Plan B: martes 9 de junio de 2026
> *Plan reagendado una semana por enfermedad (12-16 mayo)*

## 📋 Contexto

- **Certificación previa:** AWS Certified Cloud Practitioner (CCP) aprobada con 820/1000
- **Experiencia AWS:** ~1 año de uso (despliegues sencillos + permisos)
- **Curso base:** Stephane Maarek SAA - Udemy (~34h de video)
- **Recursos complementarios:** Tutorials Dojo SAA Practice Exams
- **Idioma del examen:** Inglés (con +30 min ESL accommodation)
- **Meta profesional:** transición a DevOps / Cloud Engineer

## ⏭️ Secciones a saltar (ya cubiertas en CCP)

Estas secciones se omiten porque ya fueron estudiadas y dominadas en la preparación del CCP:

| Sección | Tema | Duración liberada |
|---|---|---|
| Sec 3 | Empezando con AWS | 20 min |
| Sec 4 | IAM y CLI de AWS | 1h 10min |
| Sec 5 | Fundamentos de EC2 | 2h 12min |
| Sec 12 | Introducción a Amazon S3 | 1h 8min |

**Total liberado: ~4h 50min de video** (~6h reales con apuntes)

## 📊 Estado actual del avance (al 20 de mayo)

✅ **Secciones completadas:** 6, 7, 8, 9, 10, 11, 13, 14, 15, 16, 17 (11 de 30 a estudiar)
🔄 **En curso:** Sec 18 (Decoupling) — se retoma el miércoles 20
📅 **Pendientes:** Sec 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34

## ⏱️ Disponibilidad de tiempo

| Días | Horas/día |
|---|---|
| Lunes - Viernes | 4-5h |
| Sábado | 6-8h |
| Domingo | Descanso (0-1h opcional) |

**Total semanal:** 30-34h
**Total proyectado en lo que queda:** ~55-65h disponibles vs ~50h necesarias → margen cómodo

## 🎯 Estructura general actualizada

| Semana | Fechas | Foco | Hito |
|---|---|---|---|
| ~~1~~ | ~~5-10 may~~ | ~~EC2-SAA + Storage + ELB/ASG + RDS + Route 53~~ | ✅ Completada |
| ~~Pausa~~ | ~~12-16 may~~ | ~~Enfermedad~~ | Recuperación |
| **2** | 18-23 may | Decoupling/Serverless + BD avanzadas + **Dojo SAA #1** | ~75% del curso |
| **3** | 25-30 may | Monitoring + Security + VPC + DR + 2-3 Dojo SAA | 100% del curso |
| **4** | 1-5 jun | Solo simulacros y refinamiento | 3 Dojo SAA finales + examen |

## 📚 Distribución del temario (secciones a estudiar)

| Bloque | Secciones | Estado | Horas | Prioridad |
|---|---|---|---|---|
| **A. Fundamentos avanzados** | 6, 7, 8 | ✅ | ~3h 56min | CRÍTICA |
| **B. Bases de datos básicas** | 9 | ✅ | ~1h 31min | CRÍTICA |
| **C. Route 53 + arquitecturas** | 10, 11 | ✅ | ~2h 31min | ALTA |
| **D. S3 avanzado** | 13, 14, 15 | ✅ | ~2h | CRÍTICA |
| **E. CDN + Storage extras** | 16, 17 | ✅ | ~1h 22min | ALTA |
| **F. Decoupling + Serverless** | 18, 19, 20, 21 | 🔄 Esta semana | ~4h 21min | CRÍTICA |
| **G. BD avanzadas + Data + ML** | 22, 23, 24 | 🔄 Esta semana | ~1h 41min | MEDIA |
| **H. Monitoring + Security** | 25, 26, 27 | 📅 Sem 3 | ~4h 22min | ALTA |
| **I. Networking VPC** | 28 | 📅 Sem 3 | ~3h 31min | **CRÍTICA — el más grande** |
| **J. DR + Migration** | 29 | 📅 Sem 3 | ~54min | ALTA |
| **K. Cierre** | 30, 31, 32, 33, 34 | 📅 Sem 3-4 | ~2h 5min | MEDIA |

**Total estudiado a la fecha:** ~11h 20min de video
**Total pendiente:** ~17h de video

## 🔑 Reglas no negociables

1. **NO hacer 2 simulacros completos en un mismo día.** El cansancio cuesta puntos.
2. **Día previo al examen:** cero simulacros. Solo notas. Cerrar a las 5-6 PM.
3. **Hands-on > videos repetidos.** Cuando dudes, abre la consola AWS.
4. **Domingos sagrados:** descanso real para sostener el mes.
5. **Time-boxing por sección:** si te excedes al doble del tiempo estimado, marca para revisión y avanza.
6. **Regla de oro de apuntes:** si ya lo sabías del CCP y lo recuerdas, NO lo apuntes.
7. **Post-enfermedad:** si el cuerpo dice basta, parar. Mejor sesiones cortas enfocadas que largas dispersas.

## 📝 Sistema de apuntes (3 capas)

### Capa 1 — Papel/Tablet: APRENDIZAJE EN VIVO
**Cuándo:** mientras ves el video.
**Qué:** diagramas, flujos, "ojo con esto", preguntas propias.
**No:** definiciones ni listas de features.

### Capa 2 — GitHub `notes/`: COMPARATIVAS Y NOVEDADES
**Cuándo:** al cerrar cada sección.
**Qué:** solo lo NUEVO del SAA (no repetir CCP).

**Tipos:**
1. **Tablas de decisión** (¿qué servicio según necesidad?)
2. **Comparativas servicio-vs-servicio** (RDS vs Aurora vs DynamoDB)
3. **Patrones arquitectónicos** (web HA, batch, etc.)

### Capa 3 — GitHub `tips/`: PISTAS DE EXAMEN
**Cuándo:** cuando detectes algo trampero o patrón.
**Formato:**
```markdown
> 💡 **TIP:** "Lowest latency to global users" → CloudFront
> ⚠️ **TRAMPA:** Security Groups son STATEFUL, NACL es STATELESS
> 🎯 **Frase gatillo:** "decouple" → SQS o SNS
```

## 📁 Estructura de carpetas del repo

```
saa-prep/
├── README.md                    ← Plan general (este archivo)
├── planning/
│   ├── SEMANA-1.md             ✅ Completada
│   ├── SEMANA-2.md             🔄 En curso (18-23 may)
│   ├── SEMANA-3.md             📅 Próxima (25-30 may)
│   └── SEMANA-4.md             📅 Final (1-5 jun)
├── notes/
│   ├── 01-ec2-saa.md           ← Sección 6
│   ├── 02-storage-ec2.md       ← Sección 7
│   ├── 03-elb-asg.md           ← Sección 8
│   ├── 04-rds-aurora.md        ← Sección 9
│   ├── 05-route53.md           ← Sección 10-11
│   ├── 06-s3-avanzado.md       ← Sección 13-15
│   ├── 07-cdn.md               ← Sección 16-17
│   ├── 08-decoupling.md        ← Sección 18
│   ├── 09-containers.md        ← Sección 19
│   ├── 10-serverless.md        ← Sección 20-21
│   ├── 11-bd-data-ml.md        ← Sección 22-24
│   ├── 12-monitoring.md        ← Sección 25
│   ├── 13-iam-avanzado.md      ← Sección 26
│   ├── 14-security-cifrado.md  ← Sección 27
│   ├── 15-vpc.md               ← Sección 28
│   └── 16-dr-migration.md      ← Sección 29
├── tips/
│   ├── tips-examen.md          ← TODOS los tips para repaso final
│   ├── frases-gatillo.md       ← Keywords y qué disparan
│   └── vocabulario-ingles.md   ← Términos en inglés
├── errors/
│   └── doc-maestro.md          ← Errores de simulacros
└── diagrams/
    └── (fotos de diagramas hechos a mano)
```

## 🧪 Estrategia de simulacros

| Tipo | Cuándo | Frecuencia |
|---|---|---|
| **Dojo Topic-based** (preguntas sueltas por tema) | Cada día | Después de cada bloque grande |
| **Dojo Simulacro completo SAA** | Semana 2 final → Semana 4 | 6 simulacros en total |

### Distribución de los 6 Dojo SAA (fechas actualizadas)

| # | Fecha | Notas |
|---|---|---|
| 1 | Sábado 23 mayo | Primer simulacro - calibración (esperar 50-60%) |
| 2 | Viernes 29 mayo | Semana 3 |
| 3 | Sábado 30 mayo | Semana 3 |
| 4 | Lunes 1 junio | Semana 4 |
| 5 | Martes 2 junio | Semana 4 |
| 6 | Miércoles 3 junio | Semana 4 - último antes del examen |

### Tabla de decisión GO/NO-GO

Evaluación final el **miércoles 3 de junio en la noche** después del Dojo #6:

| Promedio últimos 3 Dojo | Decisión |
|---|---|
| ≥ 78% | GO el 5 con confianza |
| 72-77% | GO con repaso intensivo el jueves 4 |
| 65-71% | Considera mover al martes 9 de junio (Plan B) |
| < 65% | Mueve mínimo 1 semana más |

## 🛠️ Recursos y herramientas

### Imprescindibles
- ✅ Curso de Stephane Maarek SAA (Udemy)
- ✅ Tutorials Dojo SAA Practice Exams (~$15 USD)
- ✅ Consola AWS para hands-on
- ✅ Doc maestro: `errors/doc-maestro.md`

### Complementarios (gratis)
- AWS Skill Builder (curso oficial gratuito)
- AWS Whitepapers: Well-Architected Framework
- AWS FAQs: S3, EC2, VPC, RDS, DynamoDB

### Apoyo con Claude
**Después de cada sección, pedir:**
1. ¿Qué falta importante en mis notas?
2. Genera 5 preguntas tipo examen sobre estos conceptos.
3. ¿Hay algún tip de examen que deba agregar a `tips/`?

**SÍ útil:**
- Explicaciones de conceptos confusos
- Generación de preguntas de práctica por tema
- Revisión de apuntes
- Resúmenes comparativos

**NO útil:**
- Reemplazar videos con texto
- Pedir apuntes hechos (perjudica aprendizaje)
- Simulacros generados (los Dojo están mejor calibrados)

## 📊 Lecciones aprendidas del CCP que aplicaré

✅ **Listas de vocabulario inglés** + frases gatillo (most cost-effective, highly available, etc.)
✅ **Regla "select N":** contar marcas antes de avanzar de pregunta
✅ **+30 min ESL** al agendar el examen
✅ **Doc maestro de errores** con formato: servicio → trampa → regla
✅ **Examen AM con buen desayuno** y descanso previo
✅ **No estudiar contenido nuevo** las últimas 12-18h antes del examen

## ⚠️ Diferencias críticas SAA vs CCP

| Aspecto | CCP | SAA |
|---|---|---|
| Tipo de preguntas | Conceptuales | Escenarios largos |
| Profundidad técnica | Superficial | Profunda + comparativas |
| Primer Dojo esperable | 70-80% | **50-60%** (normal, no asustarse) |
| Foco crítico | Servicios y modelo nube | **VPC/Networking + arquitecturas** |

## 📅 Calendario macro actualizado

```
MAYO 2026
Lu Ma Mi Ju Vi Sá Do
            1  2  3   ← descanso post-CCP
 4  5  6  7  8  9 10  ← ✅ Semana 1: EC2-SAA + Storage + ELB + RDS + Route 53
11 12 13 14 15 16 17  ← 🤒 Enfermedad (parcial: Sec 13-17 vistas)
18 19 20 21 22 23 24  ← 🔄 Semana 2: Decoupling + Serverless + Dojo #1
25 26 27 28 29 30 31  ← Semana 3: Security + VPC + DR + Dojo #2 y #3

JUNIO 2026
Lu Ma Mi Ju Vi Sá Do
 1  2  3  4  5        ← Semana 4: Dojo #4-6 + EXAMEN 5 jun 🎯
                      ← Plan B: 9 jun
```

## 🚀 Acción inmediata

**Hoy miércoles 20 de mayo:**
- [ ] Retomar con Sección 18 (Decoupling - SQS/SNS/Kinesis)
- [ ] Confirmar que las notas de Sec 13-17 están en orden
- [ ] Reagendar el examen en Pearson VUE para viernes 5 de junio
- [ ] Verificar que el +30 min ESL siga activo

**Antes del sábado 23 (Dojo SAA #1):**
- [ ] Tener completas las Sec 18-24
- [ ] Tener actualizado `tips/tips-examen.md` con mínimo 25 tips
- [ ] Doc maestro con comparativas críticas listas

---

*Última actualización: 20 de mayo de 2026 (post-enfermedad, examen reagendado al 5 de junio)*