[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# Error Reviews — Dojo simulators

> Un archivo por simulacro (`dojo-review-N.md`) en formato *weak points*: scorecard por dominio + errores agrupados por prioridad + tabla resumen. Tras cada Dojo: registrar errores y actualizar el **progreso por dominio** y el **consolidado de cards** de abajo.

## Reviews por simulacro

| Dojo | Fecha | Score | Review |
|---|---|---|---|
| #1 | 2026-06-15 | 70% (46/65) | [dojo-review-1.md](./dojo-review-1.md) |
| #2 | 2026-06-16 | 64% (42/65) | [dojo-review-2.md](./dojo-review-2.md) |
| #3 | 2026-06-19 | 66% (43/65) | [dojo-review-3.md](./dojo-review-3.md) |

---

## Progreso por dominio

| Dominio | Peso | #1 | #2 | #3 | Lectura |
|---|---|---|---|---|---|
| Secure | 30% | 90% | 71% | 65% | 🔻 bajando 3 tests seguidos; pesa más que ninguno |
| Resilient | 26% | 53% | 47% | 56% | ↔ leve repunte pero crónico <60% |
| Cost-Optimized | 20% | 100% | 50% | 56% | 🔻 bajo; ya con bloque 17 de cards (recién creado) |
| High-Performing | 24% | 65% | 87% | 81% | 🔺 sólido — ya no es prioridad |

> **Total:** 70% → 64% → 66% (promedio ~67%, umbral 72%). Estancado en el borde.
> **Foco ahora:** **Networking/VPC** (Route 53, Direct Connect, VPC foundations, NACL — varios crónicos) y **Cost** (bloque 17 de cards recién creado — repásalo). Vigilar **Secure**: pesa 30% y lleva 3 tests bajando.
> _Scores aproximados: cada test varía el nº de preguntas por dominio. Úsalo como tendencia, no como medida exacta._

---

## Cards a repasar — consolidado (Dojo #1 + #2 + #3)

> Orden de prioridad: lo que **repites entre Dojos** o pesa más en el examen, primero. "Fallos" = veces que el tema cayó en los tres simulacros.

### 🔴 Crítico — crónico (≥2 Dojos) o ≥3 fallos

| Card | Tema | Dominio | Fallos |
|---|---|---|---|
| [RDS](../cards/04-rds-aurora/01-rds.md) | Multi-AZ vs Read Replica, failover (CNAME), IAM DB Auth, storage autoscaling, backup >35d→AWS Backup | Resilient / Secure | 6× |
| [VPC Foundations](../cards/15-vpc/01-vpc-foundations.md) | subnets/CIDR (/16–/28), IGW + route tables + public IP, secondary ENI | Resilient | 3× |
| [Identity Center](../cards/13-iam-advanced/05-identity-center.md) | IAM Identity Center + AD Connector | Secure | 3× |
| [DMS & SCT](../cards/16-dr-migration/02-dms-sct.md) | full load + CDC, homogeneous migration, migrar con mínimo downtime | Resilient | 3× |
| [Routing Policies 2](../cards/05-route53/03-routing-policies-2.md) | failover (active-active vs passive), weighted, geoproximity | Resilient | 2× |
| [Direct Connect](../cards/15-vpc/07-direct-connect.md) | DX Gateway + Transit Gateway, redundancia + VPN backup | Resilient | 2× |
| [Organizations & SCPs](../cards/13-iam-advanced/03-organizations-scps.md) | Organizations, SCP, Control Tower | Secure | 2× |
| [Aurora Advanced](../cards/04-rds-aurora/04-aurora-advanced.md) | Aurora Global DB, native Lambda invoke | Resilient | 2× |
| [Auto Scaling Group](../cards/03-elb-asg/05-asg.md) | HA capacity (N × AZs), termination policy | Resilient | 2× |
| [API Gateway](../cards/10-serverless/04-api-gateway.md) | canary deploy, features (vs AppSync) | High-Perf | 2× |
| [DynamoDB](../cards/11-bd-data-ml/01-dynamodb.md) | partition key cardinality, key-value vs Aurora | High-Perf | 2× |
| [DynamoDB Advanced](../cards/11-bd-data-ml/02-dynamodb-advanced.md) | Streams + Lambda, DAX + auto scaling | High-Perf | 2× |
| [CloudWatch](../cards/12-monitoring/01-cloudwatch.md) | custom metrics (agent), + SNS para alertas | High-Perf | 2× |

### 🟡 Importante — 1–2 fallos en dominio pesado/débil (Secure, Resilient, Cost)

| Card | Tema | Dominio | Fallos |
|---|---|---|---|
| [Roles & STS](../cards/13-iam-advanced/01-roles-sts.md) | IAM Groups para muchos usuarios; cross-account S3 (bucket policy + IAM) | Secure | 2× |
| [SG & NACL](../cards/15-vpc/02-sg-nacl.md) | NACL stateless + puertos efímeros vs SG stateful | Secure | 1× |
| [KMS](../cards/14-security/01-kms.md) | decrypt → key policy concede al execution role (no al ARN) | Secure | 1× |
| [CloudFront Security](../cards/07-cdn/02-cloudfront-security.md) | signed URLs/cookies + OAC | Secure | 1× |
| [Federation](../cards/13-iam-advanced/02-federation.md) | IAM Role + Policy en federación | Secure | 1× |
| [EKS](../cards/09-containers/03-eks.md) | envelope encryption de etcd (KMS) | Secure | 1× |
| [VPC Endpoints](../cards/15-vpc/04-vpc-endpoints.md) | gateway endpoint para DynamoDB/S3 | Secure | 1× |
| [S3 Encryption](../cards/06-s3-avanzado/02-s3-encryption.md) | header `x-amz-server-side-encryption` (SSE-S3/KMS vs SSE-C) | Secure | 1× |
| [Load Balancers](../cards/03-elb-asg/01-load-balancers.md) | ELB + Route 53 weighted para elasticidad | Resilient | 1× |
| [EBS Snapshots](../cards/02-storage-ec2/02-ebs-snapshots.md) | Data Lifecycle Manager (DLM) | Resilient | 1× |
| [Instance Store](../cards/02-storage-ec2/06-instance-store.md) | efímero; stop/start cambia host y pierde datos | Resilient | 1× |
| [Storage Gateway](../cards/16-dr-migration/05-storage-gateway.md) | File Gateway + lifecycle a Glacier | Resilient | 1× |
| [Instance Lifecycle](../cards/01-ec2-saa/02-instance-lifecycle.md) | EC2 billing por estado (RI/On-Demand/Spot) | Cost | 1× |
| [S3 Lifecycle](../cards/06-s3-avanzado/01-lifecycle-replication.md) | Glacier retrieval tiers (Expedited/Standard/Bulk + provisioned) | Cost | 1× |
| [DataSync & MGN](../cards/16-dr-migration/03-datasync-mgn.md) | DataSync directo a Glacier Deep Archive | Cost | 1× |
| [Snow Family](../cards/16-dr-migration/04-snow-family.md) | transferencia offline a escala TB/PB | Cost | 1× |
| [Pricing Models](../cards/17-billing-cost/01-pricing-models.md) | On-Demand/RI/Savings Plans/Spot/Dedicated, RI Marketplace | Cost | 1× |
| [Cost Management Tools](../cards/17-billing-cost/02-cost-management-tools.md) | Cost Allocation Tags, Cost Explorer API, Budgets, CUR | Cost | 2× |

### 🟢 Repaso ligero — 1 fallo en High-Performing (dominio ya fuerte)

| Card | Tema | Fallos |
|---|---|---|
| [Aurora](../cards/04-rds-aurora/03-aurora.md) | custom endpoints | 1× |
| [ALB](../cards/03-elb-asg/02-alb.md) | SNI multi-certificado | 1× |
| [NLB & GWLB](../cards/03-elb-asg/03-nlb-glb.md) | NLB static IP para whitelisting | 1× |
| [CloudFront](../cards/07-cdn/01-cloudfront.md) | 504 → cache hit ratio | 1× |
| [Global Accelerator](../cards/07-cdn/04-global-accelerator.md) | CloudFront + S3 vs Global Accelerator | 1× |
| [FSx](../cards/02-storage-ec2/07-fsx.md) | FSx Lustre (hot) + S3 (cold) | 1× |
| [Flow Logs & IPv6](../cards/15-vpc/08-flow-logs-ipv6.md) | subnet IPv6-only | 1× |
| [Records, Alias & TTL](../cards/05-route53/01-records-alias-ttl.md) | S3 static site + Route 53 (prereqs) | 1× |
| [Kinesis](../cards/08-decoupling/04-kinesis.md) | KDS + Lambda vs Firehose | 1× |
| [Hibernation](../cards/01-ec2-saa/04-hibernation.md) | arranque rápido sin costo extra | 1× |
| [S3 Access Points](../cards/06-s3-avanzado/04-s3-access-points.md) | S3 Object Lambda (por object key) | 1× |

### ⚠️ Sin card — candidatos a crear

| Tema | Dominio | Nota |
|---|---|---|
| CloudFormation (CreationPolicy / cfn-signal) | — | No hay bloque de IaC. |
| Lake Formation | High-Perf | Permisos de data lake multi-cuenta. |

> Cost ya tiene su bloque de cards ([17 — Billing & Cost Management](../cards/17-billing-cost/)). Pendientes solo CloudFormation y Lake Formation.

---

## Quiz dirigido con Gemini

> Cuando me pidas un quiz, te genero este prompt **relleno con tus temas débiles vigentes** (del consolidado de arriba). Variantes: *"solo Networking"*, *"mis rojos"*, *"lo de Cost"*. Lo pegas en Gemini y le añades tú el número de preguntas y cómo quieres que te las dé.

```
You are an AWS Certified Solutions Architect – Associate (SAA-C03) exam question writer.
Generate practice questions in real SAA-C03 style: realistic 3–5 line scenarios with
plausible distractors, in English. Mark any "select TWO" explicitly. Difficulty similar
to TutorialsDojo.

Focus on these weak areas:
- VPC / Networking: Route 53 routing policies (failover active-active vs active-passive,
  weighted, geoproximity); Direct Connect + Transit Gateway / DX Gateway; NACL (stateless,
  ephemeral ports) vs Security Groups; Internet Gateway + route tables + public IP needs;
  VPC CIDR ranges (/16–/28); VPC endpoints (gateway vs interface)
- Cost: EC2 billing per instance state; Reserved Instances billing & Marketplace;
  Cost Explorer API vs Budgets; S3 Glacier retrieval tiers (Expedited/Standard/Bulk,
  provisioned capacity)
- Resilient: RDS Multi-AZ vs Read Replica; Aurora Global; DMS full load + CDC; RDS backup
  retention (>35 days → AWS Backup); RDS storage autoscaling
- Gotchas: ALB SNI multi-cert; CloudFront OAC + signed URLs; S3 Object Lambda;
  instance store ephemerality on stop/start; CloudFormation CreationPolicy + cfn-signal
```

---

## Cómo registrar un nuevo Dojo

1. Sube los screenshots de las preguntas a `errors/dojo-N/`.
2. Crea `errors/dojo-review-N.md` copiando el formato de un review existente (scorecard → secciones por dominio → summary).
3. Actualiza la tabla **Reviews por simulacro**, el **Progreso por dominio** y el **consolidado de cards** (suma los `Fallos` de los temas que reaparezcan; sube a 🔴 lo que caiga en ≥2 Dojos).

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
