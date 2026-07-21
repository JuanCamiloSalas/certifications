[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-backends-and-state-storage.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-state-drift-refresh-only.md)

# Inspecting State

> **Pitch (1 line):** read what Terraform *thinks* exists — `state list` (addresses only), `show` (everything), `state show <addr>` (one resource in full).

## 🎯 What the exam tests

- Which command returns **just addresses** (`terraform state list`) vs **full attributes** (`terraform show` / `terraform state show`).
- The **workflow**: `state list` to find the address → `state show <addr>` to inspect it.
- That the legacy **write** subcommands exist (`state mv`, `state rm`, `state pull/push`) but 004 favors config-driven blocks.

## 🧠 Core (non-obvious bits)

- **`terraform state list`** → only the **addresses** of managed objects, including data sources and **indexed** items (`aws_subnet.public[0]`). No attributes.
- **`terraform show`** → **human-readable full dump** of the whole state (or of a saved plan file). Use to review all attributes / computed values / planned changes.
- **`terraform state show <addr>`** → full attributes of **one** resource. Pro flow: `list` to get the exact address, then `state show`.
- **Legacy write commands** (still valid, increasingly rare):
  - `state mv` → move/rename an object in state.
  - `state rm` → stop managing an object (**does not destroy it**).
  - `state pull` / `state push` → manual read/overwrite of remote state (risky).
- **004 direction:** know these exist, but HashiCorp pushes **config-driven** `moved` / `removed` / `import` blocks — version-controlled, reviewable, part of plan/apply (deep-dived in **S11 refactoring**).

## 💻 Syntax / Example

```bash
terraform state list                    # addresses only
# aws_vpc.vpc
# aws_subnet.public[0]
# data.aws_region.current

terraform show                          # full human-readable dump of ALL state
terraform state show aws_vpc.vpc        # full attributes of ONE resource

# legacy write ops (prefer moved/removed/import blocks on 004)
terraform state mv aws_instance.a aws_instance.b
terraform state rm aws_instance.old     # forget it — real resource keeps running
```

## ⚠️ Common traps

- `state list` gives **addresses only** — if the question wants attributes, it's `show` / `state show`.
- **`terraform show`** (no `state`) = whole state or a **plan file**; **`terraform state show ADDR`** = one resource. Easy to mix up.
- **`state rm` does NOT destroy** the real resource — it only drops it from Terraform's tracking.

## 🔄 Easily confused with

- `state mv` vs `state rm` vs `import` (CLI) → config-driven equivalents: [`moved`](./06-moved-block.md) / [`removed`](./07-removed-block.md) / [`import`](../07-maintain/01-import-block.md) blocks · [comparativa](../../comparativas/refactoring-moved-removed-import.md).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-backends-and-state-storage.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-state-drift-refresh-only.md)
