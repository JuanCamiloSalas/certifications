[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./06-instance-store.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../03-elb-asg/README.md)

# Amazon FSx (All Variants)

> **Pitch (1 line):** fully managed third-party file systems on AWS — choose the right FSx flavor based on the protocol, OS, and workload type the question describes.

## 🎯 When the exam picks this

- "Windows / SMB / Active Directory / NTFS / DFS" → **FSx for Windows File Server**
- "HPC / ML / sub-millisecond latency / Lustre / integrate with S3" → **FSx for Lustre**
- "multi-protocol (NFS + SMB + iSCSI) / migrate NetApp on-prem / data deduplication" → **FSx for NetApp ONTAP**
- "NFS only / ZFS snapshots / OpenZFS migration / up to 1M IOPS" → **FSx for OpenZFS**

## 🧠 Core (non-obvious bits)

**FSx for Windows File Server:**
- Native Windows NTFS, SMB protocol, Active Directory integration.
- Supports **Microsoft DFS** (Distributed File System) for multi-AZ namespaces.
- Can be accessed from on-premises (over Direct Connect or VPN).

**FSx for Lustre:**
- Built for **HPC, ML, financial modeling, video processing** — workloads needing massive parallel throughput.
- Can be integrated with **S3**: reads from / writes back to an S3 bucket transparently.
- Deployment options: **Scratch** (no replication, max performance) vs **Persistent** (replicated within AZ, for long-running jobs).

**FSx for NetApp ONTAP:**
- Supports **NFS, SMB, and iSCSI** simultaneously (multi-protocol).
- Works with Linux, Windows, and macOS clients.
- Features: data deduplication, compression, point-in-time snapshots, SnapMirror replication.
- Best for lifting-and-shifting NetApp on-premises workloads to AWS.

**FSx for OpenZFS:**
- NFS protocol, works with Linux, Windows, macOS.
- Point-in-time snapshots, up to **1,000,000 IOPS** with < 0.5 ms latency.
- Best for migrating ZFS on-premises workloads.

## ⚠️ Common traps

- "shared file system for Windows" → FSx for Windows (not EFS — EFS is Linux NFS only).
- "Lustre scratch vs persistent" → scratch = short jobs, no HA; persistent = long-running jobs with replication.
- ONTAP ≠ just NFS — it's the multi-protocol option. If the question says iSCSI or multi-protocol → ONTAP.

## 🔄 Easily confused with

- → [EFS](./05-efs.md) — Linux NFS only, fully serverless, auto-scaling
- → [EBS](./01-ebs-volume-types.md) — block storage, single-instance (except Multi-Attach)

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./06-instance-store.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
