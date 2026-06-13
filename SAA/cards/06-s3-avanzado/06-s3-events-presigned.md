[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-s3-performance.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../07-cdn/README.md)

# S3 Events, Pre-Signed URLs & Requester Pays

<img src="../../assets/icons/s3.png" width="64">

> **Pitch (1 line):** three S3 features that appear in integration and cost-control questions — events trigger downstream processing, pre-signed URLs grant temporary access, Requester Pays shifts data transfer cost.

## 🎯 When the exam picks this

- "automatically process a file when uploaded to S3" → **S3 Event Notifications**
- "give a user temporary, time-limited access to a private object" → **Pre-signed URL**
- "customers download large datasets from your bucket, you don't want to pay the transfer" → **Requester Pays**

## 🧠 Core (non-obvious bits)

**S3 Event Notifications:**
- Trigger on: `s3:ObjectCreated`, `s3:ObjectRemoved`, `s3:ObjectRestore`, `s3:Replication`, etc.
- Destinations: **SNS topic**, **SQS queue**, **Lambda function**, or **EventBridge** (EventBridge supports filtering and routing to 18+ targets).
- Use **EventBridge** when you need advanced filtering, multiple destinations, or archiving events.
- Events are delivered **at least once** — design consumers to be idempotent.

**Pre-Signed URLs:**
- Generate a temporary URL that grants GET or PUT access to a specific object, expiring after a set time.
- Generated using IAM credentials of the **signing user/role** — the URL inherits their permissions.
- Use case: let unauthenticated users download a private object (e.g., a paid report) or upload directly to S3 without exposing AWS credentials.
- Default expiry: 3600s (1 hour). Max: 7 days (with SigV4 pre-signing).

**Requester Pays:**
- When enabled, the **requester** (not the bucket owner) pays for data transfer and request costs.
- Requester must be authenticated (anonymous access not supported).
- Use case: public datasets where you want to share data without incurring egress costs.

## ⚠️ Common traps

- Pre-signed URL validity depends on the credentials used: if the IAM role that signed the URL expires (e.g., STS token), the URL stops working even if the expiry hasn't passed.
- Event Notifications are NOT guaranteed to preserve order and may be delivered more than once.
- Requester Pays does NOT apply to S3 storage costs — only to request and transfer costs.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-s3-performance.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../07-cdn/README.md)
