[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# SQS vs SNS vs Kinesis vs Amazon MQ

> SQS to decouple workers, SNS to fan out notifications, Kinesis to stream and replay, Amazon MQ to migrate legacy brokers.

## Decision table

| | SQS Standard | SQS FIFO | SNS | Kinesis Data Streams | Kinesis Firehose | Amazon MQ |
|---|---|---|---|---|---|---|
| **Model** | Queue (pull) | Queue (pull) | Pub/Sub (push) | Stream (pull / push) | Delivery pipeline | Broker (AMQP/JMS) |
| **Ordering** | Best-effort | Strict FIFO per group | None | Per-shard ordered | None | Protocol-dependent |
| **Delivery** | At-least-once | Exactly-once | At-least-once | At-least-once | At-least-once | Protocol-dependent |
| **Replay** | ❌ deleted after ACK | ❌ deleted after ACK | ❌ no persistence | ✅ 24 h–365 days | ❌ no persistence | ❌ |
| **Multiple consumers** | Compete for messages | Compete for messages | All subscribers in parallel | Each consumer reads full stream | One destination | Protocol-dependent |
| **Throughput** | Unlimited | 300 msg/s (3 k w/ batching) | Unlimited | 1 MB/s write per shard | Auto-scales | Bound by instance size |
| **Retention** | 1 min–14 days | 1 min–14 days | None | 24 h–365 days | None | Configurable |
| **Serverless** | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ EC2 instances |
| **Native AWS protocols** | ✅ | ✅ | ✅ | ✅ | ✅ | ❌ AMQP / MQTT / JMS / STOMP |

## When the exam picks each

- **SQS Standard:** "decouple components", "buffer / smooth traffic spikes", "async processing", "workers scale independently from producers"
- **SQS FIFO:** "exactly-once", "strict ordering", "financial transactions", "e-commerce order pipeline"
- **SNS:** "notify multiple subscribers from one event", "fan out to independent SQS queues", "email/SMS alert to many recipients"
- **Kinesis Data Streams:** "real-time analytics", "replay events", "multiple consumers read the same records", "IoT / clickstream at scale"
- **Kinesis Firehose:** "deliver logs / events to S3 / Redshift / OpenSearch near real-time", "no custom consumer code needed"
- **Amazon MQ:** "existing app uses JMS / AMQP / MQTT, migrate without code changes", "lift-and-shift ActiveMQ or RabbitMQ"

## Common traps

- **SQS ≠ Kinesis replay.** SQS deletes the message after a consumer ACKs it. Kinesis retains records for the full retention window — multiple consumers replay independently.
- **SNS does NOT persist messages.** If a subscriber is down, the message is lost. Add SQS behind SNS (fan-out) to get durability.
- **New app → SQS / SNS, not MQ.** Amazon MQ is a migration tool. New cloud-native workloads get SQS/SNS (infinite scale, native AWS integrations, serverless).
- **SNS FIFO → only SQS FIFO.** HTTP, email, and SMS endpoints are NOT supported for SNS FIFO topics.
- **SQS FIFO throughput cap.** 300 msg/s (3,000 with batching). Standard has unlimited throughput. Exam uses throughput clues to force a FIFO vs Standard choice.
- **Firehose ≠ Data Streams.** Firehose delivers to a destination once (no replay, ~60 s buffer). Data Streams stores records for your consumer apps to read and re-read.

## Linked cards

- [SQS Standard](../cards/08-decoupling/01-sqs-standard.md)
- [SQS FIFO & Advanced](../cards/08-decoupling/02-sqs-fifo-advanced.md)
- [SNS & Fan-Out](../cards/08-decoupling/03-sns-fanout.md)
- [Kinesis](../cards/08-decoupling/04-kinesis.md)
- [Amazon MQ](../cards/08-decoupling/05-amazon-mq.md)

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
