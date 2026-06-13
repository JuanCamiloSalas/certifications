[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-efs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./07-fsx.md)

# EC2 Instance Store

> **Pitch (1 line):** physically attached local disk on the host — **highest IOPS of any EC2 storage** option, but **ephemeral**: data is lost on stop, terminate, or host failure.

## 🎯 When the exam picks this

- "highest possible IOPS, millions of IOPS, very low latency" → **Instance Store**
- "temporary storage, buffer, cache, scratch space" → **Instance Store**
- "data must survive instance stop" → ❌ NOT Instance Store → EBS

## 🧠 Core (non-obvious bits)

- Unlike EBS (network), Instance Store is a **physical disk on the host** — no network I/O overhead, hence the extreme IOPS.
- Survives a **reboot** but is wiped on **stop, hibernate, terminate, or host hardware failure**.
- **Not all instance types** include Instance Store — only specific families (i3, i4i, d2, h1, etc.).
- You are responsible for replication and backup — AWS provides no managed backup for Instance Store.
- Capacity is fixed at instance launch — cannot be expanded.

## ⚠️ Common traps

- "high IOPS database" → if durability matters, use **io1/io2 EBS**, not Instance Store.
- Survives **reboot** (common trap) — it is **stop and terminate** that wipe it.

## 🔄 Easily confused with

- → [EBS Volume Types](./01-ebs-volume-types.md) — persistent, network-attached, io2 for high IOPS with durability
- Data persistence across lifecycle events → [Instance Lifecycle card](../01-ec2-saa/02-instance-lifecycle.md)

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-efs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./07-fsx.md)
