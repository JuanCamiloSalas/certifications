[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-rds-proxy.md)

# RDS — Managed Relational DB

<img src="../../assets/icons/rds.png" width="64">

> **Pitch (1 line):** managed SQL DB (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Db2) with automated backups, Multi-AZ for HA, and Read Replicas for read scaling.

## 🎯 When the exam picks this

- "managed SQL database, no admin overhead" → **RDS**
- "scale read traffic, reporting queries" → **RDS Read Replicas**
- "automatic failover, high availability" → **RDS Multi-AZ**
- "encrypt data at rest in the DB" → **RDS encryption with KMS**
- "auth token from the instance's IAM profile, no password" → **IAM DB Authentication**

## 🧠 Core (non-obvious bits)

**Read Replicas (scaling reads, NOT HA):**
- Up to **15 read replicas** per instance (5 for non-Aurora RDS).
- Replication is **asynchronous** — replica may lag; reads are eventually consistent.
- Can be in the **same AZ, different AZ, or different region**.
- Can be **promoted** to a standalone DB (loses replica role permanently).
- Cross-region replicas incur data transfer costs.

**Multi-AZ (HA, NOT scaling):**
- AWS maintains a **synchronous standby** in another AZ.
- **Automatic failover** in 1–2 minutes if the primary fails — DNS endpoint flips.
- Standby is **NOT readable** — it only serves as failover. Zero read scaling benefit.
- Backups are taken from the standby — no I/O impact on primary.

**Backups:**
- **Automated backups**: enabled by default, 1–35 day retention, stored in S3. Enables point-in-time restore.
- **Manual snapshots**: user-initiated, no expiry, survive even after DB deletion.

**Encryption:**
- **At rest:** KMS (CMK or AWS-managed). Must be enabled at **creation time** — to encrypt an existing unencrypted DB, snapshot → copy with encryption → restore.
- **In transit:** SSL/TLS always available; enforce with `rds.force_ssl` parameter.
- Read Replicas of an encrypted DB are **automatically encrypted**.

**IAM DB Authentication (MySQL/PostgreSQL):**
- Connect with a **short-lived token** (15 min) generated from the EC2 instance's IAM role — no DB password stored. Uses STS under the hood; SSL/TLS required.
- Trigger phrase: "authentication token from instance profile credentials" → enable **IAM DB Authentication**.

## 🔢 Numbers to memorize

- Read replicas: up to **5** (RDS) / **15** (Aurora)
- Automated backup retention: **1–35 days**
- Multi-AZ failover: **~1–2 minutes**

## ⚠️ Common traps

- Read Replica ≠ Multi-AZ: replica = read scaling (async); Multi-AZ = failover (sync, not readable).
- "cross-region read replica" → network cost applies, standby does not help with this.
- Enabling Multi-AZ on existing DB causes brief I/O suspension (a few minutes).

## 🔄 Easily confused with

- → [Aurora](./03-aurora.md) — MySQL/PostgreSQL compatible, but proprietary engine with much higher throughput

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-rds-proxy.md)
