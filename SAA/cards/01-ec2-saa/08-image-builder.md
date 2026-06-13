[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./07-spot.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)

# EC2 Image Builder

> **Pitch (1 line):** a managed pipeline that **automatically builds, tests, and distributes** AMIs (or container images) on a schedule or trigger — no manual golden-image maintenance.

## 🎯 When the exam picks this

- "automate AMI creation, patching, and distribution" → **EC2 Image Builder**
- "ensure every AMI is tested before being shared across accounts/regions" → **EC2 Image Builder**
- "keep a hardened, up-to-date golden image without manual effort" → **EC2 Image Builder**

## 🧠 Core (non-obvious bits)

- Pipeline steps: **Source (base AMI or OS)** → **Build (install/configure software)** → **Test (run automated tests)** → **Distribute (copy to regions / share with accounts)**.
- **Free service** — you only pay for the underlying EC2 instances and EBS snapshots used during the build and test phases.
- Can output **EC2 AMIs** or **Docker container images** (for ECR).
- Runs on a **schedule** (cron) or can be triggered manually / via EventBridge.
- Each build spins up a temporary EC2 instance, applies the recipe, runs tests, then terminates the instance and creates the AMI from the resulting snapshot.

## ⚠️ Common traps

- Image Builder itself is free; the **EC2 time + EBS storage** during build/test is what you pay for.
- It does **not** manage running instances — it only creates images. Instance patching at runtime is done with Systems Manager Patch Manager, not Image Builder.

## 🔄 Easily confused with

- → [AMI Lifecycle (copy, sharing, encryption)](./05-ami-lifecycle.md) — manual AMI operations
- Systems Manager Patch Manager — patches running instances (not images)

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./07-spot.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
