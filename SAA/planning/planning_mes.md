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

## ⏱️ Disponibilidad de tiempo

| Días | Horas/día |
|---|---|
| Lunes - Viernes | 4-5h |
| Sábado | 6-8h |
| Domingo | Descanso (0-1h opcional) |

**Total semanal:** 30-34h
**Total mes:** ~120-136h disponibles vs ~83h proyectadas → margen ajustado-cómodo

## 🎯 Estructura general

| Semana | Fechas | Foco | Hito |
|---|---|---|---|
| **1** | 5-10 may | Fundamentos + RDS + Route 53 | Bloques A, B, C completados |
| **2** | 12-17 may | S3 + CDN + Decoupling/Serverless + BD avanzadas | 70% del curso visto + primer Dojo SAA |
| **3** | 19-24 may | Monitoring + Security + VPC + DR | TODO el contenido visto + 3 Dojo SAA |
| **4** | 26-29 may | Solo simulacros y refinamiento | 3 Dojo SAA finales + examen |

## 📚 Distribución del temario (34 secciones)

| Bloque | Secciones | Horas | Prioridad |
|---|---|---|---|
| **A. Fundamentos** | 3, 4, 5, 6, 7, 8 | ~7h 38min | CRÍTICA |
| **B. Bases de datos básicas** | 9 | ~1h 31min | CRÍTICA |
| **C. Route 53 + arquitecturas** | 10, 11 | ~2h 31min | ALTA |
| **D. S3 completo** | 12, 13, 14, 15 | ~3h 8min | CRÍTICA |
| **E. CDN + Storage extras** | 16, 17 | ~1h 22min | ALTA |
| **F. Decoupling + Serverless** | 18, 19, 20, 21 | ~4h 21min | CRÍTICA |
| **G. BD avanzadas + Data + ML** | 22, 23, 24 | ~1h 41min | MEDIA |
| **H. Monitoring + Security** | 25, 26, 27 | ~4h 22min | ALTA |
| **I. Networking VPC** | 28 | ~3h 31min | **CRÍTICA — el más grande** |
| **J. DR + Migration** | 29 | ~54min | ALTA |
| **K. Cierre** | 30, 31, 32, 33, 34 | ~2h 5min | MEDIA |

## 🔑 Reglas no negociables

1. **NO hacer 2 simulacros completos en un mismo día.** El cansancio cuesta puntos.
2. **Día previo al examen:** cero simulacros. Solo notas. Cerrar a las 5-6 PM.
3. **Hands-on > videos repetidos.** Cuando dudes, abre la consola AWS.
4. **Domingos sagrados:** descanso real para sostener el mes.
5. **Time-boxing por sección:** si te excedes al doble del tiempo estimado, marca para revisión y avanza.

## 📝 Sistema de apuntes

**Regla 70/30:**
- 70% notas en formato comparativo (ver tipos abajo)
- 30% notas lineales solo cuando sea imprescindible

### Tipos de notas a construir

**Tipo 1 — Tablas de decisión por servicio:**
```
Almacenamiento de objetos → S3 (Standard / IA / One Zone-IA / Glacier / Deep Archive)
   ¿Cuál depende de?
   - Frecuencia acceso → Standard / IA / Glacier
   - Una sola AZ ok? → One Zone-IA
   - Tiempo recuperación → Instant / Flexible / Deep Archive
```

**Tipo 2 — Comparativas servicio-vs-servicio:**
```
RDS vs DynamoDB vs Aurora
- RDS → SQL tradicional, hasta ~64TB, escala vertical
- Aurora → Compatible MySQL/PostgreSQL, hasta 128TB, 5x rendimiento
- DynamoDB → NoSQL, serverless, single-digit ms latency
```

**Tipo 3 — Patrones arquitectónicos:**
```
Web app HA → ALB + ASG (multi-AZ) + RDS Multi-AZ + ElastiCache
Procesamiento batch → SQS + EC2 con ASG basado en queue depth
Migración archivos on-prem → DataSync (one-time) o Storage Gateway (continuo)
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
- ✅ Doc maestro: `SAA - Errores y comparativas.md`

### Complementarios (gratis)
- AWS Skill Builder (curso oficial gratuito)
- AWS Whitepapers: Well-Architected Framework
- AWS FAQs: S3, EC2, VPC, RDS, DynamoDB

### Apoyo con Claude
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
 4  5  6  7  8  9 10  ← Semana 1: Fundamentos
11 12 13 14 15 16 17  ← Semana 2: S3 + Serverless + Dojo #1
18 19 20 21 22 23 24  ← Semana 3: Security + VPC + DR
25 26 27 28 29        ← Semana 4: Solo simulacros + EXAMEN 29
```

## 🚀 Acción inmediata

**Sábado 3 - Domingo 4 mayo:** descanso real, cero AWS.

**Domingo 4 PM (1h máximo):**
- [ ] Comprar Tutorials Dojo SAA Practice Exams
- [ ] Crear doc maestro vacío
- [ ] Verificar acceso al curso de Stephane SAA
- [ ] Preparar plantillas de notas (3 tipos comparativos)

**Lunes 5 mayo, 9:00 AM:** arranque oficial 🎯

---

*Última actualización: 3 de mayo de 2026*