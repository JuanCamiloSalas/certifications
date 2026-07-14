[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-terraform-state.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-inspecting-state.md)

# Backends & State Storage

> **Pitch (1 line):** the **`backend`** (inside the `terraform {}` block) decides **where state lives** — local by default, or remote (S3, azurerm, gcs, HCP) for teams, with **locking** + encryption.

## 🎯 What the exam tests

- Default backend is **local** (`terraform.tfstate` in the working dir).
- Backend config goes in the **`terraform` block, NOT a `provider` block** — and you must run **`terraform init`** after adding/changing it.
- **State locking** prevents concurrent runs from corrupting state.
- S3-native locking is **`use_lockfile = true`**; **DynamoDB locking is deprecated** (004 gotcha — this changed).
- Local vs remote trade-offs (collaboration, locking, encryption, versioning).

## 🧠 Core (non-obvious bits)

- **Local (default):** `terraform.tfstate` on disk. Fine for learning/solo. Limits: **no team collaboration, no locking, plain-text on disk, no automatic backups.**
- **Remote:** S3 / Azure Blob (`azurerm`) / GCS / **HCP Terraform**. Gives **team collaboration, state locking, encryption at rest, automatic versioning.** Needs setup and may cost money. **Recommended for the exam & production.**
- **State locking** — Terraform locks state during any write op so two applies can't corrupt it. **Automatic** for most remote backends; for **S3** you opt in with **`use_lockfile = true`**.
- The **backend block takes literal values only** — no `var.`/expressions/interpolation. Supply dynamic values with **`terraform init -backend-config=...`** (partial config).
- **Never put credentials in the backend block** — use IAM roles / environment variables (see the Azure example).
- Changing backend → re-run **`terraform init`**; Terraform offers to **migrate** existing state (→ [`terraform init`](../03-core-workflow/02-terraform-init.md) `-migrate-state` / `-reconfigure`).

## 💻 Syntax / Example

```hcl
# Amazon S3 — native locking (no DynamoDB needed anymore)
terraform {
  backend "s3" {
    bucket       = "prd-terraform-state"      # the S3 bucket
    key          = "prod/terraform.tfstate"   # the object (path) for this state
    region       = "us-east-1"
    use_lockfile = true                        # ← S3-native state locking
  }
}
```

```hcl
# Azure Blob Storage — DO NOT hardcode auth here; use roles / env vars
terraform {
  backend "azurerm" {
    storage_account_name = "prodterraform"
    container_name       = "tfstate"
    key                  = "prod.terraform.tfstate"
    # tenant_id / client_id → prefer env vars or a managed identity
  }
}
```

## 🚩 Flags & values to memorize

- **`use_lockfile = true`** → S3-native state locking. **DynamoDB `dynamodb_table` locking is deprecated.**
- Backend block = **literal values only**; dynamic values via **`-backend-config=<file|key=value>`** at `init`.
- **`terraform init` is mandatory** after adding/changing a backend; `-migrate-state` copies existing state, `-reconfigure` discards the saved association.
- Only **one** backend per configuration.

## ⚠️ Common traps

- Backend config in a **`provider` block** → wrong; it lives in the **`terraform` block**.
- Interpolation/variables **inside the backend block** → not allowed; use `-backend-config`.
- Added/changed backend but didn't `init` → "Backend initialization required" error.
- "S3 needs DynamoDB for locking" → **outdated**; 004/TF 1.12 use `use_lockfile`.

## 🔄 Easily confused with

- → [local vs remote backend](../../comparativas/local-vs-remote-backend.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-terraform-state.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-inspecting-state.md)
