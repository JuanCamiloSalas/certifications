[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/SAA-175074?style=for-the-badge)](../README.md)

# SAA Practice Test 2 — Weak Points

**Result:** 64% (42/65) — Failed (exceeded standard time; within limit with +30 min ESL). 2026-06-16.

| Domain | AWS Weight | Score | Error impact (W × err%) | Priority |
|---|---|---|---|---|
| **Design Resilient Architectures** | 26% | 47% | **13.8** | 🔴 HIGHEST |
| **Design Cost-Optimized Architectures** | 20% | 50% | 10.0 | 🟡 High |
| **Design Secure Architectures** | 30% | 71% | 8.7 | 🟡 Medium |
| **Design High-Performing Architectures** | 24% | 87% | 3.1 | 🟢 Low |

> [!IMPORTANT]
> Ordered by **highest weight × lowest score**. Vs Test 1: High-Performing improved (65% → 87%) but **Cost collapsed (100% → 50%)** and Secure dropped (90% → 71%). Resilient is still the worst — chronic.

---

# 🔴 1. Design Resilient Architectures (26%)

## 1.1 RDS Multi-AZ failover behavior → CNAME switch

**Sample question (Q54):** *"RDS Multi-AZ — what happens when the primary instance fails?"*

- ✅ The **CNAME (DNS) record is switched** from primary to standby. The client endpoint stays the same.
- ❌ "The IP address is switched to the standby" — the IP doesn't move; the DNS does.

> [!TIP]
> **Exam tip:** Multi-AZ failover = **DNS/CNAME repointed to the standby**, not an IP change. The endpoint is stable for the application.
> 📇 [Card: RDS](../cards/04-rds-aurora/01-rds.md)

## 1.2 Failover of a private IP → secondary ENI

**Sample question (Q31):** *"Dashboard on a Spot EC2 in a private subnet, reached via a domain mapped to the instance's private IP. Resume traffic on another instance if the primary is terminated."*

- ✅ Create a **secondary ENI** with the private IP mapped to the domain; move the ENI to another instance on failure.
- ❌ Elastic IP + Transit Gateway — EIP is **public**, doesn't apply to an internal private IP.

> [!TIP]
> **Exam tip:** **private-IP failover = secondary ENI** you can detach/reattach. Elastic IP is for public addressing.
> 📇 [Card: VPC Foundations](../cards/15-vpc/01-vpc-foundations.md)

## 1.3 Direct Connect resilience → 2nd DX + backup VPN

**Sample question (Q30):** *"Single Direct Connect to VPC-1. Increase the fault tolerance of the connection to VPC-1 (Select TWO)."*

- ✅ A **second Direct Connect + private VIF in the same region as VPC-1**.
- ✅ A **hardware VPN over the Internet between VPC-1 and on-prem** (backup path).
- ❌ Anything pointing at VPC-2 — the redundancy must target the VPC you're protecting.

> [!TIP]
> **Exam tip:** DX resilience = **second DX** (full redundancy) or a **site-to-site VPN backup**, both to the **same VPC**. A peered VPC doesn't add resilience to VPC-1's link.
> 📇 [Card: Direct Connect](../cards/15-vpc/07-direct-connect.md)

## 1.4 Automate EBS snapshots → Data Lifecycle Manager

**Sample question (Q28):** *"Automated backup of all EBS volumes — fastest, cost-effective, simple to maintain."*

- ✅ **Amazon Data Lifecycle Manager (DLM)** — automates EBS snapshot creation/retention.
- ❌ AWS Backup retention rule (broader/heavier) · CLI cron · Storage Gateway.

> [!TIP]
> **Exam tip:** **automate EBS snapshots, simple** → **DLM**. AWS Backup is the centralized multi-service option, not the lightest for plain EBS.
> 📇 [Card: EBS Snapshots](../cards/02-storage-ec2/02-ebs-snapshots.md)

## 1.5 Continuous on-prem → AWS DB sync → DMS full load + CDC

**Sample question (Q58):** *"On-prem MySQL replicated to S3/Aurora; ongoing changes must be captured continuously, low overhead."*

- ✅ **DMS full load + change data capture (CDC)** task, with a CA certificate + DMS endpoint over **SSL**.
- ❌ DMS with SSL via Network Firewall · one-off full load only · SCT + MGN.

> [!TIP]
> **Exam tip:** **continuous migration with ongoing changes = DMS + CDC**. SSL comes from a CA cert on the DMS endpoint, not Network Firewall.
> 📇 [Card: DMS & SCT](../cards/16-dr-migration/02-dms-sct.md)

## 1.6 Elasticity for a single EC2 → ELB + Route 53 weighted · *(Select TWO)*

**Sample question (Q19):** *"Single EC2 web app; user volume will grow — add elasticity and scalability."*

- ✅ **Two EC2 behind an ELB**, and **two EC2 + Route 53 weighted routing**.
- ❌ Launch Templates + **AWS Glue** (Glue is ETL, irrelevant) · WAF · S3 cache.

> [!TIP]
> **Exam tip:** elasticity/scaling for EC2 = **ELB** and/or **Route 53 routing**. Glue/WAF/S3-cache are distractors here.
> 📇 [Card: Load Balancers](../cards/03-elb-asg/01-load-balancers.md)

## 1.7 Bias traffic by geography → Route 53 Geoproximity

**Sample question (Q42):** *"Route a larger portion of traffic from a region (Philippines/N. India) to a specific AWS region."*

- ✅ **Geoproximity routing** — lets you shift traffic to a resource using a bias.
- ❌ **Geolocation** (maps user location → endpoint, no bias) · Weighted · Latency.

> [!TIP]
> **Exam tip:** **"bias / shift more traffic by geography"** = **Geoproximity**. **"route by user location"** = **Geolocation**.
> 📇 [Card: Routing Policies 2](../cards/05-route53/03-routing-policies-2.md)

---

# 🟡 2. Design Cost-Optimized Architectures (20%)

> [!NOTE]
> There is **no billing/cost card block** in the repo yet — this domain has no study material, which is likely why it dropped to 50%. Candidate for new cards.

## 2.1 Track cost by department → Cost Allocation Tags

**Sample question (Q16):** *"Generate a monthly report of total billing per department."*

- ✅ Tag resources by department + enable **Cost Allocation Tags**.
- ❌ Tags + **Budgets action** (Budgets = alerts) · Cost Explorer filter · CUR.

> [!TIP]
> **Exam tip:** **categorize/track cost by department** → **Cost Allocation Tags**. Budgets = alerts when a threshold is crossed. *(Same concept missed on the CCP exam.)*
> 📇 Card: _none yet (no billing block)_

## 2.2 Archive on-prem data → DataSync direct to Glacier Deep Archive

**Sample question (Q13):** *"Move historical records from on-prem to AWS — best cost + operational management."*

- ✅ **DataSync → S3 Glacier Deep Archive** directly as the destination.
- ❌ DataSync → S3 Standard **+ lifecycle** to Deep Archive after 30 days — pays for Standard + an extra step for data that's cold from day one.

> [!TIP]
> **Exam tip:** if data is **archival from the start**, write **straight to Glacier Deep Archive**. Don't stage in Standard + lifecycle.
> 📇 [Card: DataSync & MGN](../cards/16-dr-migration/03-datasync-mgn.md)

## 2.3 TB over a slow line → offline / physical transfer

**Sample question (Q45):** *"250 TB on-prem to S3; 100 Mbps line would take weeks. Fastest + most cost-effective."*

- ✅ **Offline/physical transfer** (AWS Data Transfer Terminal / Snow Family).
- ❌ **S3 Transfer Acceleration** — still bound by the slow 100 Mbps Internet line · Direct Connect (weeks to provision) · direct upload.

> [!TIP]
> **Exam tip:** **TB-scale over a slow/constrained line = offline transfer** (Snow / Data Transfer Terminal). Transfer Acceleration optimizes the Internet path but doesn't beat physical for huge datasets.
> 📇 [Card: Snow Family](../cards/16-dr-migration/04-snow-family.md)

---

# 🟡 3. Design Secure Architectures (30%)

## 3.1 SSO with a corporate directory → IAM Identity Center + AD Connector · *(Select TWO)*

**Sample question (Q26, Q41):** *"Multi-account org needs centralized authentication using the existing corporate directory."*

- ✅ **IAM Identity Center integrated with the corporate directory** (via AD Connector) + **AWS Organizations** (+ SCP).
- ❌ Directory Service "directly" as the org auth · Cognito identity pool · CloudTrail.

> [!TIP]
> **Exam tip:** **centralized SSO over an existing corporate directory** = **IAM Identity Center + AD Connector**, governed by **Organizations + SCP**.
> 📇 [Card: Identity Center](../cards/13-iam-advanced/05-identity-center.md) · [Organizations & SCPs](../cards/13-iam-advanced/03-organizations-scps.md)

## 3.2 Provision accounts with preapproved baselines → Control Tower

**Sample question (Q62):** *"Streamline creating accounts in an Organization with preapproved configs/guardrails — least effort."*

- ✅ **AWS Control Tower Landing Zone** + pre-packaged guardrails.
- ❌ AWS RAM (resource sharing) · Systems Manager OpsCenter · Config aggregator.

> [!TIP]
> **Exam tip:** **new accounts with baselines/guardrails, least effort** → **Control Tower**. RAM shares resources; it doesn't provision governed accounts.
> 📇 [Card: Organizations & SCPs](../cards/13-iam-advanced/03-organizations-scps.md)

## 3.3 Private access to DynamoDB → VPC gateway endpoint

**Sample question (Q50):** *"Fargate app using DynamoDB; private access from the VPC, least overhead, cross-account DR."*

- ✅ **DynamoDB gateway endpoint** (like S3) + **AWS Backup** cross-account for DR.
- ❌ A NACL rule allowing outbound to `dynamodb.amazonaws.com` · interface endpoint · Network Firewall.

> [!TIP]
> **Exam tip:** **private VPC access to DynamoDB or S3 = gateway endpoint** (free, route-table based). Other services use interface endpoints (PrivateLink).
> 📇 [Card: VPC Endpoints](../cards/15-vpc/04-vpc-endpoints.md)

## 3.4 SSE-S3 / SSE-KMS request header

**Sample question (Q63):** *"S3 bucket uses SSE-S3 (AES-256). Which request header must be used?"*

- ✅ `x-amz-server-side-encryption`
- ❌ `x-amz-server-side-encryption-customer-algorithm` (and the other `-customer-*` headers) — those are for **SSE-C** (customer-provided keys).

> [!TIP]
> **Exam tip:** **SSE-S3 / SSE-KMS** → `x-amz-server-side-encryption`. The `-customer-*` headers belong to **SSE-C** only.
> 📇 [Card: S3 Encryption](../cards/06-s3-avanzado/02-s3-encryption.md)

---

# 🟢 4. Design High-Performing Architectures (24%)

## 4.1 Clients need a static IP to whitelist → NLB

**Sample question (Q32):** *"Public APIs on EC2 behind an ELB; on-prem clients can only reach trusted IPs whitelisted on their firewalls."*

- ✅ Associate an **Elastic IP to a Network Load Balancer** (NLB gives static IPs).
- ❌ EIP to an **ALB** (no static IP) · SSD volumes · CloudFront to private IPs.

> [!TIP]
> **Exam tip:** **clients need a fixed/static IP to whitelist** → **NLB**. ALB has no static IP.
> 📇 [Card: NLB & GWLB](../cards/03-elb-asg/03-nlb-glb.md)

## 4.2 Cheap global static content → CloudFront + S3

**Sample question (Q56):** *"Deliver static content globally with low latency, reduce server costs (Select TWO)."*

- ✅ **CloudFront + S3**.
- ❌ **Global Accelerator** (for non-HTTP/TCP-UDP app acceleration, not cacheable static content) · Fargate · Lambda.

> [!TIP]
> **Exam tip:** **cacheable static content globally** → **CloudFront + S3**. Global Accelerator is for TCP/UDP app traffic, not static caching.
> 📇 [Card: Global Accelerator](../cards/07-cdn/04-global-accelerator.md)

## 4.3 IPv4 exhaustion + future scale → IPv6-only subnet

**Sample question (Q57):** *"VPC with IPv4 nearing exhaustion; no free IPs on the subnet; need scalability."*

- ✅ Create a **new IPv6-only subnet** with a large CIDR.
- ❌ New IPv4 subnet with a larger CIDR (kicks the can) · remove IPv4 entirely · disable IPv4 support.

> [!TIP]
> **Exam tip:** **IPv4 exhaustion + scale** → **IPv6-only subnet** (effectively unlimited address space).
> 📇 [Card: Flow Logs & IPv6](../cards/15-vpc/08-flow-logs-ipv6.md)

## 4.4 Route 53 to an S3 static website — prerequisites · *(Select TWO)*

**Sample question (Q21):** *"Route traffic with Route 53 to a website hosted in an S3 bucket — prerequisites?"*

- ✅ The **bucket name must equal the domain name**, and a **registered domain name**.
- ❌ Record type "MX" · bucket in the same region as the hosted zone (Route 53 is global) · CORS.

> [!TIP]
> **Exam tip:** **S3 static site + Route 53** → **bucket name = domain name** + registered domain. No same-region rule (Route 53 is global).
> 📇 [Card: Records, Alias & TTL](../cards/05-route53/01-records-alias-ttl.md)

## 4.5 API Gateway key features · *(Select TWO)*

**Sample question (Q27):** *"Key features of API Gateway to highlight to a client."*

- ✅ **Pay only for API calls + data transferred out**, and **build RESTful + WebSocket APIs** for serverless.
- ❌ "Query language like GraphQL" — that's **AppSync** · static anycast IPs (Global Accelerator) · OS-bypass HPC.

> [!TIP]
> **Exam tip:** API Gateway = **REST + WebSocket + pay-per-use**. **GraphQL = AppSync**, not API Gateway.
> 📇 [Card: API Gateway](../cards/10-serverless/04-api-gateway.md)

## 4.6 Process Kinesis records to S3 → KDS + Lambda

**Sample question (Q59):** *"Upload → Kinesis Data Streams for processing → S3, async, cost-effective."*

- ✅ **Kinesis Data Streams + Lambda consumers** to process and write to S3.
- ❌ KDS → **Firehose** → S3 (adds a service when records need custom processing) · SQS + EC2 · Step Functions.

> [!TIP]
> **Exam tip:** **process KDS records then store** → **Lambda consumers**. Firehose = direct delivery without custom processing.
> 📇 [Card: Kinesis](../cards/08-decoupling/04-kinesis.md)

## 4.7 Key-value store with provisioned capacity → DynamoDB

**Sample question (Q64):** *"Key-value store, provisioned capacity mode, document models; web tier on ECS Fargate."*

- ✅ **DynamoDB table**.
- ❌ **Aurora Serverless** (relational) · WorkDocs · RDS with read replicas.

> [!TIP]
> **Exam tip:** **"key-value store"** → **DynamoDB**. Aurora is relational, never the answer for key-value.
> 📇 [Card: DynamoDB](../cards/11-bd-data-ml/01-dynamodb.md)

## 4.8 Monitor DB metrics + email alerts → CloudWatch + SNS · *(Select TWO)*

**Sample question (Q36):** *"Monitor certain database metrics and send email notifications to the Operations team."*

- ✅ **Amazon CloudWatch** (alarm) + **Amazon SNS** (email subscription).
- ❌ **SES** (transactional/marketing email, not alarms) · SQS · EC2 + BIND.

> [!TIP]
> **Exam tip:** **monitoring + email alert** = **CloudWatch + SNS**. SES sends application email, not operational alerts.
> 📇 [Card: CloudWatch](../cards/12-monitoring/01-cloudwatch.md)

---

# Patterns to watch

- **Multi-select misses (Q19, Q21, Q27, Q30, Q36, Q41):** you got one right and picked **one plausible distractor**. Validate **each** marked option on its own before moving on.
- **Cost-Optimized has no card block** — biggest content gap; it cost you 5 questions here.
- **Resilient still chronic** (47%, worst in both tests) — Multi-AZ, networking failover, DR connectivity.

---

# Summary — what to memorize

| Common confusion | Correct answer |
|---|---|
| Multi-AZ failover behavior | **CNAME/DNS** repointed to standby (not IP) |
| Failover of a private IP | **Secondary ENI** (not Elastic IP) |
| Direct Connect resilience | **2nd DX** or **backup VPN**, same VPC |
| Automate EBS snapshots, simple | **Data Lifecycle Manager** |
| Continuous DB migration | **DMS full load + CDC** (+SSL via CA cert) |
| Elasticity for EC2 | **ELB + Route 53 weighted** (not Glue) |
| Bias traffic by geography | **Geoproximity** (Geolocation = by user location) |
| Track cost by department | **Cost Allocation Tags** (Budgets = alerts) |
| Archive on-prem data | **DataSync direct to Glacier Deep Archive** |
| TB over a slow line | **Offline transfer** (Snow / Data Transfer Terminal) |
| SSO over corporate directory | **IAM Identity Center + AD Connector** (+ Organizations/SCP) |
| Accounts with baselines, least effort | **Control Tower** (not RAM) |
| Private DynamoDB/S3 access | **Gateway endpoint** |
| SSE-S3 / SSE-KMS header | `x-amz-server-side-encryption` (`-customer-*` = SSE-C) |
| Clients need static IP | **NLB** (not ALB) |
| Cheap global static content | **CloudFront + S3** (not Global Accelerator) |
| IPv4 exhaustion + scale | **IPv6-only subnet** |
| S3 static site + Route 53 | **bucket name = domain** + registered domain |
| API Gateway vs GraphQL | API GW = REST/WebSocket; **GraphQL = AppSync** |
| Process Kinesis records | **KDS + Lambda** (Firehose = direct delivery) |
| Key-value store | **DynamoDB** (not Aurora) |
| Monitor + email alert | **CloudWatch + SNS** (not SES) |

---

[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/SAA-175074?style=for-the-badge)](../README.md)
