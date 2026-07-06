[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-terraform-editions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)

# HCL Basics, Style & `fmt`

> **Pitch (1 line):** HCL is Terraform's declarative language — everything is a **block** (`type "labels" { arguments }`), and `terraform fmt` enforces the canonical style.

## 🎯 What the exam tests

- Reading a block's anatomy: block type + labels + `{ arguments }`.
- That **`terraform fmt`** is the built-in **formatter** (style only) — not a linter, not `validate`.
- Basic style conventions and that HCL is Terraform's primary interface.

## 🧠 Core (non-obvious bits)

- A **block** = `<type> "<label1>" "<label2>" { ... }`. For a `resource`: label1 = resource *type* (fixed by provider), label2 = *name* (yours) → address `<type>.<name>`.
- **Arguments** are `key = value`; blocks can nest. `resource` *manages* objects, `data` *reads* existing info.
- Terraform reads **all `.tf` files** in a directory as one merged config (files aren't isolated).
- **Comments:** `#` is idiomatic single-line (also `//`); `/* ... */` for block comments.
- **Style guide:** 2-space indent · align `=` on consecutive lines · `_` in names · blank lines between arg groups · avoid hardcoding (use variables).
- **`terraform fmt`** auto-formats files in place; use `.tf` extension so tooling recognizes them.

## 💻 Syntax / Example

```hcl
# block type ─┐  ┌─ resource type   ┌─ resource name (yours)
resource "aws_vpc" "vpc" {          #  ← address: aws_vpc.vpc
  cidr_block = "10.0.0.0/16"        #  ← argument; aligned '=', 2-space indent
}
```

```bash
terraform fmt              # rewrite files in current dir to canonical style
terraform fmt -check       # report only, non-zero exit if unformatted (CI gate)
terraform fmt -recursive   # include subdirectories
```

## 🚩 Flags & values to memorize

- `terraform fmt` — rewrites in place; `-check` = no write (report), `-recursive` = subdirs, `-diff` = show changes.
- **`fmt` = formatting only.** It does NOT check correctness — that's `validate`.

## ⚠️ Common traps

- First label of a `resource` is the **type** (provider-defined); second is a **name** you choose.
- Don't confuse **`fmt`** (style) with **`validate`** (syntax/consistency, no provider calls) — see [glosario](../../glosario.md).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-terraform-editions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)
</content>
