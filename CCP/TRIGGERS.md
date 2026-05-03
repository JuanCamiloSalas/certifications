# Trigger Words & Phrases — CCP Exam

Listado de **palabras y frases en inglés** que aparecen en las preguntas del **AWS Certified Cloud Practitioner (CLF-C02)** y la respuesta a la que apuntan. El examen es esencialmente un mapeo *keyword → servicio*, así que reconocer estos disparadores es la diferencia entre acertar rápido o quedarse pensando.

[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](./README.md)

> [!TIP]
> Léelo en voz alta varias veces antes de cada simulacro. Cuando veas el trigger en el examen, la respuesta debe llegarte automática.

---

## 📑 Índice

1. [Compute (EC2, Lambda, contenedores, Batch)](#1-compute)
2. [EC2 Purchase Options](#2-ec2-purchase-options)
3. [Storage (S3, EBS, EFS, FSx, Glacier)](#3-storage)
4. [Snow Family & Data Transfer](#4-snow-family--data-transfer)
5. [Databases & Analytics](#5-databases--analytics)
6. [Networking & VPC](#6-networking--vpc)
7. [Load Balancing & Scaling](#7-load-balancing--scaling)
8. [Content Delivery & Edge](#8-content-delivery--edge)
9. [Security, Identity & Compliance](#9-security-identity--compliance)
10. [Monitoring & Management](#10-monitoring--management)
11. [Deployment & Infrastructure](#11-deployment--infrastructure)
12. [Integration & Messaging](#12-integration--messaging)
13. [Migration](#13-migration)
14. [Machine Learning](#14-machine-learning)
15. [IoT, Edge, Satellite](#15-iot-edge-satellite)
16. [Cost Management & Billing](#16-cost-management--billing)
17. [Support & Professional Services](#17-support--professional-services)
18. [AWS Cloud Concepts](#18-aws-cloud-concepts)
19. [Well-Architected Framework (6 Pillars)](#19-well-architected-framework-6-pillars)
20. [AWS CAF (Cloud Adoption Framework)](#20-aws-caf-cloud-adoption-framework)
21. [Shared Responsibility Model](#21-shared-responsibility-model)
22. [Common Traps & Distractors](#22-common-traps--distractors)
23. [Question-Pattern Phrases (jerga vista en simulacros)](#23-question-pattern-phrases-jerga-vista-en-simulacros)

---

## 1. Compute

| Trigger phrase | Service |
|---|---|
| "Run **Docker containers**", "container orchestration on AWS" (you manage EC2) | **ECS** |
| "**Serverless containers**", "no infrastructure to manage" + containers | **Fargate** |
| "**Private Docker registry**" | **ECR** |
| "**Kubernetes**", "**cloud-agnostic** orchestration" | **EKS** |
| "**Functions as a Service (FaaS)**", "**event-driven** execution", "**pay per invocation + duration**", "**15-minute max** runtime" | **AWS Lambda** |
| "**Batch jobs**", "**batch processing at scale**", "Docker images on ECS", "no time limit" | **AWS Batch** |
| "**Beginners**", "**predictable pricing**", "**simplest** EC2/RDS alternative", "WordPress / LAMP / MEAN templates" | **Amazon Lightsail** |
| "**REST or WebSocket APIs**", "serverless API management" | **API Gateway** |

---

## 2. EC2 Purchase Options

| Trigger phrase | Option |
|---|---|
| "**Bring Your Own License (BYOL)**", "**per-socket / per-core licensing**", "compliance requires dedicated physical server" | **Dedicated Host** |
| "**Dedicated hardware** but no host visibility" | **Dedicated Instance** |
| "Workload **less than a year**", "**short-term**", "**uninterruptible** + **3 months**" | **On-Demand** |
| "**Interruptible**", "**fault-tolerant**", "**up to 90% discount**", "batch / data analysis" | **Spot Instances** |
| "**1 or 3 year commitment**", "**predictable / constant** workload" (e.g. database) | **Reserved Instance** |
| "**Change family / OS / tenancy**" mid-term | **Convertible RI** |
| "**Commit to $/hour**", "flexible across regions / instance families" | **Savings Plan** |
| "**Capacity guaranteed** in a specific AZ, **no discount**" | **Capacity Reservations** |

---

## 3. Storage

| Trigger phrase | Service / Class |
|---|---|
| "**Block storage** attached to EC2", "network drive", "**tied to one AZ**" | **EBS** |
| "**Highest IOPS / hardware disk**" + "**ephemeral**" / lost on stop | **EC2 Instance Store** |
| "**NFS**", "**Linux** shared file system", "**multi-AZ**", "100s of EC2 simultaneously" | **EFS** |
| "**Windows file share**", "**SMB**", "**Active Directory**", "NTFS" | **FSx for Windows File Server** |
| "**HPC**", "**Linux + cluster**", "**high-performance computing**", "ML / financial modeling" | **FSx for Lustre** |
| "**Object storage**", "**buckets**", "static website hosting", "**11 9's** durability" | **Amazon S3** |
| "**Frequent access**, low latency" | **S3 Standard** |
| "**Infrequent access**, immediate retrieval, lower cost" | **S3 Standard-IA** |
| "**Single AZ**, recreatable / non-critical data" | **S3 One Zone-IA** |
| "**Unknown / changing access patterns**", auto-tier | **S3 Intelligent-Tiering** |
| "Archive, **milliseconds retrieval**, ~once a quarter" | **S3 Glacier Instant Retrieval** |
| "Archive, **minutes-to-hours retrieval**" | **S3 Glacier Flexible Retrieval** |
| "**Long-term archive**", **12-48h retrieval**, **cheapest** | **S3 Glacier Deep Archive** |
| "**Prevent accidental / unauthorized S3 object deletion**" | **MFA Delete** (with versioning) |
| "**Hybrid storage** between on-prem and S3" | **AWS Storage Gateway** |

---

## 4. Snow Family & Data Transfer

| Trigger phrase | Service |
|---|---|
| "**Speed up uploads/downloads to S3** globally" (network-based) | **S3 Transfer Acceleration** |
| "**Speed up content delivery to users**", CDN | **CloudFront** (NOT S3 Transfer Acceleration) |
| "**Offline data transfer**", "transfer would take **>1 week** over network" | **AWS Snow Family** |
| "Edge computing", "**small/portable**", "harsh environments" | **AWS Snowcone** |
| "**Up to 80 TB**", physical appliance with storage **and compute** | **AWS Snowball Edge** |
| "**Exabytes** of data", "**truck**", "100 PB per device" | **AWS Snowmobile** |
| "**Online sync** (hourly/daily/weekly)", "**incremental** transfers" | **AWS DataSync** |

---

## 5. Databases & Analytics

| Trigger phrase | Service |
|---|---|
| "**Managed relational SQL database**", "MySQL / PostgreSQL / **Oracle / SQL Server / MariaDB**", "OLTP" | **Amazon RDS** |
| "**5x MySQL / 3x PostgreSQL** performance", "AWS-proprietary database" | **Amazon Aurora** |
| "**Intermittent / unpredictable / infrequent** workloads", "no capacity planning", "pay per second" | **Aurora Serverless** |
| "**NoSQL key-value**", "**serverless**", "**single-digit ms** latency", "auto-scaling" | **DynamoDB** |
| "**Microsecond cache** for DynamoDB" | **DAX** |
| "**In-memory cache**", "**Redis or Memcached**" | **ElastiCache** |
| "**Data warehouse**", "**OLAP**", "**petabyte-scale** SQL analytics", "**columnar storage**" | **Amazon Redshift** |
| "**Hadoop cluster**", "**Big Data**", "Spark / HBase / Presto / Flink" | **Amazon EMR** |
| "**Query S3 with SQL** serverless", "CSV/JSON/Parquet" | **Amazon Athena** |
| "**BI dashboards**", "**visualizations**", "serverless BI" | **Amazon QuickSight** |
| "**MongoDB-compatible**", "JSON document database" | **DocumentDB** |
| "**Graph database**", "social network / fraud detection / recommendation engine" | **Amazon Neptune** |
| "**Time-series database**", "IoT data / sensor data / events over time" | **Amazon Timestream** |
| "**Blockchain**", "**Hyperledger Fabric / Ethereum**", "no central authority" | **Managed Blockchain** |
| "**ETL serverless**", "data catalog feeding Athena/Redshift/EMR" | **AWS Glue** |
| "**Migrate database to AWS**" (homogeneous or heterogeneous) | **AWS DMS** |

---

## 6. Networking & VPC

| Trigger phrase | Service / Concept |
|---|---|
| "**Private network**" inside AWS | **VPC** |
| "**Connect two VPCs** privately, **non-transitive**" | **VPC Peering** |
| "**Connect thousands of VPCs**", "**hub-and-spoke**", "**transitive peering**" | **Transit Gateway** |
| "Access **AWS services privately** without internet" | **VPC Endpoints** |
| "**S3 or DynamoDB** privately" | **VPC Endpoint Gateway** |
| "**Any other AWS service** privately" (interface + ENI) | **VPC Endpoint Interface** |
| "Expose your service to many VPCs privately" | **AWS PrivateLink** |
| "**Site-to-site VPN**", on-prem ↔ AWS over Internet | **CGW** (on-prem) + **VGW** (AWS side) |
| "Connect **from your computer with OpenVPN**" | **AWS Client VPN** |
| "**Dedicated physical connection**", "**weeks/months** to set up", high bandwidth | **AWS Direct Connect** |
| "**Capture network traffic** for analysis / troubleshooting" | **VPC Flow Logs** |
| "**Stateful firewall** at **instance/ENI** level", **ALLOW-only** rules | **Security Group** |
| "**Stateless firewall** at **subnet** level", **ALLOW + DENY** rules | **NACL** |
| "**Protect entire VPC**, layers 3-7", VPC↔VPC, DX, VPN | **AWS Network Firewall** |
| "**Outbound IPv6 only**" | **Egress-Only Internet Gateway** |

---

## 7. Load Balancing & Scaling

| Trigger phrase | Service |
|---|---|
| "**Path-based / host-based routing**", "**WebSockets**", "**HTTP/HTTPS**", "Layer 7" | **ALB** (Application Load Balancer) |
| "**TCP / UDP / TLS**", "**millions of requests/sec**", "**ultra-low latency**", "**static IP**", "Layer 4" | **NLB** (Network Load Balancer) |
| "**Network appliances** (firewalls, IDS/IPS)", "Layer 3" | **Gateway Load Balancer** |
| "**Replace unhealthy instances**" | **Auto Scaling Group** (Reliability angle) |
| "**Match capacity to demand**", "scale in/out automatically" | **Auto Scaling Group** (Performance angle) |

---

## 8. Content Delivery & Edge

| Trigger phrase | Service |
|---|---|
| "**DNS service**", routing policies (Simple/Weighted/Latency/Failover) | **Route 53** |
| "**CDN**", "cache content globally (images, videos, HTML)", "**Edge Locations** cache" | **CloudFront** |
| "Lambda **at the edge**" | **Lambda@Edge** |
| "**Static IPs**", "**TCP/UDP**", "**no caching**", "fast regional failover" | **Global Accelerator** |
| "**5G**", "ultra-low latency on mobile networks", "vehicle / AR/VR" | **AWS Wavelength** |
| "**Run AWS in your own data center**", "hybrid", "low local latency" | **AWS Outposts** |

---

## 9. Security, Identity & Compliance

| Trigger phrase | Service |
|---|---|
| "**Manage users, roles, policies, MFA**" | **IAM** |
| "**Find resources shared externally** (buckets, KMS, roles)" | **IAM Access Analyzer** |
| "**Single Sign-On**", "central identity for AWS accounts and apps" | **IAM Identity Center** (formerly SSO) |
| "**Federated users**", "**temporary credentials**" | **AWS STS** |
| "**Mobile/web app user authentication**", sign-up/sign-in | **Amazon Cognito** |
| "**Active Directory**" managed | **AWS Directory Service** |
| "**Encryption keys**", "**KMS keys**", encryption at rest | **AWS KMS** |
| "**Hardware security module**", "**FIPS 140-2 Level 3**", "dedicated hardware" | **CloudHSM** |
| "**SSL/TLS certificates**", "HTTPS for ELB/CloudFront/API GW" | **ACM** (Certificate Manager) |
| "**Store secrets**", "**rotate automatically**", "integrate with RDS" | **AWS Secrets Manager** |
| "**Store parameters / configuration cheaply**" | **SSM Parameter Store** |
| "**DDoS protection**, automatic, free" | **AWS Shield Standard** |
| "**DDoS premium 24/7**", "$3000/month", DRT team, surge credits | **AWS Shield Advanced** |
| "**Layer 7 protection**", "**SQL injection / XSS**", "**geo-blocking / rate limiting**", on CloudFront/ALB/API GW | **AWS WAF** |
| "**Threat detection** with **ML on CloudTrail/VPC Flow/DNS logs**", "cryptomining" | **Amazon GuardDuty** |
| "**Vulnerability scanning** on **EC2 / ECR / Lambda**" (CVEs) | **Amazon Inspector** |
| "**Discover sensitive data / PII** in **S3** with ML" | **Amazon Macie** |
| "**Configuration history / compliance** of resources" | **AWS Config** |
| "**Central security dashboard** aggregating findings (GuardDuty/Inspector/Macie/Config)" | **Security Hub** |
| "**Investigate root cause** of security findings using **graphs**" | **Amazon Detective** |
| "**Manage firewall rules** centrally across **AWS Organizations**" | **AWS Firewall Manager** |
| "**Compliance reports**: ISO, PCI, SOC, HIPAA, BAA, GDPR, FedRAMP" | **AWS Artifact** |
| "**Chaos engineering / fault injection**" on EC2/ECS/EKS/RDS | **AWS FIS** |

---

## 10. Monitoring & Management

| Trigger phrase | Service |
|---|---|
| "**What is happening?**", metrics, logs, alarms, dashboards | **Amazon CloudWatch** |
| "**Who did what?**", "API call history", audit | **AWS CloudTrail** |
| "**Detect unusual API activity** automatically" | **CloudTrail Insights** |
| "**Is my resource configured correctly?**", config history | **AWS Config** |
| "**Trace requests across microservices**", service map, latency | **AWS X-Ray** |
| "**Cron / scheduled triggers**", "**react to AWS / SaaS events**" | **Amazon EventBridge** |
| "**ML-powered code review** (development)" | **CodeGuru Reviewer** |
| "**Application profiling at runtime** (production)" | **CodeGuru Profiler** |
| "**AWS service health / outage notifications**" | **AWS Health Dashboard** |

---

## 11. Deployment & Infrastructure

| Trigger phrase | Service |
|---|---|
| "**Infrastructure as Code (IaC)**", "**declarative templates**", JSON/YAML | **CloudFormation** |
| "**IaC in JavaScript / TypeScript / Python / Java / .NET**" | **AWS CDK** |
| "**Visual drag-and-drop IaC**", generates CFN/SAM | **Infrastructure Composer** |
| "**Platform as a Service (PaaS)**", "deploy app without managing infra" | **Elastic Beanstalk** |
| "**Hybrid deploy** to **EC2 + on-premises**", "blue/green" | **AWS CodeDeploy** |
| "**Source control / Git managed** in AWS" | **AWS CodeCommit** |
| "**Build, compile, test** source code, serverless" | **AWS CodeBuild** |
| "**Orchestrate CI/CD** pipeline (Source → Build → Test → Deploy)" | **AWS CodePipeline** |
| "**Artifacts / dependencies** (npm, pip, Maven, NuGet)" | **AWS CodeArtifact** |
| "**Manage fleet of servers** (EC2 + on-prem) at scale", patching, run commands | **AWS Systems Manager (SSM)** |
| "**SSH alternative without key pairs**" | **SSM Session Manager** |
| "**Visual workflow / orchestrate Lambdas**", parallel + retries + human approval | **AWS Step Functions** |

---

## 12. Integration & Messaging

| Trigger phrase | Service |
|---|---|
| "**Message queue**", "**decouple producer and consumer**", 1-to-1 | **Amazon SQS** |
| "**Pub/Sub**", "**fan-out**", one publisher → many subscribers | **Amazon SNS** |
| "**Real-time data streaming**", large volumes, video/clickstream | **Amazon Kinesis** |
| "**Open messaging protocols** (MQTT, AMQP, STOMP)" | **Amazon MQ** |
| "**Event-driven** + **decouple**", route events from AWS or SaaS | **Amazon EventBridge** |

---

## 13. Migration

| Trigger phrase | Service |
|---|---|
| "**Inventory of on-prem servers + dependencies**" (with or without agent) | **AWS Application Discovery Service** |
| "**Build a business case** for migration", "**cost baseline**" | **AWS Migration Evaluator** |
| "**Lift-and-shift execution** to AWS" (physical/virtual/cloud → AWS) | **AWS Application Migration Service (MGN)** |
| "**Central dashboard / track migration progress**" | **AWS Migration Hub** |
| "**Continuous block-level replication** for DR" | **AWS Elastic Disaster Recovery (DRS)** |
| "**Sync data from on-prem to AWS**", incremental hourly/daily/weekly | **AWS DataSync** |
| "**Hybrid storage** to S3" | **AWS Storage Gateway** |
| "**Migrate databases** (homogeneous/heterogeneous)" | **AWS DMS** |

---

## 14. Machine Learning

| Trigger phrase | Service |
|---|---|
| "**Image / video / face / object recognition**", celebrity / content moderation | **Amazon Rekognition** |
| "**Speech to text**", transcribe, **subtitles** | **Amazon Transcribe** |
| "**Text to speech**", voice synthesis, audiobooks | **Amazon Polly** |
| "**Translation**", localize content | **Amazon Translate** |
| "**Chatbot**", "**conversational AI**", "**Alexa-like**", ASR + NLU | **Amazon Lex** |
| "**Cloud call center / contact center**" | **Amazon Connect** |
| "**Natural Language Processing (NLP)**", **sentiment analysis**, entity extraction | **Amazon Comprehend** |
| "**Build, train, deploy custom ML models**", end-to-end | **Amazon SageMaker** |
| "**Time-series forecasting**", sales prediction, demand planning | **Amazon Forecast** |
| "**Document search with natural language**", PDFs/Word/FAQs | **Amazon Kendra** |
| "**Real-time personalized recommendations**", products/content | **Amazon Personalize** |
| "**OCR**", "extract text/tables/forms from documents/IDs" | **Amazon Textract** |

---

## 15. IoT, Edge, Satellite

| Trigger phrase | Service |
|---|---|
| "**Internet of Things**", "**billions of devices**", sensors → Cloud | **AWS IoT Core** |
| "**Satellite communications**", earth station network | **AWS Ground Station** |

---

## 16. Cost Management & Billing

| Trigger phrase | Service / Concept |
|---|---|
| "**Categorize and track costs in detail** by project/dept/team" | **Cost Allocation Tags** |
| "**Alert when budget is exceeded**" | **AWS Budgets** |
| "**Visualize and forecast costs**" | **AWS Cost Explorer** |
| "**Most comprehensive billing dataset**" | **AWS Cost and Usage Reports (CUR)** |
| "**Detect unusual spending** automatically with ML" | **AWS Cost Anomaly Detection** |
| "**Service quota / limit increase**" | **AWS Service Quotas** |
| "**Right-size recommendations** for EC2/EBS/Lambda" | **AWS Compute Optimizer** |
| "Cost / Performance / Security / Fault Tolerance / Service Limits" — **5 categories** | **Trusted Advisor** |
| "**1 bill** for multiple accounts", "**volume discounts**", "share RI/SP" | **Consolidated Billing** (in Organizations) |
| "**Mass account creation**", **SCPs** to restrict actions | **AWS Organizations** |
| "**Service Control Policies (SCPs)**", restrict APIs across accounts | **AWS Organizations** |
| "**Catalog of pre-approved IT products**" | **AWS Service Catalog** |
| "**Share resources across accounts**" | **AWS RAM** (Resource Access Manager) |
| "**Multi-account governance / landing zone**" | **AWS Control Tower** |

---

## 17. Support & Professional Services

| Trigger phrase | Plan / Service |
|---|---|
| "**Free**, available to all customers" | **Basic plan** |
| "**Email support, business hours**" | **Developer plan** |
| "**24/7 phone/chat**", critical down **< 1 hour** | **Business plan** |
| "**Technical Account Manager (TAM)**", critical down **< 15 min** | **Enterprise plan** |
| "**Infrastructure Event Management (IEM)**", "**Well-Architected Reviews**", "**Operations Reviews**" | **Enterprise plan** |
| "**Concierge** billing assistance" | **Business or Enterprise** |
| "**Specialty paid consulting / cloud adoption project**" | **AWS Professional Services** |
| "**Hire AWS-certified expert on-demand**", short projects | **AWS IQ** |
| "**AWS operates your infrastructure**" (run/maintain) | **AWS Managed Services (AMS)** |
| "**Network of partners / consultants / training**" | **APN** (AWS Partner Network) |
| "**Q&A community** replacing forums" | **AWS re:Post** |
| "**Marketplace for third-party software**" (single AWS bill) | **AWS Marketplace** |

---

## 18. AWS Cloud Concepts

| Trigger phrase | Concept |
|---|---|
| "**Pay only for what you use**" | Cloud essential characteristic |
| "**Variable expense / OPEX**" instead of upfront costs | **CAPEX → OPEX** |
| "**Scale automatically with demand**", cloud-friendly | **Elasticity** |
| "**Handle increased load** (vertical or horizontal)" | **Scalability** |
| "**Speed of provisioning** (weeks → minutes)" | **Agility** (NOT scalability) |
| "**Multi-AZ**, ≥ 2 AZs" | **High Availability (HA)** |
| "**Continue running** despite component failure" | **Fault Tolerance** |
| "**Recover from region/AZ outage**" | **Disaster Recovery** |
| "**Reduce TCO**" | Cloud economic benefit |
| "**Reduce time to market**", deploy in minutes | Cloud agility benefit |
| "**Stop guessing capacity**" | Cloud benefit (pay-as-you-go scale) |
| "**Go global in minutes**" | Cloud benefit (regions) |

---

## 19. Well-Architected Framework (6 Pillars)

| Trigger phrase | Pillar |
|---|---|
| "IaC, runbooks, automate processes, **monitoring proactively** — *how you operate*" | **Operational Excellence** |
| "IAM, encryption, **threats / attacks**, CIA triad" | **Security** |
| "**Multi-AZ, failover, backup, recover from failures**" | **Reliability** |
| "**Right instance type, latency, throughput, CDN, right-sizing**" | **Performance Efficiency** |
| "**Pay per use, RI/Spot, tagging, ROI, lowest cost**" | **Cost Optimization** |
| "**Environmental impact, energy efficiency, reduce idle resources**" | **Sustainability** (added 2021) |

> [!CAUTION]
> ❌ **NOT pillars** (common distractors): Availability, Scalability, Agility, Elasticity, Manageability, Recoverability.

**Reliability vs Performance Efficiency** (the classic trap):
- "**Replace unhealthy instances**" → Reliability
- "**Adapt to demand / not over-provision**" → Performance Efficiency

---

## 20. AWS CAF (Cloud Adoption Framework)

### 6 Perspectives

| Trigger phrase | Perspective |
|---|---|
| "**Align cloud with business goals**" | **Business** |
| "**Bridge between tech and business**, **culture** change" | **People** |
| "**Orchestrate initiatives**, risk management, governance" | **Governance** |
| "**Hybrid cloud platform**, modernize workloads" | **Platform** |
| "**Confidentiality, integrity, availability** of data" | **Security** |
| "**Deliver services at agreed level (SLA)**" | **Operations** |

### Security perspective — 9 capabilities

| Trigger phrase | Capability |
|---|---|
| "**Identity and access**" | **Identity and Access Management** |
| "**Detect threats** (anomalies, malicious activity)" | **Threat Detection** |
| "**Protect networks/hosts/apps** from unintended access and **vulnerabilities**" | **Infrastructure Protection** |
| "**Encryption**, classification of data" | **Data Protection** |
| "**Vulnerability / patching** strategy" | **Vulnerability Management** |
| "**Secure code / SDLC**" | **Application Security** |
| "**Respond** to security events" | **Incident Response** |

### Operations perspective — capabilities

| Trigger phrase | Capability |
|---|---|
| "**Match capacity to demand at agreed SLA**" | **Performance and Capacity Management** |
| "**Patch infrastructure**" | **Patch Management** |
| "**Track configuration changes**" | **Configuration Management** |
| "**Logs and metrics**" | **Observability** |

---

## 21. Shared Responsibility Model

| Trigger phrase | Whose responsibility |
|---|---|
| "**Host OS / hypervisor patching**" | **AWS only** |
| "**Guest OS patching** (inside EC2)" | **Customer only** |
| "**Network segmentation / NACL / Security Groups / Zone Security**" | **Customer only** |
| "**Hardware / data centers / physical security**" | **AWS only** |
| "**IAM users / roles / MFA**" | **Customer only** |
| "**Customer data / encryption of data**" | **Customer only** |
| "**Patch management** (in general)" | **Shared** |
| "**Configuration management** (in general)" | **Shared** |
| "**Awareness and training**" | **Shared** |

> [!TIP]
> Si la pregunta dice "**solely**" / "**only**" + customer → es algo del **lado del cliente puro** (zona de seguridad, IAM, datos, guest OS). Si dice solely + AWS → host/hypervisor/datacenter.

---

## 22. Common Traps & Distractors

| Trampa típica | Realidad |
|---|---|
| "Aurora supports **SQL Server**" | ❌ Aurora **only** MySQL & PostgreSQL — for SQL Server use **RDS** or **EC2** |
| "**ElastiCache is serverless**" | ❌ Managed pero basado en instancias; no es serverless |
| "**Reserve Instance** for **3 months**" | ❌ RI mínimo **1 año** — usa **On-Demand** |
| "**Sustainability is not a pillar**" | ❌ Es el **6º pilar** desde 2021 |
| "**Availability** is a pillar" | ❌ No — es **parte de Reliability** |
| "**Snow Family for online sync**" | ❌ Snow es **offline (físico)**; online sync es **DataSync** |
| "**S3 Transfer Acceleration delivers content to users**" | ❌ Es para **subir/bajar a S3** rápido. Para entregar a usuarios: **CloudFront** |
| "**MFA Delete is enabled by IAM users**" | ❌ Solo el **root account** puede activarlo |
| "**Egress-Only IGW** is for VPN" | ❌ Es solo para **IPv6 saliente**. VPN: **VGW + CGW** |
| "**Beanstalk deploys to on-premises**" | ❌ Beanstalk **solo AWS**. Para on-prem: **CodeDeploy + SSM** |
| "**Deferred payments** as cloud benefit" | ❌ OPEX es **gasto variable inmediato**, no diferido |
| "**Master/management account is the one paying** is reversed in Consolidated Billing" | ❌ El management **paga**, no al revés |
| "Stricter **IAM policies prevent unauthorized S3 deletion**" | ❌ Mejor: **MFA Delete** (factor adicional) |
| "**Threat Detection** in CAF Security covers infra protection" | ❌ Threat Detection = detectar; **Infrastructure Protection** = proteger redes/hosts/apps |
| "**Identity and Access Management** in CAF Operations" | ❌ IAM es de **Security perspective**, no Operations |
| "**Dedicated Instance** is best for BYOL" | ❌ **Dedicated Host** (visibilidad de socket/core) |
| "**AISPL** (India accounts) consolidates with global" | ❌ AISPL **no consolida** con cuentas globales |

---

## 23. Question-Pattern Phrases (jerga vista en simulacros)

Frases concretas en inglés que aparecen una y otra vez en los simulacros y que apuntan **directamente** a una respuesta.

### Pricing & purchasing

| Trigger phrase | Apunta a |
|---|---|
| "**All upfront / Partial upfront / No upfront**" | Modalidades de pago de **Reserved Instances** |
| "**Steady / predictable** workload" | **Reserved Instance** o **Savings Plan** |
| "**Spikes** in demand/traffic" | **Auto Scaling** (elasticidad) |
| "**Purchasing options**" | **Opciones de compra de EC2** (On-Demand / RI / Spot / Dedicated…) |
| "**Types of RI**" | Standard, Convertible, ~~Scheduled~~ (deprecated) |
| "**Server-bound software licenses**", "**per-socket licensing**" | **Dedicated Host** (BYOL) |
| "**Bundled AMI**" / "**license bundled in AMI**" | Windows + SQL Server **bundled AMI** (no necesitas comprar la licencia aparte) |
| "**AISPL accounts**" | **NO consolidan** con cuentas globales en Consolidated Billing |

### Performance & instance types

| Trigger phrase | Apunta a |
|---|---|
| "**Bare-metal**" | EC2 instancias `.metal` (acceso directo al hardware, sin hipervisor) |
| "**Multi-threading / chipsets**" | Compute-optimized o bare-metal EC2 |
| "**High-frequency trading (HFT)**", "**ultra-low latency**" | **NLB**, **FSx for Lustre**, EC2 placement groups (cluster) |
| "**Throughput-intensive**" | **Storage-optimized** instances (i3/d3) |
| "**I/O queries / high IOPS**" | **EBS Provisioned IOPS (io1/io2)** o **EC2 Instance Store** |

### Architecture & resilience

| Trigger phrase | Apunta a |
|---|---|
| "**Mission-critical**" | **Multi-AZ / High Availability** + **Enterprise** support plan |
| "**Non-stop / 24×7 / always-on**" | **HA Multi-AZ** |
| "**Failover**" | Route 53, **RDS Multi-AZ**, pilar de **Reliability** |
| "**Tightly coupled**" | ❌ Anti-patrón (monolítico) → **refactorizar**, decouple |
| "**Loosely coupled / decouple components**" | **SQS / SNS / EventBridge** |
| "**Event-driven application**" | **EventBridge / Lambda** |
| "**Short runtime / short executions**" | **AWS Lambda** (≤ 15 min) |
| "**Invoked by changes in data**", "**by shifts in system state**" | **AWS Lambda** (invocación dirigida por eventos) |
| "**Resilient / Resilience**" | Pilar de **Reliability** (Well-Architected) |
| "**Transient (network) issues**" | Patrones de **retry / fault tolerance** (Reliability) |
| "**Fleet of** (EC2 / servers)" | **Auto Scaling Group** o **Spot Fleet** |
| "**Idle** resources" | **Compute Optimizer** + pilar de **Sustainability** |
| "**Reduce overhead**" | Servicios **gestionados** / **serverless** |
| "**Space-constrained environment**" | **AWS Snowcone** (pequeño/portátil) |

### Security & monitoring

| Trigger phrase | Apunta a |
|---|---|
| "**Solely** / **sole**" responsibility | Modelo de Responsabilidad Compartida — **elimina** opciones "shared" |
| "**Threshold**" | **CloudWatch alarms** |
| "**Below** the threshold" | CloudWatch alarm en estado OK / abajo del límite |
| "**Breached** / **security gaps**" | **GuardDuty** / **Inspector** / **Security Hub** |
| "**Threat**" detection | **GuardDuty** |
| "**Adhering** to compliance / **burden** of compliance" | **AWS Artifact**, **AWS Config** |
| "**Coverage targets**" | Pilar de **Sustainability** o métricas de cumplimiento |

### Migration & business

| Trigger phrase | Apunta a |
|---|---|
| "**Lift and shift / shift workload**" | **AWS Application Migration Service (MGN)** — estrategia **Rehost** del 7R |
| "**Undergo migration**" | Servicios de migración (MGN, DMS, Discovery…) |
| "**Forecast** costs" | **Cost Explorer** |
| "**Forecast** demand / sales / time-series" | **Amazon Forecast** (servicio ML) |
| "**Expedite** cloud adoption / investments" | **AWS CAF** (Cloud Adoption Framework) |
| "**Business outcomes**" | **CAF Business** perspective |
| "**Stakeholder**" | **CAF Business/People** perspective |
| "**Agreed upon (SLA / level)**" | **CAF Operations** → **Performance and Capacity Management** |
| "**Tailored / customized** solution" | **AMI propia**, **CFN custom**, **Lightsail templates** según contexto |
| "**Seamlessly** integrates" | Servicios **gestionados / serverless** |
| "**Capability gaps**" | **CAF Align phase** — identifica gaps en las 6 perspectivas para preparar el plan de acción |
| "**Rely on legacy systems**" | Modernización vía **7R** (típicamente **Refactor** o **Replatform**) y **MGN** |

> [!TIP]
> Para el **vocabulario en inglés** que aparece en preguntas pero NO es trigger directo de un servicio, mira [VOCABULARIO.md](./VOCABULARIO.md).

---

[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](./README.md)
