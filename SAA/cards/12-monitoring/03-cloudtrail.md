[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-eventbridge.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-config-xray.md)

# CloudTrail — API Audit Log

> **Pitch (1 line):** records every AWS API call (who did what, when, from where) — the compliance and forensics log for your account.

## 🎯 When the exam picks this

- "who deleted the S3 bucket / terminated the instance / changed the IAM policy?" → **CloudTrail**
- "audit trail of all API calls in the account" → **CloudTrail**
- "compliance: prove no unauthorized access over the last 90 days" → **CloudTrail + S3 export**
- "detect unusual API activity, react automatically" → **CloudTrail + EventBridge**

## 🧠 Core (non-obvious bits)

**Event types:**
- **Management events (control plane):** API calls that manage AWS resources (CreateBucket, RunInstances, DeleteUser…). Enabled by default, retained **90 days** in CloudTrail console.
- **Data events (data plane):** object-level operations (S3 GetObject/PutObject, Lambda Invoke, DynamoDB GetItem). Disabled by default — high volume, extra cost.
- **Insights events:** detect unusual write API activity (rate anomalies). Disabled by default.

**Trails:**
- Without a trail, events are only visible in the console for 90 days — **not stored**.
- Create a **trail** to deliver events to **S3** (indefinite retention, queryable with Athena) and optionally to **CloudWatch Logs** for alarming.
- **Organization trail:** single trail covering all accounts in an AWS Organization.
- **Multi-region trail:** captures events in all regions (recommended default).

**Integrity:**
- Enable **log file validation** to detect whether log files were modified or deleted after delivery (uses SHA-256 hash digest files).

## ⚠️ Common traps

- CloudTrail logs **API calls**, not OS-level activity inside EC2. For in-instance activity → CloudWatch Agent or Systems Manager.
- Default 90-day history is **read-only console view** — not stored anywhere. You MUST create a trail for durable storage.
- Data events cost extra and are high-volume — only enable for specific resources (not all S3 buckets) unless needed.
- CloudTrail ≠ CloudWatch: CloudTrail = API audit (who did what); CloudWatch = performance monitoring (how is it running).

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-eventbridge.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-config-xray.md)
