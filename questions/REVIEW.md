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
> **Exam tip:** **path/host routing + WebSockets + HTTP** → **ALB**. **TCP/UDP + millions of req/s + static IP** → **NLB**. **Network appliances** → **Gateway LB**.

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
