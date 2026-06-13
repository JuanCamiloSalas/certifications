[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-datasync-mgn.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-storage-gateway.md)

# AWS Snow Family

<img src="../../assets/icons/snow-family.png" width="64">

> **Pitch (1 line):** physical devices AWS ships to you for offline data transfer when the internet is too slow or unavailable — Snowcone (small), Snowball Edge (rugged/compute), Snowmobile (exabyte truck).

## 🎯 When the exam picks this

- "transfer 10s of TB to AWS, limited bandwidth or takes months online" → **Snowball Edge**
- "edge computing + storage in disconnected / ruggedized environment" → **Snowball Edge Compute Optimized**
- "transfer exabytes (100+ PB) to AWS" → **Snowmobile** (literal truck)
- "small lightweight device (8 TB), edge AI inference or IoT collection" → **Snowcone**

## 🧠 Core (non-obvious bits)

| Device | Storage | Compute | Use case |
|---|---|---|---|
| **Snowcone** | 8 TB HDD / 14 TB SSD | 2 vCPUs, 4 GB RAM | Small edge data collection, highly portable, ruggedized |
| **Snowball Edge Storage Optimized** | 80 TB usable | 40 vCPUs, 80 GB RAM | Large-scale data migration, bulk storage |
| **Snowball Edge Compute Optimized** | 42 TB usable | 52 vCPUs, 208 GB RAM + optional GPU | Edge ML inference, local processing before transfer |
| **Snowmobile** | Up to **100 PB** per vehicle | N/A | Exabyte-scale data center migration |

**How it works:**
1. Order device in AWS Console → AWS ships it to you.
2. Connect to your network → copy data to the device.
3. Ship back to AWS → AWS uploads to S3.
4. Encrypted (AES-256), tamper-resistant, tracked by GPS (Snowmobile).

**Rule of thumb — when to use Snow vs internet transfer:**
- If transferring over the internet would take > 1 week → consider Snow.
- Example: 100 TB at 1 Gbps = ~9 days → Snowball.

**OpsHub:**
- GUI application to manage Snow devices locally (start/stop EC2 instances on the device, transfer files, monitor).

## 🔢 Numbers to memorize

- Snowcone: **8 TB** (HDD) / **14 TB** (SSD)
- Snowball Edge Storage: **80 TB**
- Snowmobile: up to **100 PB**

## ⚠️ Common traps

- Snow devices are NOT for real-time or ongoing data ingestion — they're for bulk one-time (or periodic) migrations.
- "Exabyte" or "100+ PB" → Snowmobile (the truck). "80 TB" → Snowball Edge.
- Snowcone is tiny and battery-powered — not for large volumes.
- Data is encrypted on the device — AWS cannot read it; encryption keys managed in KMS.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-datasync-mgn.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-storage-gateway.md)
