[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)

# Master Error Doc — SAA Dojos

> Every wrong (or "guessed-right") Dojo answer goes here. One section per Dojo run.

## Entry format

```
[Main service] — [Key concept]
- Domain: (e.g., Design Secure Architectures)
- Question: (1-line summary)
- Trap: (what made me pick the wrong option)
- Rule: (1-2 lines I want to never forget)
```

---

## Dojo #1 — 2026-06-15 (Practice Test 1)

**Score:** 46 / 65 → 70% — Failed (time: 2h 31min; limit 2h 10min, +30min accommodation = 2h 40min → passed on time)

**Domain breakdown:**
- Design High-Performing Architectures (20 q): 65% ✗ 35%
- Design Secure Architectures (20 q): 90% ✗ 10%
- Design Cost-Optimized Architectures (3 q): 100% ✓
- Design Secure Applications and Architectures (2 q): 50% ✗ 50%
- Design Resilient Architectures (19 q): 53% ✗ 47%

---

### Errors

[EC2 / ASG] — HA minimum capacity with multiple AZs
- Domain: Design Resilient Architectures
- Question: ASG needs minimum 2 EC2 instances for normal load, up to 6 at peak; highly available + fault-tolerant
- Trap: Set min=2 with 2 AZs (1 per AZ) — "at least 2" seemed satisfied
- Rule: If the app needs N instances minimum to function, set ASG min to N × (number of AZs). With min=2 needed and 2 AZs → set min=4 (2 per AZ). One AZ failure still leaves the required 2 running.

---

[IAM / Federation] — Federation + S3 per-user folder access (multi-select)
- Domain: Design Secure Architectures
- Question: SSO from corporate AD/LDAP to S3 with per-user folder restriction (Select TWO)
- Trap: Selected "3rd party SSO (OKTA, Atlassian)" instead of "IAM Role + IAM Policy"
- Rule: Federation = Identity Provider + STS for temp tokens + IAM Role + IAM Policy. The IAM Role/Policy is always required to grant actual resource access. 3rd party SSO tools (OKTA etc.) don't replace IAM roles in AWS.

---

[DynamoDB] — Partition key cardinality and WCU distribution
- Domain: Design High-Performing Architectures
- Question: DynamoDB WCUs unevenly consumed due to poor key distribution — fix the partition key
- Trap: Chose low-cardinality partition keys (few distinct values)
- Rule: DynamoDB partition key must have HIGH cardinality (many distinct values) to spread writes evenly across partitions. Low cardinality = hot partitions = uneven WCU consumption.

---

[Aurora / Lambda] — Row-level triggers vs RDS event subscriptions
- Domain: Design Resilient Architectures
- Question: Aurora MySQL — when a row is deleted (vehicle sold), trigger a distributed processing workflow
- Trap: Used RDS event subscription → SNS → SQS; thought RDS events fire on data changes
- Rule: RDS/Aurora event subscriptions fire on INSTANCE-level events (failover, backup, maintenance), NOT row-level data changes. For row-level triggers in Aurora MySQL → Aurora native Lambda invoke function (lambda_sync / lambda_async).

---

[CloudFront] — 504 errors and cache hit ratio
- Domain: Design High-Performing Architectures
- Question: Static website behind CloudFront getting HTTP 504 errors under millions of requests
- Trap: Chose multi-region routing or Lambda@Edge instead of fixing the cache
- Rule: 504 on CloudFront = origin is timing out / overloaded. Fix = increase cache hit ratio via Cache-Control max-age at the origin. Fewer cache misses = fewer origin requests = fewer 504s.

---

[DynamoDB Streams] — Reacting to item-level data changes
- Domain: Design High-Performing Architectures
- Question: Social network app on DynamoDB — react to data changes for the follow/notification feature
- Trap: Chose Kinesis or SNS instead of DynamoDB Streams
- Rule: DynamoDB Streams captures item-level changes (INSERT, MODIFY, REMOVE) as an ordered stream. DynamoDB Streams + Lambda is the canonical pattern for reactive workflows triggered by data changes.

---

[API Gateway] — Zero-downtime deployment / canary routing
- Domain: Design High-Performing Architectures
- Question: Deploy new API version on API Gateway with zero downtime
- Trap: Updated existing API without using canary/stage routing
- Rule: API Gateway zero-downtime deployment = blue-green via canary release (stage variables + % traffic routing). Gradually shift traffic from old stage to new, validate, then cut over 100%.

---

[ASG] — Default scale-in termination policy
- Domain: Design Resilient Architectures
- Question: ASG with default settings, scale-in triggered — which instance is terminated first?
- Trap: Assumed random selection
- Rule: ASG default termination policy: (1) find the AZ with the most instances; (2) within that AZ, terminate the instance from the OLDEST launch template/configuration. Not random. Not the longest-running.

---

[RDS] — IAM DB Authentication feature name
- Domain: Design Secure Architectures
- Question: RDS must be accessed only via auth tokens derived from the EC2 instance's IAM profile credentials
- Trap: Answered "use IAM + STS combination for temp auth token" — describes the mechanism but not the feature
- Rule: The feature is Enable IAM DB Authentication. It generates short-lived tokens via the instance's IAM role (STS under the hood). Trigger phrase: "authentication token from instance profile credentials" → IAM DB Authentication.

---

[EKS] — Encrypting etcd secrets with KMS
- Domain: Design Secure Architectures
- Question: EKS cluster — encrypt sensitive data stored in the cluster's etcd key-value store
- Trap: Chose Secrets Manager + KMS (Secrets Manager stores secrets externally, not inside etcd)
- Rule: To encrypt EKS etcd secrets → enable envelope encryption on the EKS cluster using a KMS key. Secrets Manager is for external secret storage; it does NOT encrypt the etcd store itself.

---

[FSx / Storage] — Hot vs cold storage for ML workloads
- Domain: Design High-Performing Architectures
- Question: ML training needs high-performance parallel hot storage + cost-effective cold archive
- Trap: Chose FSx for Lustre + EBS io1 (EBS is per-instance block storage, not cold/archive)
- Rule: ML cold/archive = S3 (not EBS). FSx for Lustre integrates natively with S3 as a backing cold store. EBS is per-instance block storage with no archive semantics.

---

[CloudWatch] — Which EC2 metrics are custom (require agent)
- Domain: Design High-Performing Architectures
- Question: Which CloudWatch metric for EC2 requires manual/custom setup?
- Trap: Chose "Network packets out" (it's a standard hypervisor-visible metric)
- Rule: EC2 standard CW metrics (no agent): CPUUtilization, NetworkIn/Out, DiskReadOps/WriteOps, NetworkPacketsIn/Out. Custom metrics (CW Agent required): Memory utilization, disk space / swap (OS-level, not visible to the hypervisor).

---

[Aurora Global Database] — Cross-region DR with strict RPO/RTO
- Domain: Design Resilient Architectures
- Question: Relational DB — RPO = 1 s, RTO < 1 min, automatic cross-region failover (beyond RDS Multi-AZ)
- Trap: Chose RDS cross-region read replicas (require manual promotion, RTO >> 1 min)
- Rule: Cross-region RPO ~1 s + RTO < 1 min = Aurora Global Database (automated cross-region failover < 1 min). RDS cross-region read replicas require manual promotion — not automatic, not sub-minute.

---

[DMS / Elastic Beanstalk] — Homogeneous migration of .NET + Oracle
- Domain: Design Resilient Architectures
- Question: Migrate .NET ML app (Windows Server) + Oracle DB backend to AWS with minimal refactoring
- Trap: Chose ECS containers or AWS MGN instead of DMS + Beanstalk
- Rule: Homogeneous DB migration (Oracle → RDS Oracle) = AWS DMS. .NET app on Windows = Elastic Beanstalk (managed Windows platform, minimal refactoring). DMS handles the DB; Beanstalk handles the app.

---

[Aurora] — Custom endpoints for workload routing
- Domain: Design High-Performing Architectures
- Question: Route production traffic to high-capacity Aurora instances, reporting queries to low-capacity instances
- Trap: Used instance endpoint for production + cluster endpoint for reporting
- Rule: Aurora endpoints: Cluster = primary writer. Reader = load-balance across ALL readers. Custom endpoint = specific subset of instances you define. Use custom endpoints to route by instance size or workload type.

---

[Directory Services] — AD Connector vs Simple AD (multi-select)
- Domain: Design Secure Applications and Architectures
- Question: Federation from existing corporate Active Directory to AWS Console — roles already in corporate AD (Select TWO)
- Trap: Chose Simple AD instead of AD Connector
- Rule: Existing on-prem AD → AWS access = AD Connector (proxies auth requests to the existing AD, no sync, no migration). Simple AD = standalone LDAP-compatible managed directory with NO connection to on-prem AD.

---

[Lake Formation] — Multi-account data lake permissions
- Domain: Design High-Performing Architectures
- Question: Multi-account S3 data lake — query centrally with role-based access control
- Trap: Chose AWS Control Tower (Control Tower = account governance, not data access management)
- Rule: Multi-account data lake + role-based access = AWS Lake Formation (manages data lake permissions, cross-account data sharing, column/row-level security). Control Tower manages account guardrails, not data permissions.

---

[RDS] — Multi-AZ vs Read Replica for AZ failover
- Domain: Design Resilient Architectures
- Question: RDS database loses access during AZ outages — prevent it with a simpler same-region solution
- Trap: Chose "Create a read replica" (async replication, manual promotion required)
- Rule: AZ failure protection for RDS = Multi-AZ (synchronous standby, automatic failover). Read replicas = read scaling via async replication, NOT automatic failover. Read replicas must be manually promoted.

---

[Storage Gateway] — Hybrid file access + archiving
- Domain: Design Resilient Architectures
- Question: Hybrid company — on-prem documents need immediate access + cost-effective archiving of older data
- Trap: Chose DataSync or direct S3 upload (no local cache for immediate access)
- Rule: Hybrid file access + automatic tiering to Glacier = Storage Gateway File Gateway + S3 lifecycle policy. File Gateway caches recently accessed files on-prem; lifecycle rules tier older S3 objects to Glacier automatically.

---

[RDS] — Synchronous vs asynchronous replication
- Domain: Design Resilient Architectures
- Question: MySQL RDS in single AZ — improve HA using synchronous replication to another instance
- Trap: Chose RDS Read Replica (Read Replicas use ASYNCHRONOUS replication)
- Rule: "Synchronous replication" in RDS = Multi-AZ deployment. Read Replicas = asynchronous. The word "synchronous" is the exact trigger phrase for Multi-AZ. Never confuse the two.

---

### Guessed right (correct but uncertain)

- **Q3 — KMS custom key store + CloudHSM:** Custom key store = key material lives in YOUR CloudHSM, not AWS-managed. Gives immediate key deletion (no 7-30 day wait) + independent audit from CloudTrail.
- **Q13 — RDS Enhanced Monitoring:** For per-process CPU/memory inside RDS → Enhanced Monitoring (OS agent). Basic CloudWatch only sees hypervisor-level metrics, not per-process.
- **Q15 — S3 Object Lock modes:** Compliance + retention period = immutable for a fixed duration, even root can't delete. Governance = admins can override. Legal hold = no fixed period (toggle on/off). "No user including root can overwrite for a set period" → compliance mode + retention period.
- **Q21 — EventBridge → ECS:** EventBridge rule on S3 PUT can target the ECS cluster directly to run a new task (no Lambda intermediary needed).
- **Q27 — CloudWatch Agent vs Enhanced Monitoring:** EC2 memory + disk utilization → CloudWatch Agent (not Enhanced Monitoring, which is RDS-specific).
- **Q28 — Egress-Only IGW + Network Firewall:** Private subnet EC2 with IPv6 egress + traffic inspection → Egress-Only Internet Gateway + AWS Network Firewall.
- **Q33 — ElastiCache Redis AUTH:** Redis AUTH requires both `--transit-encryption-enabled` AND `--auth-token` at cluster creation. In-transit encryption must be on for AUTH to work.
- **Q38 — FSx for NetApp ONTAP:** Windows + HA across AZs + low-latency iSCSI block storage → FSx for NetApp ONTAP Multi-AZ (supports iSCSI for Windows block workloads; FSx for Windows File Server only supports SMB).
- **Q41 — Lambda for burst traffic:** "Burst traffic in seconds" + global users → API Gateway + Lambda. Lambda scales in milliseconds; EC2 ASG takes minutes.
- **Q43 — API Gateway throttling:** Backend protection from traffic spikes beyond subnet-level NACLs → API Gateway throttling limits.
- **Q48 — Kinesis + Lambda for PII anonymization:** Real-time PII ingestion → anonymize before storage → Kinesis Data Streams + Lambda (transform inline) → DynamoDB.
- **Q64 — S3 Object Lock + Access Point:** WORM storage + VPC-only access → S3 Object Lock (Legal Hold for indefinite protection) + S3 Access Point with VPC restriction.
- **Q65 — Lambda env var encryption:** Lambda encrypts env vars at rest with a service KMS key by default, but values are still visible in the console. For max security (prevent devs from seeing plaintext) → KMS encryption helpers (encrypt with your own KMS key before storing in env vars).

---

### Reflection

1. **Weakest domain:** Design Resilient Architectures — 53% (9 errors). Core gap: Multi-AZ vs Read Replica semantics, Aurora endpoint types, ASG termination policy.
2. **Services to brush up before Dojo #2:** Aurora endpoints (cluster / reader / custom), RDS Multi-AZ vs Read Replica vs Aurora Global, ASG termination + HA capacity math.
3. **New trigger phrases:** "synchronous replication" → Multi-AZ; "RPO 1s + RTO < 1min cross-region" → Aurora Global Database; "row-level Aurora trigger" → Aurora native Lambda invoke (not RDS event subscription); "authentication token from instance profile" → IAM DB Authentication; "existing on-prem AD proxy" → AD Connector (not Simple AD).

---

[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
