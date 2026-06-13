[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-ebs-multi-attach.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-efs.md)

# EBS Encryption

> **Pitch (1 line):** EBS encryption (via KMS) protects data at rest AND in transit between the volume and the instance — enabling it on an existing unencrypted volume requires a snapshot-copy dance.

## 🎯 When the exam picks this

- "encrypt data at rest on EC2 storage" → **EBS encryption**
- "encrypt an existing unencrypted EBS volume" → snapshot → copy with encryption → restore
- "enforce encryption for all new EBS volumes in the account" → **EBS encryption by default** (account setting)

## 🧠 Core (non-obvious bits)

- Encryption covers: **data at rest** on the volume, **data in flight** between the volume and the instance, **all snapshots**, and **volumes created from those snapshots**.
- Uses **AWS KMS** (CMK). You can use the AWS-managed key (`aws/ebs`) or your own CMK.
- **Encrypting an existing unencrypted volume:**
  1. Create a snapshot of the volume.
  2. Copy the snapshot and enable encryption on the copy.
  3. Create a new volume from the encrypted snapshot.
  4. Swap the volume on the instance.
- **Minimal performance impact** — encryption/decryption is handled transparently by the hypervisor; no app changes needed.
- **Account-level default:** you can enable "Encrypt new EBS volumes by default" — all newly created volumes and snapshots in the region will be encrypted automatically.
- Encrypted snapshots can be shared with other accounts, but you must also share the KMS CMK used.

## ⚠️ Common traps

- "direct conversion of an unencrypted volume to encrypted" → does NOT exist — you always go through a snapshot copy.
- "encryption at rest AND in transit with EBS" → both are covered by a single EBS encryption setting — no separate in-transit config needed.
- Sharing an encrypted snapshot across accounts requires sharing the **KMS key** as well, not just the snapshot.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-ebs-multi-attach.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-efs.md)
