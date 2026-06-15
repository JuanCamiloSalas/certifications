[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)

# SAA — Priority Review

Distilled from the Dojo error logs. Study top-down: highest exam weight × weakest score first. If time runs out, stop — the top is what moves the needle. Each point gives the rule first, then the distractor that fooled you.

**Dojo #1 (2026-06-15): 70% (46/65).** Order = domain weight × error rate.

| Priority | Domain | Weight | Score | Effort |
|---|---|---|---|---|
| 1 | Resilient Architectures | 26% | 53% | heavy |
| 2 | High-Performing Architectures | 24% | 65% | medium |
| 3 | Secure Architectures | 30% | 90% | light |
| 4 | Cost-Optimized Architectures | 20% | 100% | skip |

---

## 1. Resilient Architectures

- **Multi-AZ vs Read Replica** — "synchronous replication" or "automatic failover" → Multi-AZ (synchronous standby, automatic failover). Read Replica is async, read-only, and needs manual promotion — never the HA/failover answer. The word "synchronous" alone decides it.
- **Aurora Global Database** — cross-region DR with RPO ~1s and RTO <1min and automatic failover → Aurora Global Database. The trap is RDS cross-region read replicas: they replicate cross-region but require manual promotion, so RTO is far above 1 min.
- **ASG min capacity for HA** — if the app needs N instances to function, set min = N × number of AZs. With 2 needed across 2 AZs, min = 4 (2 per AZ) so one AZ failure still leaves 2 running. Setting min = 2 across 2 AZs (1 each) fails this — a lost AZ drops you to 1.
- **ASG default termination** — picks the AZ with the most instances, then the instance from the oldest launch template/config. It is not random and not "longest running".
- **Aurora row-level trigger** — to react to a row change (e.g. a row deleted) use an Aurora native Lambda invoke (lambda_sync / lambda_async). The trap is RDS event subscriptions: those fire on instance events (failover, backup, maintenance), never on row-level data changes.
- **Homogeneous migration** — Oracle → RDS for Oracle uses AWS DMS; a .NET app on Windows Server goes to Elastic Beanstalk (managed Windows, minimal refactor). Don't reach for ECS/containers or MGN when the source maps cleanly to a managed target.
- **Hybrid file access + archive** — on-prem needs immediate file access plus cheap archiving → Storage Gateway File Gateway (caches hot files locally) + S3 lifecycle to Glacier. DataSync or direct S3 upload give no local cache for immediate access.

## 2. High-Performing Architectures

- **Aurora endpoints** — cluster endpoint = the writer; reader endpoint = load-balances across all readers; custom endpoint = a subset you define to route by workload or instance size. Using instance/cluster endpoints to split production vs reporting traffic is the wrong split — that's what custom endpoints exist for.
- **DynamoDB partition key** — uneven WCU consumption is fixed with a high-cardinality partition key (many distinct values) so writes spread across partitions. Low cardinality concentrates writes into hot partitions — the opposite of what you want.
- **DynamoDB Streams** — to react to item-level changes (INSERT / MODIFY / REMOVE), use DynamoDB Streams + Lambda. Don't reach for Kinesis or SNS for change-data on a table; Streams is the native capture.
- **CloudFront 504** — 504s under load mean the origin is overloaded or timing out. Fix it by raising the cache hit ratio (Cache-Control max-age at the origin) so fewer requests reach the origin. Multi-region routing or Lambda@Edge don't address an overloaded origin.
- **API Gateway zero-downtime** — deploy a new version with a canary release (stage variables + a percentage of traffic shifted to the new stage, then cut over). Editing the live stage in place is not zero-downtime.
- **Hot vs cold storage** — high-performance parallel hot storage = FSx for Lustre; cost-effective cold/archive = S3 (Lustre integrates natively with S3 as its backing store). EBS is per-instance block storage with no archive tier — wrong for cold data.
- **EC2 custom CloudWatch metrics** — memory and disk-space utilization are not emitted by the hypervisor; they need the CloudWatch Agent (custom metrics). CPU, NetworkIn/Out, NetworkPackets, and DiskReadOps/WriteOps are standard and need no agent.
- **Multi-account data lake** — query data across many accounts with role-based access → AWS Lake Formation (manages lake permissions, cross-account sharing, column/row-level access). Control Tower is account governance/guardrails, not data permissions.

## 3. Secure Architectures (nearly solid — quick pass)

- **IAM DB Authentication** — "authentication token derived from the instance's IAM profile credentials" → enable IAM DB Authentication on RDS (it mints short-lived tokens via the role; STS is the underlying mechanism, not the feature name).
- **EKS etcd secrets** — encrypt secrets stored in the cluster's etcd with envelope encryption on the EKS cluster using a KMS key. Secrets Manager stores secrets externally; it does not encrypt the etcd store itself.
- **AD Connector vs Simple AD** — an existing on-prem Active Directory → AD Connector (proxies auth to the existing AD, no sync, no migration). Simple AD is a standalone managed directory with no link to on-prem AD.
- **Federation to S3** — federation = Identity Provider + STS temp tokens + IAM Role + IAM Policy. The Role/Policy is always what grants the actual resource access; 3rd-party SSO tools (OKTA, etc.) don't replace it.

## 4. Cost-Optimized Architectures

- 100% on Dojo #1. Nothing to review.

---

## Confirm (got right but unsure)

Skim only if time allows.

- **KMS custom key store** — key material lives in your own CloudHSM, giving immediate key deletion (no 7–30 day wait) and auditing independent of CloudTrail.
- **RDS Enhanced Monitoring** — needed for per-process CPU/memory inside the DB; plain CloudWatch only sees hypervisor-level metrics.
- **S3 Object Lock modes** — compliance + retention period = immutable for a fixed window, even root can't delete. Governance = admins can override. Legal hold = protection with no fixed period (toggle on/off).
- **EventBridge → ECS** — an S3 PUT rule can target the ECS cluster directly to run a task; no Lambda intermediary required.
- **Egress-Only IGW** — allows IPv6 outbound from a private subnet; pair with AWS Network Firewall when traffic inspection is required.
- **ElastiCache Redis AUTH** — requires both --transit-encryption-enabled and --auth-token at cluster creation; in-transit encryption must be on for AUTH to work.
- **FSx for NetApp ONTAP** — Windows + HA across AZs + low-latency iSCSI block storage. FSx for Windows File Server only does SMB, so it can't serve iSCSI block.
- **Lambda for bursts** — burst-in-seconds traffic for global users → API Gateway + Lambda (scales in milliseconds; an EC2 ASG takes minutes to add capacity).
- **API Gateway throttling** — protects backend systems from traffic spikes beyond what subnet-level NACLs filter.
- **Kinesis + Lambda** — real-time PII ingestion that must be anonymized before storage → Kinesis Data Streams + Lambda (transform inline) → DynamoDB.
- **S3 Object Lock + Access Point** — WORM compliance (Legal Hold for indefinite protection) plus VPC-only access via an S3 Access Point.
- **Lambda env var encryption** — for max security use KMS encryption helpers with your own key so other devs can't read plaintext; Lambda's default service key still shows values in the console.

---

[![](https://img.shields.io/badge/<_Errors-FF4859?style=for-the-badge)](./README.md)
