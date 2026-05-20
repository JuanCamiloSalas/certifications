# Semana 2 (18-23 mayo) - Decoupling/Serverless + BD avanzadas + Primer Dojo SAA

> **Foco:** Bloques F (Decoupling/Serverless) + G (BD avanzadas + Data + ML) + primer simulacro completo
> **Hito al cierre:** ~75% del curso visto + primer Dojo SAA completado
> **Examen reagendado:** viernes 5 de junio (Plan B: martes 9 de junio)

## 📍 Punto de partida real

**Avance confirmado al miércoles 20:**
- ✅ Sec 6-11 completas (semana 1)
- ✅ Sec 13: SDK/IAM (lunes 11 antes de enfermarte o martes 19)
- ✅ Sec 14: S3 avanzado
- ✅ Sec 15: S3 seguridad
- ✅ Sec 16: CloudFront y Global Accelerator
- ✅ Sec 17: Extras de almacenamiento de AWS

**Pendiente esta semana:** Sec 18-24 (Decoupling, Containers, Serverless, BD avanzadas, Data, ML)

## ⏭️ Recordatorio: secciones saltadas

- ~~Sec 12: Introducción a Amazon S3~~ (cubierta en CCP)

## 🎯 Objetivos de la semana

- ✅ Completar secciones 18, 19, 20, 21, 22, 23, 24
- ✅ Construir comparativas críticas (SQS vs SNS vs Kinesis, Lambda vs ECS vs Fargate)
- ✅ Hands-on con SQS, Lambda, DynamoDB
- ✅ **Primer Dojo SAA completo el sábado** (esperar 50-60%, es normal)
- ✅ Hacer al menos 80 preguntas Dojo topic-based durante la semana
- ✅ Recuperar el ritmo de la semana de enfermedad

## 📅 Plan día por día

### 🟦 Miércoles 20 de mayo - SQS/SNS/Kinesis (4-5h)

**Contenido:**
- [ ] Sección 18: Aplicaciones de desacoplamiento - SQS, SNS, Kinesis, ActiveMQ (1h 40min)

**Hands-on (1.5h):**
- [ ] Crear cola SQS Standard y enviar/recibir mensajes con CLI
- [ ] Crear cola FIFO y probar deduplicación + orden
- [ ] Configurar Dead Letter Queue
- [ ] Crear topic SNS y suscribir 2 endpoints (email + SQS - fan out)
- [ ] Crear stream Kinesis Data Stream
- [ ] (Opcional) crear Kinesis Data Firehose hacia S3

**Apuntes a construir en `notes/08-decoupling.md`:**
- Comparativa CRÍTICA: **SQS vs SNS vs Kinesis vs Amazon MQ**
  - Modelo (queue/pub-sub/stream), persistencia, orden, replay, casos de uso
- Tabla: **SQS Standard vs FIFO** (throughput, orden, dedupe, casos)
- Tabla: **Kinesis Data Streams vs Firehose vs Data Analytics vs Video Streams**
- Patrón: **Fan-out con SNS + SQS** (1 mensaje → múltiples colas)
- Patrón: **Decoupling con SQS** (productor + ASG consumiendo)
- Tips para `tips/tips-examen.md`:
  - "decouple components" → SQS
  - "fan-out / publish-subscribe" → SNS o SNS+SQS
  - "real-time analytics on streaming data" → Kinesis
  - "ordering matters / no duplicates" → SQS FIFO
  - "lift and shift de aplicación con JMS/AMQP" → Amazon MQ
  - "process data and deliver to S3" → Kinesis Firehose

**Preguntas Dojo topic-based (20 preguntas - Decoupling):**
- [ ] Hacer 20 preguntas
- [ ] Anotar errores en `errors/doc-maestro.md`

---

### 🟦 Jueves 21 de mayo - Containers + Serverless overview (4-5h)

**Contenido:**
- [ ] Sección 19: Contenedores en AWS - ECS, Fargate, ECR y EKS (1h 7min)
- [ ] Sección 20: Visión general sin servidor desde la perspectiva de un arquitecto (1h 17min)

**Hands-on (1.5h):**
- [ ] Crear cluster ECS con Fargate (tarea simple nginx)
- [ ] Crear ECR repository y pushear una imagen
- [ ] Lanzar tarea ECS desde tu imagen ECR
- [ ] Crear función Lambda con runtime Python
- [ ] Configurar trigger desde S3 (subir archivo → ejecuta Lambda)
- [ ] Configurar trigger desde EventBridge (cron schedule)
- [ ] Probar Lambda destinations (success/failure)

**Apuntes a construir en `notes/09-containers.md` y `notes/10-serverless.md`:**
- Comparativa CRÍTICA: **ECS vs EKS vs Fargate**
- Comparativa: **ECS launch types** (EC2 vs Fargate)
- Tabla: **ECR vs Docker Hub** (cuándo usar ECR)
- Comparativa CRÍTICA: **Lambda vs ECS Fargate vs EC2**
  - Cuándo cada uno según workload
- Tabla: **Lambda triggers** (síncronos vs asíncronos vs poll-based)
- Patrón: **Serverless API** (API Gateway + Lambda + DynamoDB)
- Patrón: **Procesamiento async** (S3 → Lambda → DynamoDB)
- Tips para `tips/tips-examen.md`:
  - "no servers to manage, scale to zero" → Lambda
  - "long-running container workloads" → ECS/EKS
  - "lift and shift Kubernetes" → EKS
  - "máximo 15 min de ejecución" → si es más → ECS Fargate (no Lambda)
  - "cold start matters" → Provisioned Concurrency en Lambda

**Preguntas Dojo topic-based (20 preguntas - Containers + Serverless):**
- [ ] Hacer 20 preguntas
- [ ] Anotar errores

---

### 🟦 Viernes 22 de mayo - Discusiones serverless + BD avanzadas + Data + ML (4-5h)

**Contenido:**
- [ ] Sección 21: Debates sobre la arquitectura de las soluciones sin servidor (17 min)
- [ ] Sección 22: Bases de datos en AWS (26 min)
- [ ] Sección 23: Datos y analítica (50 min)
- [ ] Sección 24: Machine Learning (35 min)

**Hands-on (1h):**
- [ ] Crear tabla DynamoDB con on-demand capacity
- [ ] Probar insertar/leer items con AWS CLI
- [ ] Habilitar DynamoDB Streams + Lambda trigger
- [ ] (Opcional) crear bucket Athena + tabla sobre S3 + correr query SQL

**Apuntes a construir en `notes/11-bd-data-ml.md`:**
- Tabla COMPLETA: **Servicios de BD AWS por tipo**
  - Relacional: RDS, Aurora
  - NoSQL: DynamoDB, DocumentDB, Keyspaces
  - In-memory: ElastiCache, MemoryDB
  - Graph: Neptune
  - Time-series: Timestream
  - Ledger: QLDB
  - Wide-column: Keyspaces
- Tabla CRÍTICA: **Servicios de Data & Analytics**
  - Athena: query SQL sobre S3 (serverless)
  - Redshift: data warehouse
  - EMR: big data con Hadoop/Spark
  - Glue: ETL serverless
  - QuickSight: BI/visualización
  - Kinesis: streaming
  - OpenSearch: búsqueda y análisis de logs
  - MSK: Kafka managed
- Tabla: **Servicios de ML básicos** (Rekognition, Transcribe, Polly, Translate, Comprehend, Lex, SageMaker, Forecast, Personalize, Textract)
- Patrón: **Análisis de logs** (Kinesis → S3 → Athena)
- Patrón: **Data Lake** (S3 + Glue + Athena + QuickSight)
- Tips para `tips/tips-examen.md`:
  - "query data in S3 with SQL" → Athena
  - "data warehouse petabyte scale" → Redshift
  - "ETL serverless" → Glue
  - "real-time dashboards" → QuickSight + Kinesis
  - "transcribe audio to text" → Amazon Transcribe
  - "extract text from images/PDFs" → Textract
  - "image recognition" → Rekognition

**Repaso pre-Dojo (1h):**
- [ ] Lectura horizontal de las notas de toda la semana
- [ ] Identificar los 2-3 temas más confusos
- [ ] Revisar tu `tips/tips-examen.md` acumulado
- [ ] Preparar mentalmente para el primer Dojo SAA mañana

---

### 🟦 Sábado 23 de mayo - PRIMER DOJO SAA + repaso (6-8h)

**🚨 Día clave de calibración del nivel real**

#### Mañana (3-4h)

**Antes del simulacro (45 min):**
- [ ] Revisión ligera de tu `tips/tips-examen.md` acumulado
- [ ] Revisión ligera de tu doc maestro de errores topic-based
- [ ] **NO estudiar contenido nuevo**

**🎯 Dojo SAA Simulacro #1 (90 min cronometrados):**
- [ ] Modo exam mode, en inglés, sin pausas
- [ ] Tomar nota solo de números: DUDAS / ADIVINÉ / SERVICIO DESCONOCIDO
- [ ] Aplicar regla "select N": contar marcas antes de avanzar

**Revisión del simulacro (1.5h):**
- [ ] Ver puntaje pero NO leer explicaciones inmediatamente. Tomar 5 min de descanso.
- [ ] Revisar pregunta por pregunta TODOS los errores
- [ ] Revisar también las preguntas que estaban en DUDAS aunque acertaras
- [ ] Para cada error, anotar en `errors/doc-maestro.md`:
  ```
  [Servicio principal] — [Concepto clave]
  Pregunta: (resumen 1 línea)
  Trampa: ¿qué te confundió?
  Regla: la lección en 1-2 líneas
  ```
- [ ] Identificar dominios débiles según el desglose Dojo

#### Tarde (3-4h)

**Repaso enfocado (2h):**
- [ ] Estudiar a profundidad los 2 dominios donde sacaste menor puntaje
- [ ] Volver a las comparativas que fallaste
- [ ] Hacer 15-20 preguntas topic-based del tema más débil

**Síntesis (30 min):**
- [ ] Escribir respuestas a estas 3 preguntas en `errors/doc-maestro.md`:
  1. ¿Cuál fue mi dominio más débil hoy?
  2. ¿Qué 3 servicios necesito repasar antes del próximo simulacro?
  3. ¿Detecté nuevas frases gatillo o patrones?

#### 📊 Expectativa del primer Dojo

| Resultado | Lectura |
|---|---|
| 70%+ | Excelente, mejor de lo esperado |
| 60-69% | Bueno, en línea con primer simulacro |
| **50-59%** | **NORMAL** - es el rango esperado |
| 40-49% | Bajo pero recuperable, identificar gaps grandes |
| < 40% | Revisar si hay gap mayor de contenido visto |

**⚠️ IMPORTANTE:** El primer Dojo SAA es **deliberadamente brutal**. NO te asustes con un 50%. Ya pasaste por esto en el CCP donde el diagnóstico te dio 53% y terminaste con 820.

---

### 🟦 Domingo 24 de mayo - Descanso

**Plan recomendado:**
- ❌ NO abrir AWS, Udemy, ni Dojo
- ✅ Actividad no técnica que disfrutes
- ✅ Dormir bien (te enfermaste hace poco, el descanso ahora es doble importante)

**Opcional (máximo 45 min):**
- Lectura ligera de las notas de comparativas
- Revisar `tips/tips-examen.md` acumulado
- NO hacer preguntas ni simulacros

---

## 📊 Métricas de control de la semana

Al cerrar el sábado, deberías tener:

| Métrica | Meta |
|---|---|
| Secciones completadas (acumuladas) | 6-11, 13-24 (18 secciones de 34) |
| Curso total avanzado | ~75% |
| Horas netas dedicadas esta semana | ~22-26h (Mié-Sáb, no L-M) |
| Notas comparativas en `notes/` | Mínimo 12 tablas acumuladas |
| Tips de examen acumulados | Mínimo 25 |
| Preguntas Dojo topic-based hechas | 60+ esta semana |
| Dojo SAA Simulacro #1 | ✅ Completado y revisado |
| Hands-on completados | 3+ |

## 🚨 Señales de alarma

**Si al jueves 21 no has terminado Containers + Serverless:**
- Mover parte del contenido al viernes
- Recortar hands-on del viernes a 30 min
- Es preferible llegar al sábado con TODO visto que con hands-on extras

**Si el Dojo SAA #1 te da menos de 40%:**
- No entrar en pánico, pero analizar si hay gap de contenido grande
- Considerar dedicar el domingo a repaso intensivo (excepción al descanso)
- NO mover la fecha del examen aún, los siguientes simulacros dirán más

**Si la enfermedad te dejó secuelas (fatiga, dolor de cabeza):**
- Reducir hands-on a la mitad
- Priorizar contenido del curso
- El descanso del domingo es **innegociable**

## 💡 Tips específicos para esta semana

1. **Decoupling es crítico:** SQS vs SNS vs Kinesis confunde mucho y aparece bastante en el examen. Hazte la pregunta "¿queue, pub-sub o stream?" para cada caso.

2. **Lambda tiene muchos detalles trampa:** límite de 15 min, cold starts, concurrency, destinations. Apunta todas las limitaciones.

3. **Antes del Dojo SAA del sábado:** duerme bien el viernes. Llega fresco al simulacro. Tus mejores Dojo del CCP fueron en la mañana descansado.

4. **Cleanup obligatorio:** después de cada hands-on, eliminar recursos pagos. Especialmente: ECS Fargate, Kinesis streams, DynamoDB con throughput provisionado, ECR images.

5. **Apuntes regla 70/30:** sigues sin transcribir. Solo comparativas y patrones.

6. **Post-enfermedad:** prioriza descanso sobre adelantar. Si te sientes cansado a las 4h, párate. Mejor 4h enfocadas que 6h dispersas.

## 🤖 Apoyo con Claude después de cada día

Al cerrar cada día, abrir Claude y pedirle:

```
Acabo de ver las secciones X del curso SAA. Aquí están mis apuntes:
[pegar el .md]

1. ¿Qué te falta importante para el SAA?
2. Genera 5 preguntas tipo examen sobre estos conceptos.
3. ¿Hay algún tip de examen que debería agregar a tips/?
```

Después del Dojo SAA #1, pedirle también:

```
Hice mi primer Dojo SAA y saqué X%. Mis dominios más débiles fueron:
- Dominio A: X%
- Dominio B: X%

Mis errores principales fueron:
[pegar los errores del doc maestro]

¿Qué patrones detectas? ¿Qué temas debería reforzar primero en la semana 3?
```

## 📝 Checklist de cierre semanal (sábado 23 noche)

- [ ] Secciones 18-24 completadas
- [ ] ~75% del curso total visto
- [ ] Doc maestro con mínimo 12 comparativas estructuradas
- [ ] `tips/tips-examen.md` con mínimo 25 tips
- [ ] Dojo SAA Simulacro #1 hecho y revisado
- [ ] Dominios débiles identificados para semana 3
- [ ] Recursos AWS apagados/eliminados (sin costos extras)
- [ ] Cost Explorer revisado
- [ ] Listas de vocabulario inglés actualizadas

---

## 🎯 Lo que viene en Semana 3 (25-30 mayo)

**Foco:** Monitoring + Security + **VPC (la sección más grande del curso, 3h 31min)** + DR

**El bloque más crítico del SAA:** VPC merece un sábado completo. Si fallas VPC, fallas el SAA. Si dominas VPC, tienes el examen prácticamente asegurado.

**2-3 Dojo SAA en la semana 3:** empiezas la fase intensiva de simulacros.

## 📅 Lo que viene en Semana 4 (1-5 junio)

**Solo simulacros y refinamiento:**
- Lun 1: Dojo SAA #4
- Mar 2: Dojo SAA #5
- Mié 3: Dojo SAA #6
- Jue 4: repaso ligero (cerrar a las 5 PM)
- **Vie 5: EXAMEN** 🎯

---

*Próxima semana: Monitoring + Security + VPC + DR + 2-3 simulacros Dojo SAA*