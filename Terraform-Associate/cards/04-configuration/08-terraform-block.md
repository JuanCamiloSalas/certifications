[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./07-output-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)

# Terraform Block & Version Constraints

> **Pitch (1 line):** the `terraform {}` block sets project-wide settings — `required_version`, `required_providers`, and the state `backend`.

## 🎯 What the exam tests

- What lives in the `terraform` block: **`required_version`**, **`required_providers`** (source + version), **`backend`**.
- **Version-constraint operators**: `=` (exact), `>=`, and **`~>`** (pessimistic) — and exactly what `~>` allows.
- That a provider **source** is `namespace/name` (e.g. `hashicorp/aws`).

## 🧠 Core (non-obvious bits)

- **`required_version`** — which Terraform **CLI** versions may run this config (prevents "works on my 1.10, breaks on their 1.11").
- **`required_providers`** — pins each provider's **`source`** (`hashicorp/aws`) and **`version`**. Provider versions live **here**, not in the `provider` block.
- **`backend`** — where state is stored (e.g. `s3`); only one backend. Details are a block-06 (state) topic.
- **Version operators:**
  - **`= 5.77.0`** (or bare `"5.77.0"`) → **exactly** that version.
  - **`>= 1.9.8`** → that version **or newer**.
  - **`~> 5.87.0`** → **pessimistic**: lets the **right-most** component increment → `>= 5.87.0, < 5.88.0`.

## 💻 Syntax / Example

```hcl
terraform {
  required_version = "~> 1.10.0"          # 1.10.x only

  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"                   # >= 5.0.0, < 6.0.0
    }
  }

  backend "s3" {
    bucket = "prd-terraform-east-2"
    key    = "state/terraform.tfstate"
    region = "us-east-2"
  }
}
```

## 🚩 Flags & values to memorize

- **`~> 1.10.0`** (3 parts) = `>= 1.10.0, < 1.11.0` → **patch** floats.
- **`~> 5.0`** (2 parts) = `>= 5.0, < 6.0` → **minor** floats.
- `=` / bare = exact · `>=` = at-least · `~>` = pessimistic (right-most increments).
- Provider `source` = `namespace/name` (default namespace `hashicorp`).

## ⚠️ Common traps

- **Provider version goes in `required_providers`**, not the `provider` block → [provider-block](./03-provider-block.md).
- `~> 1.10.0` floats the **patch**; `~> 1.10` floats the **minor** — know which is which.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./07-output-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)
