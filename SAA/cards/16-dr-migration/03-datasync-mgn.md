[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-dms-sct.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-snow-family.md)

# DataSync & Application Migration Service (MGN)

<img src="../../assets/icons/datasync.png" width="64">

> **Pitch (1 line):** DataSync moves file/object data (NFS/SMB/S3) at high speed with scheduling and integrity checks; MGN lifts-and-shifts servers to EC2 with continuous block-level replication.

## 🎯 When the exam picks this

- "migrate NFS / SMB file shares to Amazon EFS or S3" → **DataSync**
- "move petabytes of on-prem file data to AWS on a recurring schedule" → **DataSync**
- "migrate physical servers / VMs to EC2 (lift-and-shift)" → **Application Migration Service (MGN)**
- "replicate live server data to AWS with minimal cutover downtime" → **MGN (continuous replication)**

## 🧠 Core — DataSync

- Agent-based: install the **DataSync Agent** on your on-premises NFS/SMB server or in your existing storage system.
- Supports: on-premises ↔ S3, EFS, FSx for Windows, FSx for Lustre, FSx for ONTAP.
- Also S3 ↔ S3 cross-region, EFS ↔ EFS cross-region.
- Features: **scheduling** (run nightly, hourly, etc.), data integrity verification (checksums), bandwidth throttling, encryption in transit.
- **Much faster than a manual copy** — uses parallel, multi-part transfers and the AWS network.
- Use DataSync for initial large-data migration + Storage Gateway for ongoing hybrid access after migration.

**DataSync vs Storage Gateway:**
- DataSync: **one-time or scheduled data movement** (migration, replication).
- Storage Gateway: **ongoing hybrid access** (on-prem apps continuously using AWS storage).

## 🧠 Core — Application Migration Service (MGN)

- Formerly **CloudEndure Migration**. Preferred over the older **Server Migration Service (SMS)**.
- Works by installing an **MGN agent** on the source server (physical, VMware, Hyper-V, or other cloud).
- Continuously replicates **block-level data** to a staging area in AWS → minimal RPO.
- At cutover: launch **test or production EC2 instances** from the replicated data. Cutover downtime is minutes.
- Supports any OS and application — no changes to the server needed.

**MGN vs DMS:**
- MGN: lift-and-shift **servers** (whole OS + applications → EC2).
- DMS: migrate **databases** (data only, no OS).

## ⚠️ Common traps

- DataSync is NOT for real-time sync — it's scheduled or on-demand batch transfers.
- MGN requires network connectivity from source to AWS (over internet, VPN, or Direct Connect) for the continuous replication.
- DataSync agent on NFS/SMB servers; MGN agent on the source server — both require agent installation.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-dms-sct.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-snow-family.md)
