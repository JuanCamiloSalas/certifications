[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-depends-on.md)

# `import` Block

> **Pitch (1 line):** brings **existing** (manually-created) infrastructure under Terraform management by mapping a real-world **`id`** to a config **address** — declaratively, inside plan/apply.

## 🎯 What the exam tests

- The syntax: **`import { to = <addr>  id = "<provider-id>" }`**.
- The hard requirement: **you must write the target `resource` block first** (or generate it) — importing to a non-existent block errors.
- The config-generation flag: **`terraform plan -generate-config-out=PATH`**.
- The contrast with the **CLI** `terraform import <addr> <id>`: imperative, **no plan step**, modifies state immediately. Exam: know it exists, but **the block is the modern approach**.

## 🧠 Core (non-obvious bits)

- **`to`** = the resource address it maps to · **`id`** = the provider's real-world identifier. The **`id` format is provider-specific**: `"my-org/production"` (GitHub repo), `"/subscriptions/1234/rg/my-rg"` (Azure RG), `i-1234…` (EC2).
- **Write the resource block first** — manually, or scaffold it with `terraform plan -generate-config-out=generated.tf`.
- **Part of plan/apply** → you can **preview** the import before it happens (the CLI command can't).
- **Delete the `import` block** after a successful apply (same lifecycle as `moved`/`removed`).
- Import **adopts** existing infra — it does **not create** anything new.

## 💻 Syntax / Example

```hcl
import {
  to = github_repository.prd_app
  id = "my-org/production"          # provider-specific real-world ID
}

resource "github_repository" "prd_app" {   # MUST exist before importing
  name        = "production"
  description = "Production codebase"
}
```

```bash
terraform plan -generate-config-out=generated.tf   # scaffold the resource block for you

# Legacy CLI (imperative, no plan step, state changed immediately):
terraform import aws_instance.web i-1234567890abcdef0
```

## 🚩 Flags & values to memorize

- Block args: **`to`** (config address) · **`id`** (provider ID, format varies).
- **`-generate-config-out=PATH`** — auto-write the resource block during plan.
- CLI `terraform import ADDR ID` — no plan step, still needs the config written manually.

## ⚠️ Common traps

- **Importing without a `resource` block → error.** Create it first (or generate it).
- CLI `terraform import` **modifies state immediately, no plan** — the `import` block is previewable/reviewable.
- Import **maps existing** infra; it never provisions new resources.

## 🔄 Easily confused with

- → [moved vs removed vs import](../../comparativas/refactoring-moved-removed-import.md)

---

[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-depends-on.md)
