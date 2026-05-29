[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./README.md)

# SQS Standard

> **Pitch:** Fully managed queue to decouple producers from consumers, with unlimited throughput and best-effort ordering.

## 🎯 When the exam picks this

- "decouple components"
- "buffer requests / smooth traffic spikes"
- "asynchronous processing"
- "scale workers independently from producers"

## 🧠 Core (non-obvious bits)

- **At-least-once delivery.** Consumers must be idempotent.
- **Best-effort ordering.** No order guarantee. If order matters → SQS FIFO.
- **Pull-based.** Consumers poll (`ReceiveMessage`). Use **long polling** (up to 20s) to cut empty responses and cost.
- **Visibility timeout** hides the message after a consumer picks it. If the consumer doesn't `DeleteMessage` in time, the message reappears and another worker processes it (poison-pill risk).
- **Dead Letter Queue (DLQ)** captures messages that exceed `maxReceiveCount`. Always set one in production.

## 🔢 Numbers to memorize

- Message size: **256 KB** max (use S3 + reference for larger payloads → "SQS Extended Client Library")
- Retention: **4 days default**, **1 min to 14 days** range
- Visibility timeout: **30s default**, max **12 hours**
- Long polling wait time: **0–20s**
- Delay queue: up to **15 min**
- Throughput: **unlimited** (Standard)

## ⚠️ Common traps

- "Order is required" → **NOT Standard**, use **FIFO**.
- "Exactly-once" → **NOT Standard**, use **FIFO** (dedupe window 5 min).
- "Real-time analytics on a continuous stream / replay" → **NOT SQS**, use **Kinesis** (SQS deletes messages after consumption; no replay).
- "Fan-out to multiple subscribers" → **NOT SQS alone**, use **SNS → SQS** pattern.
- ASG scaling on queue depth: target metric is `ApproximateNumberOfMessagesVisible`.

## 🔄 Easily confused with

- → [SQS Standard vs FIFO](../../comparativas/sqs-standard-vs-fifo.md)
- → [SQS vs SNS vs Kinesis vs Amazon MQ](../../comparativas/sqs-vs-sns-vs-kinesis.md)

## 💡 Architectural patterns

- **Decouple producer + ASG of consumers:** producer writes → SQS → ASG of EC2/Lambda consumes. ASG scales on queue depth.
- **Buffer for backend:** API in front, slow worker behind. SQS absorbs spikes.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./README.md)
