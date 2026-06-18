[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# Error Reviews — Dojo simulators

> Un archivo por simulacro (`dojo-review-N.md`) en formato *weak points*: scorecard por dominio + errores agrupados por prioridad + tabla resumen. Tras cada Dojo: registrar errores y actualizar el **progreso por dominio** y el **consolidado de cards** de abajo.

## Reviews por simulacro

| Dojo | Fecha | Score | Review |
|---|---|---|---|
| #1 | 2026-06-15 | 70% (46/65) | [dojo-review-1.md](./dojo-review-1.md) |
| #2 | 2026-06-16 | 64% (42/65) | [dojo-review-2.md](./dojo-review-2.md) |

---

## Progreso por dominio

| Dominio | Peso | Dojo #1 | Dojo #2 | Tendencia |
|---|---|---|---|---|
| Secure | 30% | 90% | 71% | 🔻 −19 |
| Resilient | 26% | 53% | 47% | 🔻 −6 |
| High-Performing | 24% | 65% | 87% | 🔺 +22 |
| Cost-Optimized | 20% | 100% | 50% | 🔻 −50 |

> **Foco ahora:** Resilient (crónico <50%) y Cost (desplome + sin material); vigilar Secure (pesa 30% y bajó a 71%, justo bajo el umbral). High-Performing recuperado — ya no es prioridad.
> _Scores aproximados: cada test varía el nº de preguntas por dominio. Úsalo como tendencia, no como medida exacta._

---

## Cards a repasar — consolidado (Dojo #1 + #2)

> Orden de prioridad: lo que **repites** o pesa más en el examen, primero. Repasa de arriba hacia abajo y para cuando se acabe el tiempo. "Fallos" = veces que el tema cayó entre los dos simulacros.

### 🔴 Crítico — fallado en ambos / repetido

| Card | Tema | Dominio | Fallos |
|---|---|---|---|
| [RDS](../cards/04-rds-aurora/01-rds.md) | Multi-AZ vs Read Replica, failover (CNAME), IAM DB Auth | Resilient / Secure | 4× |
| [Identity Center](../cards/13-iam-advanced/05-identity-center.md) | IAM Identity Center + AD Connector | Secure | 3× |
| [Organizations & SCPs](../cards/13-iam-advanced/03-organizations-scps.md) | Organizations, SCP, Control Tower | Secure | 2× |
| [Aurora Advanced](../cards/04-rds-aurora/04-aurora-advanced.md) | Aurora Global DB, native Lambda invoke | Resilient | 2× |
| [Auto Scaling Group](../cards/03-elb-asg/05-asg.md) | HA capacity (N × AZs), termination policy | Resilient | 2× |
| [DMS & SCT](../cards/16-dr-migration/02-dms-sct.md) | DMS full load + CDC, homogeneous migration | Resilient | 2× |
| [API Gateway](../cards/10-serverless/04-api-gateway.md) | canary deploy, features (vs AppSync) | High-Perf | 2× |
| [DynamoDB](../cards/11-bd-data-ml/01-dynamodb.md) | partition key cardinality, key-value vs Aurora | High-Perf | 2× |
| [CloudWatch](../cards/12-monitoring/01-cloudwatch.md) | custom metrics (agent), + SNS para alertas | High-Perf | 2× |

### 🟡 Importante — 1 fallo en dominio pesado/débil (Resilient, Secure, Cost)

| Card | Tema | Dominio | Fallos |
|---|---|---|---|
| [Load Balancers](../cards/03-elb-asg/01-load-balancers.md) | ELB + Route 53 weighted para elasticidad | Resilient | 1× |
| [EBS Snapshots](../cards/02-storage-ec2/02-ebs-snapshots.md) | Data Lifecycle Manager (DLM) | Resilient | 1× |
| [Direct Connect](../cards/15-vpc/07-direct-connect.md) | redundancia DX + VPN de respaldo | Resilient | 1× |
| [VPC Foundations](../cards/15-vpc/01-vpc-foundations.md) | secondary ENI para failover de IP privada | Resilient | 1× |
| [Storage Gateway](../cards/16-dr-migration/05-storage-gateway.md) | File Gateway + lifecycle a Glacier | Resilient | 1× |
| [Routing Policies 2](../cards/05-route53/03-routing-policies-2.md) | Geoproximity vs Geolocation | Resilient | 1× |
| [Federation](../cards/13-iam-advanced/02-federation.md) | IAM Role + Policy en federación | Secure | 1× |
| [EKS](../cards/09-containers/03-eks.md) | envelope encryption de etcd (KMS) | Secure | 1× |
| [VPC Endpoints](../cards/15-vpc/04-vpc-endpoints.md) | gateway endpoint para DynamoDB/S3 | Secure | 1× |
| [S3 Encryption](../cards/06-s3-avanzado/02-s3-encryption.md) | header `x-amz-server-side-encryption` (SSE-S3/KMS vs SSE-C) | Secure | 1× |
| [DataSync & MGN](../cards/16-dr-migration/03-datasync-mgn.md) | DataSync directo a Glacier Deep Archive | Cost | 1× |
| [Snow Family](../cards/16-dr-migration/04-snow-family.md) | transferencia offline a escala TB/PB | Cost | 1× |

### 🟢 Repaso ligero — 1 fallo en High-Performing (dominio ya fuerte)

| Card | Tema | Dominio | Fallos |
|---|---|---|---|
| [Aurora](../cards/04-rds-aurora/03-aurora.md) | custom endpoints | High-Perf | 1× |
| [NLB & GWLB](../cards/03-elb-asg/03-nlb-glb.md) | NLB static IP para whitelisting | High-Perf | 1× |
| [DynamoDB Advanced](../cards/11-bd-data-ml/02-dynamodb-advanced.md) | Streams + Lambda | High-Perf | 1× |
| [CloudFront](../cards/07-cdn/01-cloudfront.md) | 504 → cache hit ratio | High-Perf | 1× |
| [Global Accelerator](../cards/07-cdn/04-global-accelerator.md) | CloudFront + S3 vs Global Accelerator | High-Perf | 1× |
| [FSx](../cards/02-storage-ec2/07-fsx.md) | FSx Lustre (hot) + S3 (cold) | High-Perf | 1× |
| [Flow Logs & IPv6](../cards/15-vpc/08-flow-logs-ipv6.md) | subnet IPv6-only | High-Perf | 1× |
| [Records, Alias & TTL](../cards/05-route53/01-records-alias-ttl.md) | S3 static site + Route 53 (prereqs) | High-Perf | 1× |
| [Kinesis](../cards/08-decoupling/04-kinesis.md) | KDS + Lambda vs Firehose | High-Perf | 1× |

### ⚠️ Sin card — candidatos a crear

| Tema | Dominio | Nota |
|---|---|---|
| Cost Allocation Tags | Cost | No hay bloque de billing/cost en `cards/` — es el mayor gap de contenido (Cost cayó a 50% en el Dojo #2). |
| Lake Formation | High-Perf | Permisos de data lake multi-cuenta; sin card. |

---

## Quiz dirigido con Gemini

> Cuando me pidas un quiz, te genero este prompt **relleno con tus temas débiles vigentes** (del consolidado de arriba). Puedes pedir una variante: *"solo Resilient"*, *"mis rojos"*, *"lo de Cost"*. Lo pegas en Gemini y le añades tú el número de preguntas y cómo quieres que te las dé.

```
You are an AWS Certified Solutions Architect – Associate (SAA-C03) exam question writer.
Generate practice questions in real SAA-C03 style: realistic 3–5 line scenarios with
plausible distractors, in English. Mark any "select TWO" explicitly. Difficulty similar
to TutorialsDojo.

Focus on these weak areas:
- RDS: Multi-AZ vs Read Replica, failover behavior (CNAME), IAM DB Authentication
- IAM Identity Center + AD Connector; Organizations / Control Tower
- Aurora Global Database; Aurora native Lambda invoke
- Auto Scaling Group (HA capacity, termination policy); DMS full load + CDC
- API Gateway (canary, vs AppSync); DynamoDB (partition key, vs Aurora); CloudWatch + SNS
- Cost: Cost Allocation Tags; archival transfer (DataSync→Glacier, Snow/offline)
```

---

## Cómo registrar un nuevo Dojo

1. Sube los screenshots de las preguntas a `errors/dojo-N/`.
2. Crea `errors/dojo-review-N.md` copiando el formato de un review existente (scorecard → secciones por dominio → summary).
3. Actualiza la tabla **Reviews por simulacro**, el **Progreso por dominio** y el **consolidado de cards** (suma los `Fallos` de los temas que reaparezcan).

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
