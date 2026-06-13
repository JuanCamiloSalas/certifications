[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-s3-encryption.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-s3-access-points.md)

# S3 Object Lock & Glacier Vault Lock

<img src="../../assets/icons/s3.png" width="64"> (WORM)

> **Pitch (1 line):** Write-Once-Read-Many (WORM) protection — Object Lock prevents S3 objects from being deleted or overwritten for a retention period; Glacier Vault Lock does the same for Glacier archives.

## 🎯 When the exam picks this

- "regulatory compliance, data cannot be deleted for 7 years" → **S3 Object Lock**
- "WORM storage" → **S3 Object Lock**
- "even the root account cannot delete these objects" → Object Lock in **Compliance mode**
- "lock a Glacier vault policy and make it immutable" → **Glacier Vault Lock**

## 🧠 Core (non-obvious bits)

**S3 Object Lock:**
- Requires **versioning** on the bucket.
- Two retention modes:
  - **Governance mode:** most users can't delete/overwrite, but accounts with `s3:BypassGovernanceRetention` permission can.
  - **Compliance mode:** **no one** — including the root account — can delete or modify the object until the retention period expires. Stricter, immutable.
- **Retention period:** a fixed time window (days/years) during which the object is protected.
- **Legal Hold:** independent of retention period. Object is protected until the hold is explicitly removed. No expiry.

**Glacier Vault Lock:**
- Applies a **Vault Lock policy** to a Glacier vault — e.g., "deny all deletes for 10 years."
- Once the policy is locked (confirmed), it is **immutable** — not even AWS can remove it.
- Use case: regulatory archives (SEC, FINRA, HIPAA) where you need proof the data hasn't been tampered with.

## ⚠️ Common traps

- Compliance mode ≠ Governance mode: Compliance is truly immutable (even root can't override); Governance allows authorized bypass.
- Legal Hold overrides the retention period in both directions — you can add or remove it independently.
- Glacier Vault Lock once confirmed is permanent — test in Compliance mode carefully before confirming.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-s3-encryption.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-s3-access-points.md)
