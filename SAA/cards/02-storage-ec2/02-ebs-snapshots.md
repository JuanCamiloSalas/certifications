[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-ebs-volume-types.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-ebs-multi-attach.md)

# EBS Snapshots

> **Pitch (1 line):** point-in-time incremental backups of EBS volumes stored in S3 — the mechanism for cross-AZ/region volume migration and the basis of AMI creation.

## 🎯 When the exam picks this

- "move an EBS volume to a different AZ or region" → snapshot → copy → restore
- "restore a snapshot instantly without warming up" → **Fast Snapshot Restore (FSR)**
- "reduce snapshot storage cost for long-term retention" → **Snapshot Archive tier**
- "protect against accidental snapshot deletion" → **Recycle Bin**

## 🧠 Core (non-obvious bits)

- Snapshots are **incremental** — only changed blocks since the last snapshot are saved. Each snapshot is still a full logical restore point.
- Stored in **S3** (AWS-managed bucket, not visible in your S3 console).
- To move a volume across AZs: snapshot → create new volume from snapshot in target AZ.
- To move across regions: snapshot → **copy snapshot to target region** → create volume.
- **Fast Snapshot Restore (FSR):** eliminates the I/O latency ("initialization/warming") when creating a volume from a snapshot. Extra cost per snapshot per AZ it's enabled in.
- **Snapshot Archive:** move a snapshot to a cold tier — 75% cheaper, but restoring takes **24–72 hours**.
- **Recycle Bin:** retention rules (1 day to 1 year) that hold deleted snapshots so you can recover them from accidental deletion.
- You can snapshot a volume **while it's attached and in use** (recommended to pause I/O or detach for consistency).

## 🔢 Numbers to memorize

- Archive restore time: **24–72 hours**
- Archive savings: up to **75% cheaper** than standard snapshot storage
- Recycle Bin retention range: **1 day – 1 year**

## ⚠️ Common traps

- "snapshots are in S3" → true, but you access/manage them via EC2 console, not S3 console.
- FSR is per-AZ — enabling it in us-east-1a does NOT cover us-east-1b; you enable it per AZ.
- Restoring from archive is NOT instant — 24–72 h. If the question requires immediate restore, FSR or standard snapshot is the answer.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-ebs-volume-types.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-ebs-multi-attach.md)
