[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-sqs-fifo-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-kinesis.md)

# SNS & Fan-Out Pattern

<img src="../../assets/icons/sns.png" width="64">

> **Pitch (1 line):** SNS is a pub/sub service — one message published to a topic is delivered to all subscribers simultaneously; combining SNS → SQS is the canonical fan-out pattern.

## 🎯 When the exam picks this

- "notify multiple subscribers (email, Lambda, SQS) from one event" → **SNS**
- "one event must trigger multiple independent queues/processes" → **SNS + SQS fan-out**
- "order and deduplication in pub/sub" → **SNS FIFO topic → SQS FIFO queues**

## 🧠 Core (non-obvious bits)

**SNS:**
- **Publisher → Topic → Subscribers** (push model). Subscribers receive messages in real-time.
- Subscriber types: SQS, Lambda, HTTP/HTTPS endpoints, email, SMS, mobile push.
- Each subscriber receives every message published to the topic (with optional **filter policies**).
- **SNS FIFO topics:** preserve order, exactly-once delivery — can only fan-out to **SQS FIFO queues**.
- **Message filtering:** subscriber-level filter policy (JSON) — each subscriber only receives messages matching its filter. Reduces noise and downstream processing.

**Fan-Out Pattern (SNS + SQS):**
```
Producer
   ↓
SNS Topic
   ├── SQS Queue A (process A)
   ├── SQS Queue B (process B)
   └── Lambda (process C)
```
- One publish → all subscribers process independently and asynchronously.
- **Why not publish directly to multiple SQS?** You'd need multiple publishes in your code — if one fails, you get partial delivery. SNS fan-out is atomic from the producer's perspective.
- Also decouples producers from knowing how many consumers exist.

**SNS + S3 Events:**
- S3 can send events directly to SNS; SNS then fans out to SQS/Lambda/etc. — supports fan-out from S3 uploads.

## ⚠️ Common traps

- SNS is push-based — consumers don't poll; they receive. This is the opposite of SQS.
- SNS does NOT persist messages — if a subscriber is offline, the message is lost (use SNS → SQS to add durability).
- SNS FIFO → only SQS FIFO subscribers (not HTTP, email, SMS).

## 🔄 Easily confused with

- → [SQS Standard](./01-sqs-standard.md) — queue (pull), SNS = topic (push)
- → [Kinesis](./04-kinesis.md) — stream with replay; SNS has no replay

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-sqs-fifo-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-kinesis.md)
