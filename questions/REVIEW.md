[![](https://img.shields.io/badge/<-FF4859?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](../README.md)

# CCP Practice Exam Review — Weak Points

**Result:** 83% (54/65) — Passed (70% threshold)

| Domain | AWS Weight | Score | Priority |
|---------|----------|---------|-----------|
| **Cloud Technology and Services** | **34%** | **77%** | 🔴 **HIGHEST** |
| **Security and Compliance** | **30%** | 89% | 🟡 Medium |
| **Cloud Concepts** | 24% | 92% | 🟢 Low |
| **Billing, Pricing, and Support** | 12% | 80% | 🟡 Medium |

> [!IMPORTANT]
> This README is ordered to focus first on domains with **highest weight × lowest score**.

---

# 🔴 1. Cloud Technology and Services (34%)

## 1.1 Decoupling and event-driven applications → **EventBridge** (not SNS)

**Sample question (Q25):** *"Which AWS service enables you to build event-driven applications and decouple components?"*

| Service | When it's the answer |
|---|---|
| **Amazon EventBridge** | **Event-driven applications**, rule → target, AWS or app events |
| **Amazon SQS** | **Message queue** (producers/consumers, decouple work) |
| **Amazon SNS** | **Pub/Sub** — one publisher to many subscribers |
| **Amazon Kinesis** | **Real-time streaming** of large data volumes |

> [!TIP]
> **Exam tip:** the keyword **"event-driven"** + **"decouple components"** = **EventBridge**. If it just says **"decouple"** without event-driven, it's almost always **SQS**. **SNS** = pub/sub (notify many at once).

## 1.2 Hybrid deployment to on-premises → **Systems Manager + CodeDeploy**

**Sample question (Q27):** *"Company with hybrid architecture wants to deploy a web app to on-premises servers. Which services to use? (Select TWO)"*

- ✅ **AWS Systems Manager** — manages **EC2 and on-premises** instances (run commands, patching, inventory). Hybrid by definition.
- ✅ **AWS CodeDeploy** — deploys code to **EC2, Lambda, ECS, and on-premises servers**.
- ❌ **Elastic Beanstalk** — only deploys to **AWS** infrastructure, not on-premises.
- ❌ **CloudFormation** — provisions AWS infra, doesn't apply to on-prem servers.

> [!TIP]
> **Exam tip:** if it says **"on-premises"** + **"deploy"**, the two services are **Systems Manager** (management) and **CodeDeploy** (code deployment). **Elastic Beanstalk does NOT work on-prem**.

## 1.3 EC2: purchasing options and licensing

**Sample question (Q48):** *"Which EC2 purchasing option lets you use existing licenses (BYOL) and meet compliance requirements?"*

| Option | When |
|---|---|
| **Dedicated Host** | **Dedicated physical server**, **socket/core visibility**, ideal for **BYOL** (Bring Your Own License) and compliance |
| **Dedicated Instance** | Dedicated hardware **but no physical host visibility**. Doesn't work for per-socket BYOL |
| **Reserved Instance** | 1-3 year commitment, discount — not related to licensing |
| **On-Demand** | Pay per use, no commitment |

> [!TIP]
> **Exam tip:** **"existing licenses" / "BYOL" / "per socket or core"** → **Dedicated Host**. If it only says "dedicated hardware without BYOL" → Dedicated Instance.

## 1.4 Reserved Instances — types

**Sample question (Q20):** *"You need to launch an EC2 that will change instance family, OS, and tenancy 3 months after the trial. Which RI type?"*

| RI Type | When |
|---|---|
| **Standard RI** | Highest discount, **cannot change family/OS/tenancy** |
| **Convertible RI** | Allows **changing family, OS, tenancy** (with lower discount) |
| **Scheduled RI** | For **specific recurring schedules** (deprecated) |

> [!TIP]
> **Exam tip:** if the question mentions **"changing family/OS/tenancy"** → **Convertible RI**. If flexible across **whole family + region** → EC2 Instance Savings Plan. If flexible across **everything + Fargate/Lambda** → Compute Savings Plan.

## 1.5 Databases: SQL Server quickly and efficiently → **RDS + EC2**

**Sample question (Q57):** *"Team needs SQL Server in AWS quickly and efficiently. (Select TWO)"*

- ✅ **Amazon RDS (for SQL Server)** — managed, ready in minutes
- ✅ **Amazon EC2** — install SQL Server yourself (full control)
- ❌ **Amazon Aurora** — supports **MySQL/PostgreSQL only**, NOT SQL Server
- ❌ **Aurora Backtrack** — Aurora feature, doesn't apply
- ❌ **Redshift** — data warehouse, not OLTP

> [!TIP]
> **Exam tip:** **Aurora ≠ SQL Server**. Aurora only supports **MySQL and PostgreSQL**. For **SQL Server, Oracle, MariaDB** → **RDS** (managed) or **EC2** (self-managed).

## 1.6 On-premises ↔ VPC connection: VPN

**Sample question (Q63):** *"What do you use to resolve the connection between your on-premises VPN and your VPC?"*

- **Virtual Private Gateway (VGW)** — the AWS side of the VPN
- **Customer Gateway (CGW)** — the on-premises side of the VPN
- ❌ **Egress-Only Internet Gateway** — only for **outbound IPv6 traffic** from VPC
- ❌ **NAT Gateway** — for private instances to reach the Internet
- ❌ **VPC Peering** — connects VPCs to each other

> [!TIP]
> **Exam tip:** **Site-to-site VPN** = **VGW (AWS side)** + **CGW (on-prem side)**. **Egress-Only IGW** is only for **outbound IPv6**, don't confuse with VPN.

## 1.7 Application Load Balancer (ALB) — key features

**Sample question (Q1):** *"Which ELB supports path-based routing, host-based routing, and bidirectional WebSockets?"*

- ✅ **ALB** — Layer 7 (HTTP/HTTPS), **path-based, host-based, WebSockets, HTTP/2, redirects**
- ❌ **NLB** — Layer 4 (TCP/UDP), ultra-low latency, static IP
- ❌ **Gateway LB** — for network appliances (firewalls, IDS/IPS) at Layer 3
- ❌ **CLB** — legacy, don't use

> [!TIP]
> **Exam tip:**
> - **ALB** → path/host routing + WebSockets + HTTP
> - **NLB** → TCP/UDP + millions of req/s + static IP
> - **Gateway LB** → network appliances (firewalls, IDS/IPS)

---

# 🟡 2. Security and Compliance (30%)

## 2.1 Shared Responsibility Model — **solely customer's** responsibility

**Sample question (Q42):** *"Which of the following is **solely the customer's** responsibility?"*

**Customer (security IN the cloud):**
- ✅ **Service and Communications Protection / Zone Security** (network segmentation, NACL, SG)
- ✅ Customer data (encryption, classification)
- ✅ IAM management (users, roles, MFA)
- ✅ **Guest** OS configuration (on EC2)
- ✅ Network configuration (VPC, SG, NACL)
- ✅ Awareness & Training (employee training — but AWS also offers this, hence not "solely")

**AWS (security OF the cloud):**
- 🔵 **Host OS patching** (hypervisor)
- 🔵 Hardware, software, physical facilities
- 🔵 Managed services (RDS, S3 at infrastructure level)

**Shared:**
- 🟡 **Configuration Management** — AWS configures infra, customer configures their apps
- 🟡 Patch Management — AWS patches the infra, customer patches the EC2 OS
- 🟡 Awareness & Training

> [!TIP]
> **Exam tip:** if the question says **"solely"** or **"only the customer"**, eliminate anything shared (Config Management, Patch Mgmt, Training). **Host OS patching** is always **AWS**. **Zone security / network segmentation** is always **customer**.

---

# 🟢 3. Cloud Concepts (24%)

## 3.1 Financial benefit of migrating to AWS → **CAPEX → OPEX**

**Sample question (Q36):** *"What is a key financial benefit of migrating from on-prem to AWS?"*

✅ **Replace upfront capital expenses (CAPEX) with low variable costs (OPEX).**

- **CAPEX** = large upfront investment (servers, datacenter)
- **OPEX** = recurring operational expense, variable, pay-as-you-go

> [!TIP]
> **Exam tip:** Cloud = **CAPEX → OPEX**. You **pay only for what you use**, no upfront hardware purchase. Memorize the order: **upfront CAPEX → low variable OPEX**.

## 3.2 Edge Locations — benefits

**Sample question (Q65):** *"What are the benefits of Edge Locations? (Select TWO)"*

- ✅ **Caching that reduces load on origin servers** (CloudFront caches content)
- ✅ **Improves performance by delivering content closer to users** (low latency)
- ❌ Edge computing devices (that's Snowball Edge / Snowcone)
- ❌ Scalable object storage (that's S3)

> [!TIP]
> **Exam tip:** **Edge Locations = CloudFront**. Benefits = **cache + low latency**. **Don't confuse** with Snow Family (physical edge computing devices).

---

# 🟡 4. Billing, Pricing, and Support (12%)

## 4.1 Categorize and track costs at a detailed level → **Cost Allocation Tags**

**Sample question (Q45):** *"What lets you categorize and track your AWS costs at a detailed level?"*

| Service | Purpose |
|---|---|
| **Cost Allocation Tags** | **Categorize and track** costs in detail by project, department, team |
| **AWS Budgets** | **Alerts** when a budget is exceeded |
| **Consolidated Billing** | One bill for multiple accounts |
| **Cost Explorer** | **Visualize** and forecast costs |
| **AWS CUR** | The **most comprehensive** billing dataset |

> [!TIP]
> **Exam tip:** **"categorize and track costs in detail"** → **Cost Allocation Tags**. **"alerts when budget is exceeded"** → **Budgets**.

## 4.2 Consolidated Billing benefits

**Sample questions (Q16, Q51):**

✅ **Real benefits:**
- **Volume pricing** — volume discounts by combining usage across all accounts
- **Share RIs and Saving Plans** between organization accounts
- **One single bill** for all accounts
- **Single payment method**

❌ **Common traps:**
- "One member account paying charges of all master accounts" — **inverted**: the **master/management** pays, not a member
- "$1 every month" — false
- "AISPL accounts consolidation" — AISPL (India) **cannot be consolidated** with global accounts

> [!TIP]
> **Exam tip:** Consolidated Billing = **1 bill + volume discounts + share RI/SP**. The **master (management) account** pays, not the other way around. **AISPL doesn't consolidate** with AWS global.

## 4.3 AWS Professional Services vs TAM vs Concierge

**Sample question (Q30):** *"Which channel offers paid engagements in specialty practice areas for cloud adoption?"*

| Service | What it does |
|---|---|
| **AWS Professional Services** | **Paid engagements** specialized, **consulting projects** for cloud adoption |
| **AWS Technical Account Manager (TAM)** | **Assigned to your account** in Enterprise plans. Continuous advisory, does NOT execute projects |
| **Concierge Support** | **Billing and account** support team (Business/Enterprise) |
| **AWS Enterprise Support** | The **support plan**, not a professional service |

> [!TIP]
> **Exam tip:** **"paid engagements" / "specialty practices" / "consulting projects"** → **AWS Professional Services**. **TAM** = assigned person for advisory, doesn't execute projects.

## 4.4 Trusted Advisor — the 5 categories

**Sample question (Q10):** *"Which are the 5 Trusted Advisor categories? (Select TWO)"*

The **5 categories** are:
1. **Cost Optimization**
2. **Performance**
3. **Security**
4. **Fault Tolerance**
5. **Service Limits** (Service Quotas)

❌ NOT: Infrastructure, Instance Usage, Storage Capacity

> [!TIP]
> **Exam tip — mnemonic "CPSF-L":** **C**ost · **P**erformance · **S**ecurity · **F**ault Tolerance · service **L**imits.

---

# Summary — what to memorize before the exam

| Common confusion | Correct answer |
|---|---|
| Event-driven + decouple | **EventBridge** (not SNS) |
| Decouple only (without event-driven) | **SQS** |
| Pub/Sub | **SNS** |
| Deploy to on-premises | **Systems Manager + CodeDeploy** (not Beanstalk) |
| BYOL / per-socket licensing | **Dedicated Host** (not Dedicated Instance) |
| Change family/OS/tenancy in RI | **Convertible RI** |
| SQL Server in AWS | **RDS for SQL Server + EC2** (NOT Aurora) |
| On-prem VPN ↔ VPC | **VGW + CGW** (not Egress-Only IGW) |
| ALB vs NLB | ALB = HTTP/path/host/WebSocket; NLB = TCP/UDP/static IP |
| Solely customer responsibility | **Zone Security / network segmentation** |
| Solely AWS responsibility | **Host OS patching** |
| CAPEX vs OPEX | Cloud = **CAPEX → OPEX** |
| Edge Locations | Cache + latency (CloudFront) |
| Categorize costs in detail | **Cost Allocation Tags** (not Budgets) |
| Consolidated Billing | **1 bill + volume pricing + share RI/SP** |
| Specialty paid consulting | **AWS Professional Services** |
| 5 Trusted Advisor categories | **C**ost · **P**erformance · **S**ecurity · **F**ault Tolerance · service **L**imits |

---

# CCP Practice Exam 2 Review — Weak Points

**Result:** 86% (56/65) — Passed (70% threshold)

| Domain | AWS Weight | Score | Wrong impact (W × error%) | Priority |
|---------|----------|---------|---------|-----------|
| **Cloud Concepts** | 24% | 79% | **5.04** | 🔴 **HIGHEST** |
| **Security and Compliance** | 30% | 87% | 3.90 | 🟡 Medium |
| **Billing, Pricing, and Support** | 12% | 78% | 2.64 | 🟡 Medium |
| **Cloud Technology and Services** | 34% | 96% | 1.36 | 🟢 Low |

> [!IMPORTANT]
> Despite Cloud Tech having the highest weight (34%), it scored 96%, so its weighted error impact is the lowest. Focus first on **Cloud Concepts** and **Security**.

---

## 🔴 1. Cloud Concepts (24%)

### 1.1 ❌ AWS CAF Security perspective — capabilities

**Q33 (failed):** *"Startup wants to protect all applications against unintended/unauthorized access and potential vulnerabilities. Which AWS CAF Security perspective capability is most relevant?"*

- ✅ **Infrastructure Protection** — protects systems, networks, and applications **at the host, network and edge layer** (covers "unintended access + vulnerabilities" against infra).
- ❌ **Threat Detection** — *detect* threats (GuardDuty-style), not prevent the access in the first place.
- ❌ **Identity and Access Management** — focuses on **identity**, not network/app/host protection.
- ❌ **Data Protection** — focuses on **encryption / data classification**, not access protection of apps.

**The 9 capabilities of CAF's Security perspective** (memorize):
1. **Security Governance**
2. **Security Assurance**
3. **Identity and Access Management**
4. **Threat Detection**
5. **Vulnerability Management**
6. **Infrastructure Protection** ← *protect networks, hosts, and apps*
7. **Data Protection**
8. **Application Security**
9. **Incident Response**

> [!TIP]
> **Exam tip:** if the question mentions **"protecting applications/networks against unintended access or vulnerabilities"** → **Infrastructure Protection**. If it says **"detecting"** suspicious activity → **Threat Detection**. If it says **"identity"** → **IAM**.

### 1.2 ❌ Cloud benefits beyond CAPEX → OPEX — *Reduce Time to Market*

**Q58 (failed):** *"When a company decouples from their on-premises data center, which TWO benefits do they get?"*

- ✅ **Reduce time to market** — provision in minutes vs weeks/months on-prem
- ✅ **Decrease your TCO** (Total Cost of Ownership)
- ❌ "Replace low variable costs with upfront CAPEX" — **inverted**: cloud goes from CAPEX → OPEX, not the other way
- ❌ "Massive discounts for bare metal from Amazon.com" — fake distractor
- ❌ "**Deferred payments** to operational expenditures" — wrong wording. OPEX is **immediate variable** spend, not "deferred". Common trap.

> [!TIP]
> **Exam tip:** when listing cloud benefits, the typical TWO are **agility (faster time to market)** + **lower TCO**. **"Deferred payments"** is a trap — OPEX is immediate variable cost, not deferred.

### 1.3 ⚠️ AWS CAF Operations perspective (passed but doubt)

**Q48 (correct, doubt):** *"Which CAF Operations capability is most helpful to consistently deliver cloud services at the agreed level?"*

- ✅ **Performance and Capacity Management** — ensures the **agreed-upon service level** (SLA) is met by sizing and monitoring capacity.

**The capabilities of CAF's Operations perspective** (less obvious, memorize):
1. Observability
2. Event Management (AIOps)
3. Incident and Problem Management
4. Change and Release Management
5. **Performance and Capacity Management** ← *match capacity to demand at agreed SLA*
6. Configuration Management
7. Patch Management
8. Availability and Continuity Management
9. Application Performance Monitoring

> [!TIP]
> **Exam tip:** **"deliver consistently at the agreed level / SLA / capacity"** → **Performance and Capacity Management** (Operations perspective). **"Identity and Access Management"** is a Security capability, not Operations — common distractor in these questions.

---

## 🟡 2. Security and Compliance (30%)

### 2.1 ❌ Shared Responsibility — Host OS patching is **AWS** alone

**Q15 (failed):** *"In the Shared Responsibility Model, whose responsibility is it to patch the host OS of an EC2 instance?"*

- ✅ **AWS** — the **host** OS (the hypervisor) is patched by AWS.
- ❌ Customer — the customer patches the **guest** OS (inside the EC2 VM).
- ❌ Both — common trap: it sounds shared but **host vs guest** are clearly separated.

**Memorize:**
| Layer | Who patches |
|---|---|
| **Host OS / hypervisor** | **AWS** (only) |
| **Guest OS (inside EC2)** | **Customer** (only) |
| Managed services (RDS, Lambda) OS | **AWS** |

> [!TIP]
> **Exam tip:** **host = hypervisor → AWS**. **Guest = inside the EC2 → customer**. If the wording is "host", the answer is **AWS, NOT both**. Don't fall for the "shared" distractor when the question is specific about the host.

### 2.2 ❌ Prevent unauthorized S3 deletion → **MFA Delete**

**Q30 (failed):** *"How to prevent unauthorized deletion of S3 objects?"*

- ✅ **MFA Delete** — requires **MFA token** to permanently delete object versions or to disable versioning.
- ❌ Stricter IAM policies — can mitigate but a compromised IAM still has the listed permissions; doesn't add a separate factor.
- ❌ Set bucket private — controls **public access**, not internal account deletion.
- ❌ Access control policies — same issue: doesn't require MFA at delete time.

**Conditions for MFA Delete:**
- Versioning **must be enabled**.
- Only the **bucket owner (root account)** can enable/disable MFA Delete (not regular IAM users).
- Requires **AWS CLI/SDK** (cannot enable from console).

> [!TIP]
> **Exam tip:** **"prevent accidental/unauthorized deletion of S3 objects"** → **MFA Delete** (with versioning). Bucket policies and IAM are about *access*, not about adding a *second factor* at delete time.

---

## 🟡 3. Billing, Pricing, and Support (12%)

### 3.1 ❌ Support plans — Infrastructure Event Management, Well-Architected & Operations Reviews

**Q28 (failed):** *"Customer has Basic plan and wants to use Infrastructure Event Management, Well-Architected Reviews and Operations Reviews features. Cheapest plan to upgrade to?"*

- ✅ **Enterprise** — these features are **Enterprise-only** (and Enterprise On-Ramp partially).
- ❌ Developer / Business — do **not** include IEM, WAR or Ops Reviews as standard.

**Plan-level features cheat sheet:**
| Feature | Plan |
|---|---|
| **TAM (Technical Account Manager)** | **Enterprise** (and Enterprise On-Ramp) |
| **Infrastructure Event Management (IEM)** | **Enterprise** (paid add-on for Business) |
| **Well-Architected Reviews** | **Enterprise** |
| **Operations Reviews** | **Enterprise** |
| **Concierge (billing assistance)** | Business and Enterprise |
| **24/7 phone/chat** | Business and Enterprise |
| **Trusted Advisor — full checks** | Business and Enterprise |

> [!TIP]
> **Exam tip:** if the question lists **Infrastructure Event Management, WAR, Ops Reviews, or TAM**, you need **Enterprise** (rarely Enterprise On-Ramp). Nothing below Business gives you any of these.

---

## 🟢 4. Cloud Technology and Services (34%)

### 4.1 ❌ Serverless platform components — **API Gateway + Lambda@Edge** (not ElastiCache)

**Q8 (failed):** *"Which TWO services are part of the AWS serverless platform that doesn't require provisioning or maintaining servers?"*

- ✅ **Amazon API Gateway** — fully serverless API management.
- ✅ **Lambda@Edge** — runs Lambda functions at CloudFront edge locations, serverless.
- ❌ **Amazon ElastiCache** — managed cache (Redis/Memcached) but **runs on EC2-style nodes**, you choose instance type/size — **NOT serverless**.
- ❌ **Amazon EMR** — Hadoop cluster, requires EC2 cluster, **NOT serverless**.
- ❌ **Amazon OpenSearch** — runs on managed instances, not serverless (OpenSearch Serverless is a separate variant).

> [!TIP]
> **Exam tip:** **ElastiCache is NOT serverless** — it requires choosing node types and clusters. The classic serverless suite for the exam: **Lambda, Lambda@Edge, API Gateway, DynamoDB, Aurora Serverless, S3, SNS, SQS, EventBridge, Step Functions, Fargate**.

### 4.2 ❌ Speed up global content delivery → **CloudFront** (not S3 Transfer Acceleration)

**Q10 (failed):** *"Which service speeds up content delivery to your customers?"*

- ✅ **Amazon CloudFront** — global CDN that **delivers cached content** (images, videos, HTML) to users with low latency.
- ❌ **S3 Transfer Acceleration** — speeds up **uploads/downloads to/from S3** through edge locations. It's about **data transfer to S3**, not **content delivery to users**.
- ❌ CloudWatch / CloudTrail — monitoring/audit, unrelated.

> [!TIP]
> **Exam tip:** **delivering content to end-users globally** → **CloudFront**. **Uploading large files to an S3 bucket from far away** → **S3 Transfer Acceleration**. They're *both* edge-based but with **opposite directions of the data flow**.

### 4.3 ❌ SQL Server with cost-flexibility + RDP → **Bundled AMI** (not RDS)

**Q18 (failed):** *"Company wants SQL Server in AWS, managed by their DBA, accessible via RDP, with a Standard license, but unsure how much CPU/RAM to allocate. Which option is most flexible and cost-effective?"*

- ✅ **Use a Windows Server with SQL Server Standard bundled AMI** — license is **included in the EC2 hourly price**, you pick **any EC2 size** (flexibility for sizing), and DBA gets **RDP access**.
- ❌ **RDS for SQL Server** — managed by AWS, **not by the company's DBA**, and **no RDP access** to the underlying host. Disqualified by the requirements.
- ❌ EC2 + buy your own MSSQL license — you have to **manage the license**, less convenient.
- ❌ Aurora MS SQL Server — **doesn't exist** (Aurora supports only MySQL and PostgreSQL).

> [!TIP]
> **Exam tip:** keywords **"managed by company DBA" + "RDP access"** rule out RDS (RDS doesn't give SSH/RDP). Keywords **"unsure of CPU/RAM" + "cost-effective"** favor a **bundled AMI** so you can resize EC2 freely without buying a license.

### 4.4 ❌ EC2 for **3-month** uninterruptible job → **On-Demand**

**Q35 (failed):** *"Best EC2 purchasing option for a 3-month uninterruptible job?"*

- ✅ **On-Demand** — no commitment, pay per hour/second, perfect for **short-term workloads (≤ 1 year)**.
- ❌ **Reserved Instance** — minimum commitment is **1 year** (or 3 years), not worth it for 3 months.
- ❌ **Spot Instance** — can be **interrupted** by AWS; question explicitly says "uninterruptible".
- ❌ **Dedicated Instance** — about **isolation/licensing**, not about commitment length.

> [!TIP]
> **Exam tip:** for **short-term + uninterruptible** → **On-Demand**. RIs and Savings Plans require **1-year minimum**, so any workload **shorter than a year** is On-Demand. Spot is for **interruptible** jobs only.

### 4.5 ⚠️ NLB use case (passed but doubt)

**Q6 (correct, doubt):** *"Best load balancer for TCP/UDP/TLS, millions of req/s with ultra-low latency?"*

- ✅ **Network Load Balancer (NLB)** — Layer 4 (TCP/UDP/TLS), **millions of req/s**, **ultra-low latency**, static IP per AZ.

| ELB type | When |
|---|---|
| **ALB** | Layer 7 — HTTP/HTTPS, path/host routing, WebSockets |
| **NLB** | **Layer 4 — TCP/UDP/TLS, ultra-low latency, millions of req/s, static IP** |
| **GWLB** | Layer 3 — deploy network appliances (firewalls, IDS/IPS) |
| CLB | Legacy, do not use |

> [!TIP]
> **Exam tip:** the trio of keywords **TCP / UDP / TLS** + **millions of req/s** + **ultra-low latency** = **NLB**. If you also see **static IP**, even more sure.

### 4.6 ⚠️ Snowball Edge for petabyte transport (passed but doubt)

**Q7 (correct, doubt):** *"Data transport solution that accelerates moving terabytes to petabytes of data into and out of AWS using appliances with on-board storage and compute?"*

- ✅ **AWS Snowball Edge** — physical appliances with **storage AND compute** (run EC2/Lambda offline). Up to ~80 TB usable per device, multiple devices for petabyte transfers.
- ❌ **AWS Snowcone** — smaller (8–14 TB), portable; not for **petabyte** scale on its own.
- ❌ **AWS DataSync** — online sync over the **network**, not a physical appliance.
- ❌ **Lambda@Edge** — totally unrelated (CDN code execution).

| Service | Capacity | Online/Offline |
|---|---|---|
| **Snowcone** | 8 TB HDD / 14 TB SSD | Online or offline |
| **Snowball Edge** | up to ~80 TB | **Offline (physical)** |
| **Snowmobile** | up to ~100 PB | **Offline (truck!)** |
| **DataSync** | n/a | **Online (over network)** |

> [!TIP]
> **Exam tip:** **physical device with storage + compute + offline** → **Snowball Edge**. If the question mentions an order of magnitude in **exabytes**, it's **Snowmobile**. **Online network sync** = **DataSync**.

---

# Summary — exam 2 — what to memorize

| Common confusion | Correct answer |
|---|---|
| CAF Security: protect apps from unintended access + vulnerabilities | **Infrastructure Protection** (not Threat Detection) |
| CAF Operations: deliver consistently at agreed SLA | **Performance and Capacity Management** |
| Cloud benefit beyond CAPEX→OPEX | **Reduce time to market** + lower TCO (NOT "deferred payments") |
| Host OS patching | **AWS only** (not "both") |
| Prevent unauthorized S3 deletion | **MFA Delete** (with versioning) |
| Get IEM, WAR, Ops Reviews features | **Enterprise** support plan |
| Serverless platform examples | **API Gateway + Lambda@Edge** (NOT ElastiCache) |
| Speed up content delivery to users | **CloudFront** (NOT S3 Transfer Acceleration) |
| SQL Server, DBA-managed, RDP access, flexible size | **Windows + SQL Server bundled AMI** (NOT RDS, NOT Aurora) |
| 3-month uninterruptible EC2 job | **On-Demand** (RI minimum is 1 year) |
| TCP/UDP/TLS + millions req/s + ultra-low latency | **NLB** |
| TB-PB physical data transfer with compute | **Snowball Edge** |
