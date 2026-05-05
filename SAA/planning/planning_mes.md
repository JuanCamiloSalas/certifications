# Plan de Estudio - AWS Solutions Architect Associate (SAA-C03)

> Plan de preparación de 4 semanas para presentar el examen el **viernes 29 de mayo de 2026**
> Plan B: lunes 1 de junio de 2026

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

> ⚠️ **Importante:** revisar brevemente el índice de cada sección saltada para confirmar que no hay subtemas nuevos relevantes para SAA. Si aparece algo desconocido, ver solo ese subtema puntual.

## ⏱️ Disponibilidad de tiempo

| Días | Horas/día |
|---|---|
| Lunes - Viernes | 4-5h |
| Sábado | 6-8h |
| Domingo | Descanso (0-1h opcional) |

**Total semanal:** 30-34h
**Total mes:** ~120-136h disponibles vs ~77h proyectadas → margen cómodo

## 🎯 Estructura general

| Semana | Fechas | Foco | Hito |
|---|---|---|---|
| **1** | 5-10 may | EC2-SAA + Storage + ELB/ASG + RDS + Route 53 | Bloques A, B, C completados con holgura |
| **2** | 12-17 may | S3 avanzado + CDN + Decoupling/Serverless + BD avanzadas | 75% del curso visto + primer Dojo SAA |
| **3** | 19-24 may | Monitoring + Security + VPC + DR | TODO el contenido visto + 3 Dojo SAA |
| **4** | 26-29 may | Solo simulacros y refinamiento | 3 Dojo SAA finales + examen |

## 📚 Distribución del temario (secciones a estudiar)

| Bloque | Secciones | Horas | Prioridad |
|---|---|---|---|
| **A. Fundamentos avanzados** | ~~3, 4, 5~~, 6, 7, 8 | ~3h 56min | CRÍTICA |
| **B. Bases de datos básicas** | 9 | ~1h 31min | CRÍTICA |
| **C. Route 53 + arquitecturas** | 10, 11 | ~2h 31min | ALTA |
| **D. S3 avanzado** | ~~12~~, 13, 14, 15 | ~2h | CRÍTICA |
| **E. CDN + Storage extras** | 16, 17 | ~1h 22min | ALTA |
| **F. Decoupling + Serverless** | 18, 19, 20, 21 | ~4h 21min | CRÍTICA |
| **G. BD avanzadas + Data + ML** | 22, 23, 24 | ~1h 41min | MEDIA |
| **H. Monitoring + Security** | 25, 26, 27 | ~4h 22min | ALTA |
| **I. Networking VPC** | 28 | ~3h 31min | **CRÍTICA — el más grande** |
| **J. DR + Migration** | 29 | ~54min | ALTA |
| **K. Cierre** | 30, 31, 32, 33, 34 | ~2h 5min | MEDIA |

**Total a estudiar: ~28h de video** (vs 34h originales)

## 🔑 Reglas no negociables

1. **NO hacer 2 simulacros completos en un mismo día.** El cansancio cuesta puntos.
2. **Día previo al examen:** cero simulacros. Solo notas. Cerrar a las 5-6 PM.
3. **Hands-on > videos repetidos.** Cuando dudes, abre la consola AWS.
4. **Domingos sagrados:** descanso real para sostener el mes.
5. **Time-boxing por sección:** si te excedes al doble del tiempo estimado, marca para revisión y avanza.
6. **Regla de oro de apuntes:** si ya lo sabías del CCP y lo recuerdas, NO lo apuntes.

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
│   ├── SEMANA-1.md
│   ├── SEMANA-2.md
│   ├── SEMANA-3.md
│   └── SEMANA-4.md
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
| **Dojo Topic-based** (preguntas sueltas por tema) | Semanas 1-2 | Después de cada bloque grande |
| **Dojo Simulacro completo SAA** | Semana 2 final → Semana 4 | 6 simulacros en total |

### Distribución de los 6 Dojo SAA

| # | Fecha sugerida |
|---|---|
| 1 | Sábado 17 mayo |
| 2 | Viernes 23 mayo |
| 3 | Sábado 24 mayo |
| 4 | Lunes 26 mayo |
| 5 | Martes 27 mayo |
| 6 | Miércoles 28 mayo |

### Tabla de decisión GO/NO-GO

| Promedio últimos 3 Dojo | Decisión |
|---|---|
| ≥ 78% | GO el 29 con confianza |
| 72-77% | GO con repaso intensivo el 28 |
| 65-71% | Considera mover al 1 de junio |
| < 65% | Mueve mínimo 1 semana |

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

## 📅 Calendario macro

```
MAYO 2026
Lu Ma Mi Ju Vi Sá Do
            1  2  3   ← descanso post-CCP
 4  5  6  7  8  9 10  ← Semana 1: EC2-SAA + Storage + ELB + RDS + Route 53
11 12 13 14 15 16 17  ← Semana 2: S3 + Serverless + Dojo #1
18 19 20 21 22 23 24  ← Semana 3: Security + VPC + DR
25 26 27 28 29        ← Semana 4: Solo simulacros + EXAMEN 29
```

## 🚀 Acción inmediata

**Sábado 3 - Domingo 4 mayo:** descanso real, cero AWS.

**Domingo 4 PM (1h máximo):**
- [ ] Comprar Tutorials Dojo SAA Practice Exams
- [ ] Crear estructura de carpetas en repo
- [ ] Verificar acceso al curso de Stephane SAA
- [ ] Revisar índice de secciones 3, 4, 5 y 12 (confirmar que se pueden saltar)

**Lunes 5 mayo, 9:00 AM:** arranque oficial 🎯

---

*Última actualización: 3 de mayo de 2026*