[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./07-removed-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)

# Securing State Files

> **Pitch (1 line):** state **will** contain secrets in plaintext, so security is about **where it's stored** and **who can read it** — remote, encrypted, access-controlled, locked.

## 🎯 What the exam tests

- Why **local** state is risky (unencrypted on a laptop, easy to commit, no access controls) vs **remote** (encryption at rest, IAM/RBAC, audit logging).
- The **defense-in-depth** stack: **encryption** + **access controls** + **audit logging** (+ **state locking**).
- That the recommendation for production is **always remote state with encryption**.

## 🧠 Core (non-obvious bits)

- **State stores secrets as plaintext JSON** — you can't stop that (Terraform needs it), so protect the *storage*. → [terraform state](./01-terraform-state.md)
- **Local vs remote:** local = on disk, unencrypted, no controls, easy to leak to git. Remote (S3/HCP) = centralized, encrypted at rest, IAM/RBAC, audit logs.
- **Defense in depth:**
  - **Encryption at rest** — backend-managed; add **KMS / customer-managed keys** for compliance and rotation. → [backends & state storage](./02-backends-and-state-storage.md)
  - **Access control** — IAM/RBAC; separate **read vs write**; only authorized users/roles.
  - **Audit logging** — record every access.
  - **State locking** — prevent concurrent modifications (`use_lockfile` for S3; built-in for others). ⚠️ DynamoDB locking is **deprecated** on 004.
- **To actually keep a secret out of state**, masking isn't enough — use [ephemeral values / write-only arguments](../04-configuration/18-ephemeral-values-and-write-only-arguments.md).

## 💻 Syntax / Example

```hcl
terraform {
  backend "s3" {
    bucket       = "prd-terraform-state"
    key          = "app/terraform.tfstate"
    region       = "us-east-2"
    encrypt      = true                 # encryption at rest
    kms_key_id   = "arn:aws:kms:...:key/abc"   # customer-managed key
    use_lockfile = true                 # state locking (DynamoDB deprecated)
  }
}
```

## 🚩 Flags & values to memorize

- Production → **remote + encrypted + access-controlled + locked**.
- S3 encryption: `encrypt = true` (+ `kms_key_id` for CMK).
- S3 locking: **`use_lockfile = true`** (DynamoDB deprecated).
- Defense in depth = encryption **+** access control **+** audit logging.

## ⚠️ Common traps

- Encryption alone isn't enough — pair it with **access controls** and **audit logging**.
- `sensitive = true` does **not** secure state — it only masks logs. State security is separate.

## 🔄 Easily confused with

- **Local vs remote backend** → [comparativa](../../comparativas/local-vs-remote-backend.md)
- Keeping secrets **out** of state → [ephemeral & write-only](../04-configuration/18-ephemeral-values-and-write-only-arguments.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./07-removed-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)
