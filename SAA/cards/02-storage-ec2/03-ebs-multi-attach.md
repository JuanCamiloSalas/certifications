[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-ebs-snapshots.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-ebs-encryption.md)

# EBS Multi-Attach

> **Pitch (1 line):** attach a **single io1/io2 volume** to **up to 16 instances** in the **same AZ** simultaneously — each instance gets full read/write access.

## 🎯 When the exam picks this

- "multiple EC2 instances need concurrent read/write to the same EBS volume" → **Multi-Attach**
- "clustered or fault-tolerant app that manages its own storage consistency" → **Multi-Attach with io1/io2**

## 🧠 Core (non-obvious bits)

- Only available on **io1 and io2** volume types — not gp2, gp3, st1, sc1.
- All attached instances must be in the **same AZ** — you cannot span AZs.
- The application (or cluster-aware file system) is responsible for managing concurrent writes to avoid corruption — AWS does not handle write coordination. Typical use: **Teradata**, clustered databases, high-availability applications.
- The volume must use a **cluster-aware file system** (e.g., GFS2) — a standard file system like ext4 or XFS will corrupt data with multiple concurrent writers.

## 🔢 Numbers to memorize

- Max concurrent attachments: **16 instances**
- Same **AZ** required — no cross-AZ

## ⚠️ Common traps

- "share data between instances in different AZs" → NOT Multi-Attach (same AZ only) → use EFS instead.
- "multi-writer EBS for a regular workload" → Multi-Attach is not a silver bullet; the app must be cluster-aware.

## 🔄 Easily confused with

- → [EFS](./05-efs.md) — true shared file system, multi-AZ, Linux-only, no write-coordination burden on app

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-ebs-snapshots.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-ebs-encryption.md)
