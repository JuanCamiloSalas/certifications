[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-cloudtrail.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../13-iam-advanced/README.md)

# AWS Config + X-Ray

<img src="../../assets/icons/config.png" width="64">

> **Pitch (1 line):** Config = continuous compliance recorder ("is my resource config correct?"); X-Ray = distributed tracing ("why is my app slow?").

## 🎯 When the exam picks this

- "detect when an S3 bucket becomes public / security group allows 0.0.0.0:22" → **AWS Config rules**
- "compliance: record configuration history of every resource over time" → **AWS Config**
- "auto-remediate non-compliant resources" → **AWS Config + SSM Automation**
- "trace a request through Lambda → API GW → DynamoDB, find the slow hop" → **X-Ray**
- "end-to-end distributed tracing for microservices / serverless" → **X-Ray**

## 🧠 Core — AWS Config

**What it does:**
- Records the configuration state of AWS resources over time → answers "what did this resource look like at timestamp T?"
- **Config Rules:** evaluate resources against desired configuration. Triggered on change or on a schedule.
- **Managed rules** (AWS-provided): over 150 prebuilt checks (e.g., `s3-bucket-public-read-prohibited`, `encrypted-volumes`).
- **Custom rules:** Lambda-backed rules for any custom logic.
- **Remediation:** auto-remediate with SSM Automation documents. Can be automatic or manual.
- **Multi-account / multi-region aggregator:** central compliance view across all accounts in an Org.

**Config ≠ CloudTrail:**
- Config: tracks **resource configuration state** over time (what the resource looks like).
- CloudTrail: tracks **API calls** (who did what action).

## 🧠 Core — X-Ray

**What it does:**
- Distributed tracing — follows a single request through all services and shows a **service map** + **trace timeline**.
- Identifies latency bottlenecks, error rates, throttling, and root causes in distributed applications.

**How to enable:**
- Add the **X-Ray SDK** to your application code (instruments outgoing HTTP calls, AWS SDK calls).
- Run the **X-Ray daemon** on EC2/ECS/EKS as a sidecar. Lambda and Elastic Beanstalk handle this automatically.
- Enable **Active Tracing** on Lambda to capture Lambda traces without code changes.

**Key concepts:**
- **Trace:** end-to-end record of a single request.
- **Segment:** one service's contribution to the trace.
- **Subsegment:** finer-grained breakdown within a segment (e.g., one DynamoDB call).
- **Annotations:** indexed key-value pairs you can filter/search on.
- **Metadata:** non-indexed data attached to traces (large blobs, not searchable).

## ⚠️ Common traps

- AWS Config records history but is NOT a change management tool — it doesn't prevent changes, just detects and reports them.
- X-Ray requires code instrumentation (SDK) for custom apps — it's not automatic for all services.
- Config Rules evaluate compliance but don't fix violations on their own — remediation must be configured separately.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-cloudtrail.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../13-iam-advanced/README.md)
