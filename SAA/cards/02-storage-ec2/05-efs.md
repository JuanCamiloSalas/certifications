[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-ebs-encryption.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-instance-store.md)

# EFS — Elastic File System

> **Pitch (1 line):** a managed **NFS** file system that mounts concurrently across **hundreds of Linux EC2s in multiple AZs** — pay per use, no capacity planning.

## 🎯 When the exam picks this

- "shared file system across multiple EC2 instances" → **EFS** (not EBS)
- "shared storage for Linux workloads across AZs" → **EFS**
- "reduce storage cost for files rarely accessed" → **EFS-IA or EFS Archive**
- "lower cost, single-AZ shared storage" → **EFS One Zone**

## 🧠 Core (non-obvious bits)

**Linux only** — EFS uses NFS v4; Windows instances cannot mount it natively.

**Storage classes:**
- **Standard** — frequently accessed files, multi-AZ.
- **Standard-IA** — infrequent access, multi-AZ, up to 92% cheaper than Standard.
- **Archive** — rarely accessed (a few times a year), cheapest tier.
- **One Zone / One Zone-IA** — single AZ, lower cost, less resilient (good for dev/test or easily reproducible data).
- Lifecycle policies automatically move files between tiers based on last-access time.

**Performance modes** (set at creation, cannot change):
- **General Purpose** (default) — low latency, ideal for web serving, CMS, home directories.
- **Max I/O** — higher aggregate throughput, slightly higher latency — for big data, media processing with thousands of parallel clients.

**Throughput modes:**
- **Bursting** — throughput scales with storage size (like gp2 for EBS). Works for most workloads.
- **Provisioned** — you set a fixed throughput regardless of storage size. Use when you need more throughput than Bursting provides.
- **Elastic** — automatically scales throughput up and down based on workload. Recommended default for unpredictable workloads.

## 🔢 Numbers to memorize

- Standard-IA savings: up to **92%** vs Standard
- Elastic throughput: scales automatically (no fixed limit to memorize for exam)
- Performance mode: **cannot change after creation**

## ⚠️ Common traps

- EFS is **Linux only** — for Windows shared file system → **FSx for Windows**.
- Performance mode cannot be changed after the file system is created.
- "EFS One Zone" is cheaper but single-AZ — not suitable for multi-AZ HA workloads.

## 🔄 Easily confused with

- → [EBS Multi-Attach](./03-ebs-multi-attach.md) — block storage, same AZ only, cluster-aware app required
- → [FSx](./07-fsx.md) — for Windows (SMB/AD) or HPC (Lustre) use cases

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-ebs-encryption.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-instance-store.md)
