[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/SAA-175074?style=for-the-badge)](../README.md)

# SAA Practice Test 3 — Weak Points

**Result:** 66% (43/65) — Failed (72% required). 2026-06-19.

| Domain | AWS Weight | Score | Error impact (W × err%) | Priority |
|---|---|---|---|---|
| **Design Resilient Architectures** | 26% | 56% | **11.4** | 🔴 HIGHEST |
| **Design Secure Architectures** | 30% | 65% | 10.5 | 🟡 High |
| **Design Cost-Optimized Architectures** | 20% | 56% | 8.8 | 🟡 Medium |
| **Design High-Performing Architectures** | 24% | 81% | 4.6 | 🟢 Low |

> [!IMPORTANT]
> Ordered by **highest weight × lowest score**. Networking/VPC dominates the Resilient & Secure misses — and **Route 53 + Direct Connect repeat from Test 2** (chronic). Cost stays low and has no study material in the repo.

---

# 🔴 1. Design Resilient Architectures (26%)

## 1.1 VPC subnets & CIDR fundamentals · *(Select TWO)*

**Sample question (Q21):** *"Which statements about VPC subnets are true?"*

- ✅ Each subnet maps to a **single AZ**; each new subnet is **auto-associated to the main route table**.
- ❌ "block size between /16 and **/27**" — the VPC range is **/16 to /28**.

> [!TIP]
> **Exam tip:** subnet = **1 AZ**. VPC CIDR range is **/16 (65,536 IPs) → /28 (16 IPs)**. New subnets attach to the main route table by default.
> 📇 [Card: VPC Foundations](../cards/15-vpc/01-vpc-foundations.md)

## 1.2 EC2 unreachable from the Internet · *(Select TWO)*

**Sample question (Q39):** *"EC2 in a new subnet of an Internet-connected VPC can't be reached from the Internet — why?"*

- ✅ No **public IP** associated; the **route table** isn't sending traffic to the **Internet Gateway**.
- ❌ Not in the same ASG · no Elastic Fabric Adapter (EFA is HPC networking, irrelevant).

> [!TIP]
> **Exam tip:** public reachability needs **public IP + route table → IGW + SG/NACL allow**. A new subnet doesn't inherit a route to the IGW automatically.
> 📇 [Card: VPC Foundations](../cards/15-vpc/01-vpc-foundations.md)

## 1.3 Fault-tolerant Route 53 (all active, drop unhealthy) → Active-Active + Weighted

**Sample question (Q28):** *"Multi-region, all resources available, Route 53 drops a resource when unhealthy. Most fault-tolerant config?"*

- ✅ **Active-Active failover with a Weighted routing policy**.
- ❌ Active-Passive (keeps a standby idle) · Active-Passive weighted.

> [!TIP]
> **Exam tip:** **all resources serving + auto-drop unhealthy** = **Active-Active** (weighted/multivalue). Active-Passive keeps the secondary idle until failover. *(Route 53 also missed in Test 2 — chronic.)*
> 📇 [Card: Routing Policies 1](../cards/05-route53/02-routing-policies-1.md)

## 1.4 Direct Connect to multiple accounts → DX Gateway + Transit Gateway

**Sample question (Q43):** *"On-prem core services (DNS/AD) over DX; new AWS accounts need consistent dedicated access. Least overhead?"*

- ✅ **Direct Connect gateway + Transit Gateway** between accounts.
- ❌ DX gateway + **VPC peering** (peering isn't transitive) · one DX per account · VPN CloudHub.

> [!TIP]
> **Exam tip:** **DX shared across many accounts/VPCs** = **DX Gateway + Transit Gateway**. VPC peering doesn't scale (no transitivity). *(Direct Connect also missed in Test 2 — chronic.)*
> 📇 [Card: Direct Connect](../cards/15-vpc/07-direct-connect.md)

## 1.5 RDS running out of disk → storage autoscaling

**Sample question (Q27):** *"Production MySQL RDS out of disk; add space without impacting performance, least overhead."*

- ✅ **Enable RDS storage autoscaling**.
- ❌ Increase allocated storage manually · Provisioned IOPS · change storage engine to MyISAM.

> [!TIP]
> **Exam tip:** **grow RDS disk with least effort** = **storage autoscaling** (grows automatically up to a max).
> 📇 [Card: RDS](../cards/04-rds-aurora/01-rds.md)

## 1.6 Migrate to Aurora Serverless with minimal downtime → DMS

**Sample question (Q46):** *"Move an Aurora cluster to Aurora Serverless minimizing downtime."*

- ✅ **AWS DMS** to migrate to a new Aurora Serverless database.
- ❌ Change the instance class to Serverless (not an in-place toggle) · snapshot/restore (more downtime).

> [!TIP]
> **Exam tip:** **migrate with minimal downtime = DMS**. *(DMS is the migration answer in Tests 1, 2 and 3 — chronic.)*
> 📇 [Card: DMS & SCT](../cards/16-dr-migration/02-dms-sct.md)

## 1.7 RDS backup retention > 35 days → AWS Backup

**Sample question (Q61):** *"Implement a 90-day RDS backup retention policy."*

- ✅ **AWS Backup plan** with daily snapshots, 90-day retention.
- ❌ Automated backups set to 90 days — **automated backup max is 35 days**.

> [!TIP]
> **Exam tip:** RDS **automated backups cap at 35 days**. For longer retention → **AWS Backup** (or manual snapshots).
> 📇 [Card: RDS](../cards/04-rds-aurora/01-rds.md)

## 1.8 Instance store + stop/start behavior · *(Select TWO)*

**Sample question (Q55):** *"EC2 with instance-store volumes + Elastic IP is stopped/started — what happens?"*

- ✅ The **underlying host may change**; **all instance-store data is lost**.
- ❌ "Elastic IP is disassociated" (EIP stays associated while stopped) · ENI detached.

> [!TIP]
> **Exam tip:** stop/start = **new host + instance-store wiped**. EBS persists; **instance store does not**. EIP stays attached.
> 📇 [Card: Instance Store](../cards/02-storage-ec2/06-instance-store.md)

## 1.9 CloudFormation success signal → CreationPolicy + cfn-signal

**Sample question (Q65):** *"Ensure apps are installed/running before the CFN stack creation proceeds."*

- ✅ **CreationPolicy** attribute + send a success signal via **cfn-signal**.
- ❌ DependsOn + cfn-init · UpdatePolicy · UpdateReplacePolicy.

> [!TIP]
> **Exam tip:** **wait for app readiness before CFN continues** = **CreationPolicy + cfn-signal**. DependsOn only orders resource creation, not app readiness.
> 📇 Card: _none yet (no CloudFormation block)_

---

# 🟡 2. Design Secure Architectures (30%)

## 2.1 Cross-account S3 access → bucket policy + IAM policy

**Sample question (Q1):** *"Grant another account access to copy objects across S3 buckets (multi-account org)."*

- ✅ Configure permissions with an **S3 bucket policy + a customer-managed IAM policy**.
- ❌ Approaches relying only on ACLs / WorkDocs / replication for access control.

> [!TIP]
> **Exam tip:** **cross-account S3 access = bucket policy (resource side) + IAM policy (principal side)**.
> 📇 [Card: Roles & STS](../cards/13-iam-advanced/01-roles-sts.md)

## 2.2 KMS decrypt for Lambda → grant the execution role in the key policy

**Sample question (Q8):** *"Lambda must decrypt S3 objects encrypted with a KMS customer key."*

- ✅ Attach **kms:decrypt** to the Lambda **execution role** + a statement in the **KMS key policy granting that execution role**.
- ❌ Granting the function's **ARN** in the key policy · using the resource policy.

> [!TIP]
> **Exam tip:** KMS access = **IAM role permission + key policy grant to the role** (the principal is the role, not the function ARN).
> 📇 [Card: KMS](../cards/14-security/01-kms.md)

## 2.3 Change permissions for many users → IAM Group

**Sample question (Q13):** *"Change permissions for 100 IAM users without applying the policy to each."*

- ✅ Create an **IAM Group**, add the users, attach the policy to the group.
- ❌ EventBridge Scheduler to apply per-user · add users to an IAM role.

> [!TIP]
> **Exam tip:** **manage permissions for many users = IAM Group**. (Roles are assumed, not for static human-user grouping.)
> 📇 [Card: Roles & STS](../cards/13-iam-advanced/01-roles-sts.md)

## 2.4 NACL is stateless → open ephemeral ports outbound · *(Select TWO)*

**Sample question (Q52):** *"Default-deny NACL; allow inbound 443 from any source."*

- ✅ **SG**: allow inbound 443 from `0.0.0.0/0`. **NACL**: allow inbound 443 **and** outbound **ephemeral 32768–65535**.
- ❌ NACL allowing only 443 both ways — NACL is **stateless**, the response goes out on an ephemeral port.

> [!TIP]
> **Exam tip:** **SG = stateful** (return traffic automatic). **NACL = stateless** → must allow the **ephemeral port range (1024–65535 / 32768–65535)** outbound for responses.
> 📇 [Card: SG & NACL](../cards/15-vpc/02-sg-nacl.md)

## 2.5 Private content via CloudFront → signed URLs/cookies + OAC · *(Select TWO)*

**Sample question (Q53):** *"Serve private S3 content via CloudFront only; block direct S3 URLs."*

- ✅ **CloudFront signed URLs/cookies** + **Origin Access Control (OAC)** so only CloudFront can read the bucket.
- ❌ S3 presigned URL (that's the S3 path, not CloudFront-only) · CloudFront function · Origin Shield.

> [!TIP]
> **Exam tip:** **restrict to CloudFront-only** = **OAC** (locks the origin) + **signed URLs/cookies** (controls who can request). Presigned URLs are the S3-direct mechanism.
> 📇 [Card: CloudFront Security](../cards/07-cdn/02-cloudfront-security.md)

---

# 🟡 3. Design Cost-Optimized Architectures (20%)

> [!NOTE]
> Still **no billing/cost card block** in the repo — 3 of these 4 have no card to review. Biggest content gap.

## 3.1 EC2 billing per instance state · *(Select TWO)*

**Sample question (Q6):** *"Which statements about EC2 billing are true?"*

- ✅ Billed when a **Reserved Instance is in `terminated`** state (you pay for the reservation regardless); billed when an **On-Demand instance is preparing to hibernate** (`stopping`).
- ❌ Spot preparing to stop (`stopping`) is billed.

> [!TIP]
> **Exam tip:** stopped instances aren't billed for compute (only EBS); **RIs are billed for the term no matter what**; hibernating On-Demand is billed during `stopping`.
> 📇 [Card: Instance Lifecycle](../cards/01-ec2-saa/02-instance-lifecycle.md)

## 3.2 Programmatic cost reports → Cost Explorer API

**Sample question (Q10):** *"Programmatically access and forecast usage costs, least operational overhead."*

- ✅ **AWS Cost Explorer API** (with pagination).
- ❌ Budgets + SNS/SQS · downloadable CSV reports.

> [!TIP]
> **Exam tip:** **programmatic cost data + forecast** = **Cost Explorer API**. Budgets = alerts; CUR = raw dataset.
> 📇 Card: _none yet (no billing block)_

## 3.3 Stop charges for decommissioned Reserved Instances · *(Select TWO)*

**Sample question (Q42):** *"Decommissioned Reserved EC2 instances — stop incurring charges ASAP, cost-effective."*

- ✅ **Terminate** the instances (stop on-demand billing once the reservation expires); **sell them on the AWS Reserved Instance Marketplace**.
- ❌ Just *stop* them (RI still billed) · sell on Amazon.com · cancel the AWS subscription.

> [!TIP]
> **Exam tip:** stopping doesn't end RI billing. **Terminate + sell on the RI Marketplace** to recover cost.
> 📇 Card: _none yet (no billing block)_

## 3.4 Glacier retrieval < 15 min + throughput → Expedited + provisioned capacity · *(Select TWO)*

**Sample question (Q60):** *"Glacier data must be retrievable in under 15 min anytime, up to 150 MB/s."*

- ✅ **Expedited Retrieval** + **purchase provisioned retrieval capacity** (guarantees Expedited throughput).
- ❌ Bulk (5–12 h) · Standard (3–5 h) · range retrieval.

> [!TIP]
> **Exam tip:** Glacier tiers — **Expedited (1–5 min)**, Standard (3–5 h), Bulk (5–12 h). For guaranteed Expedited capacity → **provisioned retrieval capacity**.
> 📇 [Card: S3 Lifecycle](../cards/06-s3-avanzado/01-lifecycle-replication.md)

---

# 🟢 4. Design High-Performing Architectures (24%)

## 4.1 DynamoDB performance → DAX + auto scaling · *(Select TWO)*

**Sample question (Q18):** *"Improve DynamoDB performance and scalability while keeping cost low."*

- ✅ **API Gateway + Lambda caching** on frequent reads + global replication; **DAX + auto scaling** with higher provisioned capacity.
- ❌ Assuming auto scaling is on by default · ElastiCache on the client device.

> [!TIP]
> **Exam tip:** microsecond reads → **DAX**; throughput → **auto scaling / higher capacity**. Auto scaling is **not** on by default for provisioned tables.
> 📇 [Card: DynamoDB Advanced](../cards/11-bd-data-ml/02-dynamodb-advanced.md)

## 4.2 Filter/transform an S3 object on read → S3 Object Lambda

**Sample question (Q19):** *"Return only filtered/transformed data from a large CSV without downloading the whole object."*

- ✅ **S3 Object Lambda** processing by **bucket name + object key**.
- ❌ Same but by object **metadata** / tags / name only.

> [!TIP]
> **Exam tip:** **transform data on GET** = **S3 Object Lambda** (keyed by bucket + object **key**).
> 📇 [Card: S3 Access Points](../cards/06-s3-avanzado/04-s3-access-points.md)

## 4.3 Faster EC2 boot without higher cost → hibernation

**Sample question (Q36):** *"Windows EC2 + FSx is stopped off-hours; takes minutes to be operational. Speed up loading without driving cost up."*

- ✅ Migrate to an **EC2 instance with hibernation enabled** (RAM saved to EBS, resumes fast).
- ❌ Enable hibernation on the existing instance (needs to be set at launch) · disable IMDS · migrate to Linux.

> [!TIP]
> **Exam tip:** **fast resume after stop** = **hibernation** (preserves RAM). Must be enabled at launch on a supported instance.
> 📇 [Card: Hibernation](../cards/01-ec2-saa/04-hibernation.md)

## 4.4 Many SSL domains on one ALB → SNI

**Sample question (Q51):** *"Serve SSL for many domains on one ALB without re-provisioning the cert each time you add a domain."*

- ✅ Upload all certs to the ALB and bind multiple certs to the same secure listener — **ALB picks the cert per client using SNI**.
- ❌ Wildcard cert (doesn't cover different root domains) · CloudFront dedicated IP · SAN cert (re-provision each time).

> [!TIP]
> **Exam tip:** **multiple distinct domains on one listener** = **SNI** (multiple certs). Wildcard only covers sub-domains of one domain.
> 📇 [Card: ALB](../cards/03-elb-asg/02-alb.md)

---

# Confirmed (right but flagged as unsure)

| # | Concept | Key point |
|---|---|---|
| Q7 | DDoS mitigation (not suitable) | Dedicated instances + EFA don't mitigate DDoS; CloudFront/Shield/WAF/ALB do |
| Q31 | Read records in batches | Kinesis Data Stream + Lambda (Firehose can't be "read" by consumers) |
| Q38 | Encrypted app config, cheap | SSM Parameter Store SecureString + KMS (cheaper than Secrets Manager) |
| Q48 | Analyze combined ELB logs | S3 (store) + EMR (analyze) |
| Q56 | On-prem backups via file protocols | Storage Gateway File Gateway → S3 |
| Q58 | Glue reprocessing old data | Enable the ETL **job bookmark** |
| Q62 | Lambda-in-VPC throttling | ENI/IP exhaustion in the subnet (EC2ThrottledException) |

---

# Summary — what to memorize

| Common confusion | Correct answer |
|---|---|
| VPC CIDR range | **/16 to /28**; subnet = 1 AZ; new subnet → main route table |
| EC2 unreachable from Internet | no public IP **or** route table missing IGW route |
| All-active + drop unhealthy | Route 53 **Active-Active + Weighted** |
| DX across many accounts | **DX Gateway + Transit Gateway** (not VPC peering) |
| Grow RDS disk, least effort | **storage autoscaling** |
| Migrate with min downtime | **DMS** |
| RDS retention > 35 days | **AWS Backup** (automated max = 35 d) |
| Stop/start instance store | new host + **data lost**; EIP stays |
| CFN wait for app readiness | **CreationPolicy + cfn-signal** |
| Cross-account S3 | **bucket policy + IAM policy** |
| KMS decrypt for Lambda | key policy grants the **execution role** |
| Permissions for many users | **IAM Group** |
| NACL (stateless) | allow **ephemeral ports** outbound |
| CloudFront-only private content | **OAC + signed URLs/cookies** |
| EC2 billing | RIs billed regardless; stopped = no compute charge |
| Programmatic cost + forecast | **Cost Explorer API** |
| Decommissioned RIs | **terminate + sell on RI Marketplace** |
| Glacier < 15 min + throughput | **Expedited + provisioned capacity** |
| DynamoDB perf | **DAX + auto scaling** (not on by default) |
| Transform S3 on read | **S3 Object Lambda** (by object key) |
| Fast EC2 resume | **hibernation** (set at launch) |
| Many SSL domains, one ALB | **SNI** (not wildcard) |

---

[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/SAA-175074?style=for-the-badge)](../README.md)
