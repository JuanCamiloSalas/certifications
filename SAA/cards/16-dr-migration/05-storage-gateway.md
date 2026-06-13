[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-snow-family.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/All_blocks_>-FF4859?style=for-the-badge)](../../README.md)

# AWS Storage Gateway

> **Pitch (1 line):** hybrid storage bridge that lets on-premises applications use AWS storage (S3, EBS, Glacier) as if it were local — available as a VM appliance or hardware device.

## 🎯 When the exam picks this

- "on-prem file server backed by S3 (NFS/SMB interface)" → **S3 File Gateway**
- "on-prem apps using NFS/SMB, archive cold files to Glacier automatically" → **FSx File Gateway**
- "on-prem iSCSI block storage backed by S3 with local cache" → **Volume Gateway (Cached)**
- "full volume on-prem, asynchronously backed up to S3 as EBS snapshots" → **Volume Gateway (Stored)**
- "on-prem tape library replaced by virtual tapes in S3/Glacier" → **Tape Gateway (VTL)**

## 🧠 Core (non-obvious bits)

**Three gateway types:**

**1. S3 File Gateway:**
- Presents an NFS or SMB mount point to on-prem apps.
- Files → stored as **S3 objects** (native S3 — not EBS).
- Local cache of frequently accessed files.
- S3 bucket can have lifecycle policies → auto-tier to Glacier.
- Use: file shares, backup target, content repositories.

**2. FSx File Gateway:**
- Presents SMB interface backed by **Amazon FSx for Windows File Server**.
- Local cache for low-latency access. Full managed Windows file system in the cloud.
- Use: Windows file shares replacing on-prem Windows file servers.

**3. Volume Gateway:**
- Presents iSCSI block storage to on-prem servers.
- **Cached mode:** primary data in S3, frequently accessed data cached locally (small on-prem footprint).
- **Stored mode:** primary data on-prem, entire volume backed up asynchronously to S3 as EBS snapshots (full local performance).
- Use: disaster recovery (restore volumes as EBS in AWS), backup.

**4. Tape Gateway (VTL — Virtual Tape Library):**
- Presents a virtual tape library to backup software (Veeam, Veritas, etc.) via iSCSI.
- Virtual tapes stored in S3; archived tapes in **S3 Glacier** (Glacier Flexible Retrieval or Deep Archive).
- Replace physical tape hardware without changing backup workflows.

## ⚠️ Common traps

- S3 File Gateway → files become native S3 objects (you can use S3 lifecycle, versioning, etc.).
- Volume Gateway (Cached) vs (Stored): Cached = data in S3 (cloud-primary); Stored = data on-prem (local-primary).
- Tape Gateway is for legacy backup tools that speak VTL — not for new architectures.
- Storage Gateway needs network connectivity to AWS (internet, VPN, or Direct Connect).

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-snow-family.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/All_blocks_>-FF4859?style=for-the-badge)](../../README.md)
