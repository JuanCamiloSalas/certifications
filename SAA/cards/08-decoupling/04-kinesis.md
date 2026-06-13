[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-sns-fanout.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-amazon-mq.md)

# Kinesis — Data Streams, Firehose & Analytics

> **Pitch (1 line):** Kinesis is the streaming platform — Data Streams for real-time processing with replay, Firehose for near-real-time delivery to data stores, Analytics for real-time SQL on streams.

## 🎯 When the exam picks this

- "real-time analytics / streaming data" → **Kinesis Data Streams**
- "replay events / multiple consumers read the same stream" → **Kinesis Data Streams**
- "deliver logs/events to S3 / Redshift / OpenSearch near real-time" → **Kinesis Data Firehose**
- "run SQL on a live data stream" → **Kinesis Data Analytics**

## 🧠 Core (non-obvious bits)

**Kinesis Data Streams (KDS):**
- Data organized in **shards**. Each shard: 1 MB/s write, 2 MB/s read.
- **Retention:** 1–365 days (default 24h). Consumers can **replay** data.
- **Multiple consumers** can read the same shard independently (fan-out).
- **Enhanced fan-out:** dedicated 2 MB/s per consumer per shard (parallel reads, push-based).
- **Partition key** determines which shard a record goes to (consistent hashing).
- Consumers: Lambda (event source mapping), EC2 apps via KCL/SDK, KDA.

**Kinesis Data Firehose (KDF):**
- **No shards, no manual scaling.** Fully managed, auto-scales.
- **Near real-time** (up to 60s buffer before delivery, or 1–128 MB buffer size).
- Destinations: S3, Redshift (via S3 COPY), OpenSearch, Splunk, HTTP endpoints, Datadog.
- Can optionally transform records with **Lambda** before delivery.
- **No replay** — data is delivered once and not stored in Firehose.

**Kinesis Data Analytics (KDA):**
- Run **SQL** (or Apache Flink) against a KDS or KDF stream in real-time.
- Outputs to KDS, KDF, Lambda.

## 🔢 Numbers to memorize

- KDS shard: **1 MB/s write, 2 MB/s read**
- Default retention: **24h** (up to **365 days**)
- Firehose buffer: up to **60s** or **128 MB**

## ⚠️ Common traps

- Firehose ≠ Data Streams: Firehose delivers to a destination (no replay, near-real-time); KDS stores records for consumers (replay, real-time).
- "multiple consumers reading the same data" → KDS (fan-out), not Firehose.
- SQS deletes messages after consumption; KDS retains for the full retention period.

## 🔄 Easily confused with

- → [SQS](./01-sqs-standard.md) — queue (consume-and-delete, no replay); Kinesis = stream (retain and replay)

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-sns-fanout.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-amazon-mq.md)
