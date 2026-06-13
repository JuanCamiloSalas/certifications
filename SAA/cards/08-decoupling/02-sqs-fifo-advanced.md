[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-sqs-standard.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-sns-fanout.md)

# SQS FIFO & Advanced SQS Features

<img src="../../assets/icons/sqs.png" width="64">

> **Pitch (1 line):** SQS FIFO guarantees strict order and exactly-once delivery at the cost of lower throughput; visibility timeout, long polling, and DLQs are the operational knobs for Standard too.

## 🎯 When the exam picks this

- "order must be preserved, no duplicates" → **SQS FIFO**
- "message reappears even though it was processed" → **visibility timeout** too short
- "reduce empty poll responses and cost" → **long polling**
- "handle poison-pill messages that keep failing" → **Dead Letter Queue (DLQ)**

## 🧠 Core (non-obvious bits)

**SQS FIFO:**
- **Strict ordering** within a message group (`MessageGroupId`). Messages in different groups can be processed in parallel.
- **Exactly-once processing** via deduplication (`MessageDeduplicationId`). If the same ID is sent twice within the **5-minute deduplication window**, the second is discarded.
- Queue name must end in `.fifo`.
- **Throughput:** 300 msg/s (without batching), 3,000 msg/s (with batching of 10), up to **70,000 msg/s** in high-throughput mode.

**Visibility Timeout:**
- After a consumer receives a message, it becomes invisible for the visibility timeout duration.
- If the consumer doesn't delete it within that time → message **reappears** and another worker processes it.
- Set it longer than your processing time. Extend it programmatically with `ChangeMessageVisibility`.

**Long Polling:**
- Consumer waits up to **20s** for messages to arrive. Reduces empty responses (and cost). Always prefer long polling over short polling.

**Dead Letter Queue (DLQ):**
- After `maxReceiveCount` failed processing attempts, the message moves to a DLQ.
- The DLQ must be **the same type** (Standard DLQ for Standard queue; FIFO DLQ for FIFO queue).
- **DLQ redrive:** once you fix the bug, you can redrive messages from the DLQ back to the source queue.

## 🔢 Numbers to memorize

- FIFO deduplication window: **5 minutes**
- FIFO throughput: **300/s** (3,000 batched), up to **70,000/s** high-throughput mode
- Long polling max wait: **20s**
- Visibility timeout range: **0s – 12h**

## ⚠️ Common traps

- FIFO guarantees order only within a `MessageGroupId` — across groups, there's no cross-group ordering.
- "message processed twice" → visibility timeout is too short, not a bug in the queue type.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-sqs-standard.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-sns-fanout.md)
