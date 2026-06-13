[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-hibernation.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-user-data-imdsv2.md)

# AMI Lifecycle (Copy, Sharing & Encryption)

> **Pitch (1 line):** an AMI is a snapshot of an EC2 instance packaged as a launchable image — understanding how to copy, share, and encrypt AMIs across regions and accounts is SAA-level territory.

## 🎯 When the exam picks this

- "launch identical instances in another region" → **copy AMI to target region**
- "share a golden image with another AWS account" → **AMI sharing** (private AMI → add account ID)
- "encrypt an unencrypted AMI at rest" → **copy the AMI with encryption enabled**

## 🧠 Core (non-obvious bits)

- AMIs are **regional** — to use one in another region you must **copy** it; the copy becomes an independent AMI with its own ID.
- **Copying an AMI copies its underlying EBS snapshots.** Cross-region copies incur data transfer costs.
- You can **encrypt an unencrypted AMI by copying it** and enabling encryption on the copy. You cannot directly modify an existing AMI's encryption state.
- **Sharing:** you can share a private AMI with specific AWS account IDs. The recipient can launch instances but **cannot copy the AMI** unless you also share the underlying snapshots.
- **EC2 Image Builder** automates AMI creation, testing, and distribution (separate concept → see card 08).
- **Deregistering** an AMI does NOT delete the underlying EBS snapshots — you must delete them manually.

## ⚠️ Common traps

- "copy an AMI to encrypt it" is valid; "modify an existing AMI to add encryption" is NOT — you always go through a copy.
- Deregistering the AMI ≠ deleting the snapshots. Snapshot charges continue until you delete them explicitly.
- A shared AMI recipient **cannot re-share or copy** the AMI unless the owner also shares the snapshot(s).

## 🔄 Easily confused with

- → [EC2 Image Builder](./08-image-builder.md) — automates the build/test/distribute pipeline for AMIs

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-hibernation.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-user-data-imdsv2.md)
