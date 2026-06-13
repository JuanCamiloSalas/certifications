[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-burstable-cpu-credits.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-ami-lifecycle.md)

# EC2 Hibernation

> **Pitch (1 line):** pause an instance by freezing RAM to the root EBS volume — next start resumes from exactly where it left off, much faster than a cold boot.

## 🎯 When the exam picks this

- "preserve in-memory state between stops" → **Hibernation**
- "faster startup than a regular stop/start" → **Hibernation**
- "long-running process that must survive without restarting from scratch" → **Hibernation**

## 🧠 Core (non-obvious bits)

- On hibernate: RAM contents are written to the **root EBS volume** (must be encrypted), then the instance stops. On next start, RAM is restored and the OS resumes — no bootstrap.
- The root EBS must be large enough to hold the RAM dump **plus** the OS.
- **RAM limit: max 150 GB.**
- Supported on **On-Demand and Reserved** instances; NOT available on Spot (Spot can be interrupted, which breaks the guarantee).
- Not all instance families support it — generally available on C, M, R families (check current docs for exact list; exam tests the concept, not the full list).
- **Max hibernation time: 60 days.** Beyond that the instance is terminated.

## 🔢 Numbers to memorize

- Max RAM: **150 GB**
- Max hibernation duration: **60 days**
- Root EBS: must be **encrypted** + big enough for RAM + OS

## ⚠️ Common traps

- "save RAM state across stops" → Hibernate, NOT a regular stop (stop wipes RAM).
- Root EBS **must be encrypted** — if the question mentions unencrypted root volume, hibernation is not possible.
- Spot instances do **not** support hibernation (AWS can reclaim Spot at any time).

## 🔄 Easily confused with

- → [Instance Lifecycle (stop vs hibernate vs terminate)](./02-instance-lifecycle.md)

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-burstable-cpu-credits.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-ami-lifecycle.md)
