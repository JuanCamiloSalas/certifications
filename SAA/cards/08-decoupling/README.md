[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../07-cdn/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../09-containers/README.md)

# Block 08 — Decoupling

> **SQS, SNS, Kinesis, Amazon MQ.** The exam loves "queue, pub-sub, or stream?" questions. Learn to classify fast.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [SQS Standard](./01-sqs-standard.md) | Decoupling queue, unlimited throughput, best-effort ordering |
| 02 | [SQS FIFO & Advanced](./02-sqs-fifo-advanced.md) | Ordering, deduplication, visibility timeout, DLQ, long polling |
| 03 | [SNS & Fan-out](./03-sns-fanout.md) | Pub/sub, FIFO topics, fan-out pattern, message filtering |
| 04 | [Kinesis](./04-kinesis.md) | Data Streams (shards), Firehose (delivery), Data Analytics |
| 05 | [Amazon MQ](./05-amazon-mq.md) | ActiveMQ/RabbitMQ, MQTT/AMQP lift-and-shift |

## 🎯 Suggested concepts to cover

- SQS Standard: unlimited throughput, best-effort ordering, at-least-once delivery
- SQS FIFO: ordering + deduplication, 300 msg/s (3000 batched, 70k high-throughput)
- SQS: visibility timeout, long polling, DLQ, redrive policy
- SNS: pub/sub, topics, subscriptions (HTTP, email, Lambda, SQS, mobile)
- SNS FIFO topics
- Fan-out pattern: SNS → multiple SQS
- Kinesis Data Streams: shards, retention, producer/consumer
- Kinesis Data Firehose: to S3 / Redshift / OpenSearch (near real-time)
- Kinesis Data Analytics
- Kinesis Video Streams
- Amazon MQ: ActiveMQ and RabbitMQ (lift & shift apps using JMS/AMQP/MQTT)

## 🔗 Related comparisons

- **SQS vs SNS vs Kinesis vs Amazon MQ** (the most critical in this block)
- SQS Standard vs FIFO
- Kinesis Data Streams vs Firehose vs Data Analytics
- SNS vs SQS (when to add SQS behind SNS)

## 💡 Trigger phrases for this block

- "decouple components" → **SQS**
- "fan-out / publish-subscribe" → **SNS** (or SNS + SQS)
- "real-time analytics on streaming data" → **Kinesis Data Streams**
- "ordering matters / no duplicates" → **SQS FIFO**
- "lift and shift with JMS/AMQP" → **Amazon MQ**
- "process data and deliver to S3 near real-time" → **Kinesis Firehose**

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../07-cdn/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../09-containers/README.md)
