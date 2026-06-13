[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../09-containers/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-lambda-concurrency.md)

# Lambda — Fundamentals, Limits & Triggers

> **Pitch (1 line):** run code without servers — Lambda executes your function in response to events, bills per ms of execution, and scales automatically up to account-level concurrency limits.

## 🎯 When the exam picks this

- "run code without managing servers, scales automatically" → **Lambda**
- "event-driven processing (S3 upload, DynamoDB Stream, SQS message)" → **Lambda**
- "execution > 15 min required" → ❌ NOT Lambda → ECS/Fargate or EC2

## 🧠 Core (non-obvious bits)

**Invocation models:**
- **Synchronous (push):** caller waits for result. Sources: API Gateway, ALB, CloudFront, Cognito, SDK/CLI.
- **Asynchronous (event):** caller doesn't wait. Sources: S3 events, SNS, EventBridge. Lambda retries twice on failure; use **destinations** for success/failure routing.
- **Poll-based (stream/queue):** Lambda polls the source and processes batches. Sources: SQS, Kinesis, DynamoDB Streams, MSK. Failures go to the event source's DLQ or Lambda's destination.

**Trigger examples:**
- S3 → Lambda (image resize on upload)
- DynamoDB Streams → Lambda (real-time change processing)
- SQS → Lambda event source mapping (queue consumer)
- API Gateway → Lambda (serverless API)
- EventBridge schedule → Lambda (cron replacement)

## 🔢 Numbers to memorize

| Limit | Value |
|---|---|
| Max execution time | **15 minutes** |
| Memory | **128 MB – 10 GB** |
| Sync payload (request/response) | **6 MB** |
| Async payload | **256 KB** |
| Ephemeral storage (`/tmp`) | **512 MB – 10 GB** |
| Deployment package size (zip) | **50 MB** zipped / **250 MB** unzipped |
| Environment variable size | **4 KB** |

## ⚠️ Common traps

- "processing takes 20 minutes" → Lambda can't do it (15 min max) → ECS Fargate.
- Lambda scales by **adding more concurrent instances** of the function, not by making one instance faster.
- Asynchronous invocations retry twice automatically — design for idempotency.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../09-containers/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-lambda-concurrency.md)
