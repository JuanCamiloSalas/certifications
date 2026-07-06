[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)

# Block 04 — Read & write configuration

> **Objetivo 4:** variables, outputs, data sources, expresiones y funciones. **Bloque pesado** — sintaxis HCL pura, ideal para cards con snippets.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Resource referencing](./01-resource-referencing.md) | Attribute references → implicit dependencies _(seen in S3)_ |

> Más cards al cursar **S6 · S7 · S14** (file structure, config fundamentals, securing).

## 🎯 Suggested concepts to cover

- ⬜ **Input variables**: `type`, `default`, `description`, `validation`, `sensitive`.
- ⬜ **Variable precedence** (low→high): defaults → `TF_VAR_*` env → `terraform.tfvars` → `*.auto.tfvars` (alpha order) → `-var` / `-var-file` (CLI wins).
- ⬜ **Outputs**: `value`, `sensitive`, `description`; how they're consumed by parent modules / remote state.
- ⬜ **Data sources** (`data` blocks) — read existing/external info without managing it.
- ⬜ **Local values** (`locals`) and when to use them vs variables.
- ✅ Resource addressing & **references** (`resource.name.attr`), implicit dependencies. → card 01
- ⬜ **Built-in functions** (`element`, `lookup`, `for`, `length`, `merge`, `templatefile`, …) — test with `terraform console`.
- ⬜ **Types & complex structures**: string/number/bool, list, map, set, object, tuple.
- ⬜ Dynamic blocks; expressions (conditionals `? :`, `for` expressions, splat `[*]`).

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- Input variables vs locals vs outputs
- list vs set vs map vs object

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)
