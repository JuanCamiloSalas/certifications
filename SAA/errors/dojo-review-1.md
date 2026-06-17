[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/SAA-175074?style=for-the-badge)](../README.md)

# SAA Practice Test 1 — Weak Points

**Result:** 70% (46/65) — Failed (exceeded standard time; within limit with +30 min ESL). 2026-06-15.

| Domain | AWS Weight | Score | Error impact (W × err%) | Priority |
|---|---|---|---|---|
| **Design Resilient Architectures** | 26% | 53% | **12.2** | 🔴 HIGHEST |
| **Design High-Performing Architectures** | 24% | 65% | 8.4 | 🟡 Medium |
| **Design Secure Architectures** | 30% | 90% | 3.0 | 🟢 Low |
| **Design Cost-Optimized Architectures** | 20% | 100% | 0 | 🟢 None |

> [!IMPORTANT]
> Ordered by **highest weight × lowest score**. TutorialsDojo also reported a small "Secure Applications" bucket (50%, 2 q) — its misses are folded into Secure below.

---

# 🔴 1. Design Resilient Architectures (26%)

## 1.1 RDS HA across AZs → Multi-AZ (not Read Replica)

**Sample question (Q54, Q63):** *"An RDS database loses access during AZ outages — improve HA / replicate synchronously, same region."*

| Option | Verdict |
|---|---|
| **Multi-AZ deployment** | ✅ synchronous standby + automatic failover |
| Read Replica | ❌ asynchronous, read-only, manual promotion |
| Increase instance size | ❌ does not address AZ failure |

> [!TIP]
> **Exam tip:** the words **"synchronous"** or **"automatic failover"** = **Multi-AZ**. Read Replicas scale *reads* (async) and never auto-failover. On failover, the **CNAME/DNS endpoint** is repointed to the standby — the client endpoint is stable.
> 📇 [Card: RDS](../cards/04-rds-aurora/01-rds.md)

## 1.2 Cross-region DR with strict RPO/RTO → Aurora Global Database

**Sample question (Q45):** *"Relational DB needs RPO ≈ 1 s, RTO < 1 min, automatic cross-region failover (beyond Multi-AZ)."*

- ✅ **Aurora Global Database** — automated cross-region replication, failover < 1 min.
- ❌ **RDS cross-region read replicas** — replicate cross-region but need **manual promotion** → RTO far above 1 min.

> [!TIP]
> **Exam tip:** **cross-region + RPO ~seconds + RTO < 1 min** → **Aurora Global Database**. Multi-AZ is single-region; cross-region read replicas are manual.
> 📇 [Card: Aurora Advanced](../cards/04-rds-aurora/04-aurora-advanced.md)

## 1.3 ASG minimum capacity for HA → N × number of AZs

**Sample question (Q1):** *"App needs ≥ 2 instances in normal load (up to 6 at peak), highly available and fault-tolerant."*

- ✅ **min = 4** (2 per AZ across 2 AZs) → one AZ failure still leaves the **2** required.
- ❌ **min = 2** (1 per AZ) → losing one AZ drops you to **1**, below the minimum.

> [!TIP]
> **Exam tip:** if the app needs **N** instances to function, set ASG **min = N × number of AZs**. Don't read "needs 2" as "min = 2" when HA is required.
> 📇 [Card: Auto Scaling Group](../cards/03-elb-asg/05-asg.md)

## 1.4 ASG default termination policy

**Sample question (Q24):** *"ASG with default settings, scale-in triggered — which instance is terminated first?"*

- ✅ AZ with the **most instances** → within it, the one from the **oldest launch template/config**.
- ❌ Random / longest-running.

> [!TIP]
> **Exam tip:** default termination = **balance AZs first, then oldest launch template**. It is deterministic, not random.
> 📇 [Card: Auto Scaling Group](../cards/03-elb-asg/05-asg.md)

## 1.5 React to an Aurora row change → native Lambda invoke

**Sample question (Q11):** *"Aurora MySQL — when a row is deleted, trigger a distributed processing workflow."*

- ✅ **Aurora native Lambda invoke** (`lambda_sync` / `lambda_async`).
- ❌ **RDS event subscriptions** — fire on **instance** events (failover, backup, maintenance), never on row-level data changes.

> [!TIP]
> **Exam tip:** **row-level data change in Aurora** → native Lambda function. RDS event subscriptions ≠ data triggers.
> 📇 [Card: Aurora Advanced](../cards/04-rds-aurora/04-aurora-advanced.md)

## 1.6 Homogeneous migration of app + DB → DMS + Elastic Beanstalk

**Sample question (Q46):** *"Migrate a .NET app (Windows Server) + Oracle backend to AWS with minimal refactoring."*

- ✅ **AWS DMS** for Oracle → RDS for Oracle (homogeneous DB migration).
- ✅ **Elastic Beanstalk** for the .NET app (managed Windows platform).
- ❌ ECS/containers or AWS MGN — more refactoring than needed when the source maps to managed targets.

> [!TIP]
> **Exam tip:** **DB migration = DMS**; **app re-host with minimal change = Elastic Beanstalk**. Split the two halves of the workload.
> 📇 [Card: DMS & SCT](../cards/16-dr-migration/02-dms-sct.md)

## 1.7 Hybrid file access + archiving → Storage Gateway File Gateway

**Sample question (Q55):** *"Hybrid company — on-prem docs need immediate access + cost-effective archiving of older data."*

- ✅ **Storage Gateway File Gateway** (caches hot files on-prem) **+ S3 lifecycle to Glacier**.
- ❌ DataSync or direct S3 upload — no local cache for immediate access.

> [!TIP]
> **Exam tip:** **immediate on-prem file access + tier-to-Glacier** → **File Gateway + lifecycle**. DataSync = one-off/scheduled transfer, no cache.
> 📇 [Card: Storage Gateway](../cards/16-dr-migration/05-storage-gateway.md)

---

# 🟡 2. Design High-Performing Architectures (24%)

## 2.1 Aurora endpoints — cluster / reader / custom

**Sample question (Q47):** *"Route production traffic to high-capacity Aurora instances and reporting queries to low-capacity ones."*

| Endpoint | Use |
|---|---|
| **Cluster** | the primary **writer** |
| **Reader** | load-balances across **all** readers |
| **Custom** | a **subset you define** (route by size / workload) |

> [!TIP]
> **Exam tip:** to split traffic by instance group, use **custom endpoints**. Instance/cluster endpoints are the wrong tool for workload routing.
> 📇 [Card: Aurora](../cards/04-rds-aurora/03-aurora.md)

## 2.2 DynamoDB partition key → high cardinality

**Sample question (Q9):** *"DynamoDB WCUs are consumed unevenly due to poor key distribution — fix the partition key."*

- ✅ **High-cardinality** partition key (many distinct values) → writes spread across partitions.
- ❌ Low-cardinality key → **hot partitions** → uneven WCU consumption.

> [!TIP]
> **Exam tip:** **uneven throughput / hot partition** → choose a **high-cardinality** partition key.
> 📇 [Card: DynamoDB](../cards/11-bd-data-ml/01-dynamodb.md)

## 2.3 React to item-level changes → DynamoDB Streams + Lambda

**Sample question (Q19):** *"App on DynamoDB must react to data changes (follow/notification feature)."*

- ✅ **DynamoDB Streams + Lambda** — captures INSERT / MODIFY / REMOVE in order.
- ❌ Kinesis or SNS for table change-data.

> [!TIP]
> **Exam tip:** **react to DynamoDB data changes** → **Streams + Lambda** (the native CDC pattern).
> 📇 [Card: DynamoDB Advanced](../cards/11-bd-data-ml/02-dynamodb-advanced.md)

## 2.4 CloudFront 504 errors → raise cache hit ratio

**Sample question (Q12):** *"Static site behind CloudFront returns HTTP 504 under millions of requests."*

- ✅ Raise the **cache hit ratio** (Cache-Control `max-age` at the origin) → fewer origin hits.
- ❌ Multi-region routing or Lambda@Edge — don't fix an overloaded origin.

> [!TIP]
> **Exam tip:** **CloudFront 504** = origin overloaded/timing out → **increase caching at the origin**.
> 📇 [Card: CloudFront](../cards/07-cdn/01-cloudfront.md)

## 2.5 API Gateway zero-downtime deploy → canary release

**Sample question (Q20):** *"Deploy a new API version on API Gateway with zero downtime."*

- ✅ **Canary release** — stage variables + shift a % of traffic to the new stage, validate, cut over.
- ❌ Editing the live stage in place.

> [!TIP]
> **Exam tip:** **zero-downtime API deploy** → **canary release / stage traffic shifting**.
> 📇 [Card: API Gateway](../cards/10-serverless/04-api-gateway.md)

## 2.6 Hot + cold storage for ML → FSx for Lustre + S3

**Sample question (Q29):** *"ML training needs high-performance parallel hot storage + cost-effective cold archive."*

- ✅ **FSx for Lustre** (parallel hot) **+ S3** (cold/archive; Lustre integrates natively with S3).
- ❌ FSx for Lustre + **EBS io1** — EBS is per-instance block, no archive tier.

> [!TIP]
> **Exam tip:** **parallel hot = FSx for Lustre**; **cold/archive = S3** (not EBS).
> 📇 [Card: FSx](../cards/02-storage-ec2/07-fsx.md)

## 2.7 EC2 custom CloudWatch metrics → memory & disk need the agent

**Sample question (Q36):** *"Which EC2 CloudWatch metric requires manual/custom setup?"*

- ✅ **Memory utilization** and **disk space** — OS-level, need the **CloudWatch Agent**.
- ❌ CPUUtilization, NetworkIn/Out, NetworkPackets, DiskReadOps/WriteOps — standard, no agent.

> [!TIP]
> **Exam tip:** **memory + disk space = custom (agent)**. Anything the hypervisor sees (CPU, network, disk ops) is standard.
> 📇 [Card: CloudWatch](../cards/12-monitoring/01-cloudwatch.md)

## 2.8 Multi-account data lake → Lake Formation

**Sample question (Q53):** *"Multi-account S3 data lake — query centrally with role-based access control."*

- ✅ **AWS Lake Formation** — lake permissions, cross-account sharing, column/row-level access.
- ❌ **AWS Control Tower** — account governance/guardrails, not data permissions.

> [!TIP]
> **Exam tip:** **data-lake permissions / role-based data access** → **Lake Formation**. Control Tower governs *accounts*, not *data*.
> 📇 Card: _none yet_

---

# 🟢 3. Design Secure Architectures (30%)

## 3.1 RDS access via instance role token → IAM DB Authentication

**Sample question (Q25):** *"RDS must be accessed only via auth tokens derived from the EC2 instance's IAM profile."*

- ✅ Enable **IAM DB Authentication** (short-lived tokens via the role; STS under the hood).
- ❌ "Use IAM + STS for a temp token" — describes the mechanism, not the feature name.

> [!TIP]
> **Exam tip:** **"authentication token from instance profile credentials"** → **IAM DB Authentication**.
> 📇 [Card: RDS](../cards/04-rds-aurora/01-rds.md)

## 3.2 Encrypt EKS etcd secrets → envelope encryption with KMS

**Sample question (Q26):** *"EKS cluster — encrypt sensitive data stored in the cluster's etcd key-value store."*

- ✅ Enable **envelope encryption on the EKS cluster** using a **KMS key**.
- ❌ Secrets Manager — stores secrets externally; does not encrypt the etcd store itself.

> [!TIP]
> **Exam tip:** **encrypt the etcd store** → **EKS envelope encryption + KMS**, not Secrets Manager.
> 📇 [Card: EKS](../cards/09-containers/03-eks.md)

## 3.3 Existing on-prem AD → AD Connector (not Simple AD) · *(Select TWO)*

**Sample question (Q51):** *"Federate an existing corporate Active Directory to the AWS Console; roles already in corporate AD."*

- ✅ **AD Connector** — proxies auth to the existing AD (no sync, no migration).
- ❌ **Simple AD** — standalone managed directory with **no** link to on-prem AD.

> [!TIP]
> **Exam tip:** **existing on-prem AD** → **AD Connector**. Simple AD is a fresh standalone directory.
> 📇 [Card: Identity Center](../cards/13-iam-advanced/05-identity-center.md)

## 3.4 Federation to S3 with per-user folders → IAM Role + Policy · *(Select TWO)*

**Sample question (Q6):** *"SSO from corporate AD/LDAP to S3 with per-user folder restriction."*

- ✅ **Identity provider + STS** (temp tokens) **and IAM Role + IAM Policy** (grants the actual access).
- ❌ 3rd-party SSO (OKTA, Atlassian) as a replacement for the IAM Role/Policy.

> [!TIP]
> **Exam tip:** federation always needs the **IAM Role + Policy** to grant resource access; the IdP only handles identity.
> 📇 [Card: Federation](../cards/13-iam-advanced/02-federation.md)

---

# 🟢 4. Design Cost-Optimized Architectures (20%)

100% on this test — nothing to review.

---

# Confirmed (right but flagged as unsure)

Quick reinforcement — skim only.

| # | Concept | Key point |
|---|---|---|
| Q3 | KMS custom key store | Key material in your CloudHSM → immediate deletion + audit independent of CloudTrail |
| Q13 | RDS Enhanced Monitoring | Per-process CPU/memory inside RDS; plain CloudWatch = hypervisor-level only |
| Q15 | S3 Object Lock modes | Compliance + retention = immutable even for root; Governance = admins override; Legal hold = no fixed period |
| Q21 | EventBridge → ECS | S3 PUT rule can target the ECS cluster directly (no Lambda) |
| Q27 | CloudWatch Agent | EC2 memory/disk via agent (not RDS Enhanced Monitoring) |
| Q28 | Egress-Only IGW | IPv6 outbound from private subnet; pair with Network Firewall for inspection |
| Q33 | ElastiCache Redis AUTH | Needs `--transit-encryption-enabled` AND `--auth-token` at creation |
| Q38 | FSx for NetApp ONTAP | Windows + HA across AZs + iSCSI block (Windows File Server = SMB only) |
| Q41 | Lambda for bursts | Burst-in-seconds + global → API Gateway + Lambda (ms scaling) |
| Q43 | API Gateway throttling | Protects backend from spikes beyond NACL filtering |
| Q48 | Kinesis + Lambda | Real-time PII ingest → anonymize inline → DynamoDB |
| Q64 | S3 Object Lock + Access Point | WORM (Legal Hold) + VPC-only access |
| Q65 | Lambda env var encryption | KMS encryption helpers (your key) so devs can't read plaintext |

---

# Summary — what to memorize

| Common confusion | Correct answer |
|---|---|
| "synchronous" / "automatic failover" | **Multi-AZ** (not Read Replica) |
| Cross-region RPO~1s + RTO<1min | **Aurora Global Database** |
| App needs N instances + HA | ASG **min = N × AZs** |
| ASG default termination | AZ with most instances → **oldest launch template** |
| React to an Aurora row change | **Aurora native Lambda invoke** (not RDS event subscription) |
| Migrate app + DB, minimal refactor | **DMS** (DB) + **Elastic Beanstalk** (app) |
| On-prem file access + archive | **Storage Gateway File Gateway** + S3 lifecycle |
| Aurora workload routing | **Custom endpoints** |
| DynamoDB uneven WCU | **High-cardinality** partition key |
| React to DynamoDB changes | **Streams + Lambda** |
| CloudFront 504 | Raise **cache hit ratio** at origin |
| Zero-downtime API deploy | **Canary release** |
| ML hot + cold storage | **FSx for Lustre + S3** (not EBS) |
| EC2 memory/disk metrics | **CloudWatch Agent** (custom) |
| Multi-account data-lake access | **Lake Formation** (not Control Tower) |
| Token from instance IAM profile | **IAM DB Authentication** |
| Encrypt EKS etcd | **Envelope encryption + KMS** |
| Existing on-prem AD | **AD Connector** (not Simple AD) |
| Federation to S3 | **IAM Role + Policy** (IdP only handles identity) |

---

[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/SAA-175074?style=for-the-badge)](../README.md)
