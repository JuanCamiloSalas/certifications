[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../01-ec2-saa/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-ebs-snapshots.md)

# EBS Volume Types

> **Pitch (1 line):** six EBS volume types split into SSD (performance) and HDD (throughput); choosing the right one is one of the most common SAA cost/performance questions.

## 🎯 When the exam picks this

- "high IOPS, low latency, database workload" → **io1 / io2**
- "general purpose, balanced cost" → **gp3** (default choice today)
- "big data, data warehouse, sequential reads" → **st1**
- "cheapest, cold/archival data, infrequent access" → **sc1**
- "only SSDs can be used as boot volumes" → ⚠️ HDD (st1/sc1) **cannot** boot

## 🧠 Core (non-obvious bits)

**SSD:**
- **gp2:** IOPS are **coupled to size** (3 IOPS/GB, burst to 3,000). Legacy — prefer gp3 for new volumes.
- **gp3:** IOPS and throughput are **independent of size** (baseline 3,000 IOPS / 125 MB/s; can provision up to 16,000 IOPS / 1,000 MB/s). ~20% cheaper than gp2.
- **io1 / io2:** Provisioned IOPS SSD. Use when you need > 16,000 IOPS. io2 has better durability (99.999% vs 99.8%) and higher IOPS:GB ratio. Supports **Multi-Attach**.
- **io2 Block Express:** up to **256,000 IOPS** and **4,000 MB/s** — for the most demanding DBs.

**HDD (cannot be boot volumes):**
- **st1 (Throughput Optimized):** sequential, big data — Kafka, EMR, log processing.
- **sc1 (Cold HDD):** cheapest EBS option — cold data accessed rarely.

## 🔢 Numbers to memorize

| Type | Max IOPS | Max Throughput | Boot? |
|---|---|---|---|
| gp2 | 16,000 | 250 MB/s | ✅ |
| gp3 | 16,000 | 1,000 MB/s | ✅ |
| io1 | 64,000* | 1,000 MB/s | ✅ |
| io2 | 64,000* (256k Block Express) | 4,000 MB/s | ✅ |
| st1 | 500 | 500 MB/s | ❌ |
| sc1 | 250 | 250 MB/s | ❌ |

*64,000 IOPS requires Nitro-based instances.

## ⚠️ Common traps

- "migrate from gp2 to gp3 to save cost" → valid and safe; gp3 is strictly better-priced.
- sc1 and st1 look similar — sc1 = **cold** (even cheaper, lower IOPS limit); st1 = **throughput** (faster sequential, big data pipelines).
- io1 vs io2: prefer io2 — same price, higher durability, better IOPS:GB ratio.

## 🔄 Easily confused with

- → [EBS Multi-Attach](./03-ebs-multi-attach.md) — io1/io2 only
- → [Instance Store](./06-instance-store.md) — for max IOPS with no network overhead

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../01-ec2-saa/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-ebs-snapshots.md)
