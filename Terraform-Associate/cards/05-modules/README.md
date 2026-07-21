[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../04-configuration/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../06-state/README.md)

# Block 05 — Modules

> **Objetivo 5:** usar y crear módulos para componer y reutilizar configuración.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [What is a module](./01-what-is-a-module.md) | Container of `.tf`; root vs parent vs child; `main`/`variables`/`outputs.tf` _(S12)_ |
| 02 | [Calling modules — `module` block](./02-module-block.md) | `module "name" { source … }`; inputs; `terraform init`/`get` to download; meta-args _(S12)_ |
| 03 | [Module sources & versioning](./03-module-sources-and-versioning.md) | Registry/Git/local; `version` **registry-only**; Git `?ref=`; `~>` _(S12)_ |
| 04 | [Inputs, outputs & scope](./04-module-inputs-outputs-scope.md) | Isolated scope; args → child `var.*`; `module.<name>.<output>`; root has no access by default _(S12)_ |

## 🎯 Suggested concepts to cover

- ✅ **Root module** = the working directory; **child modules** = called via `module` blocks. → card 01 _(S12)_
- ✅ `source` types: **registry** (public/private), **Git**, **local path**. `version` applies **only** to the registry. → card 03 + [comparativa](../../comparativas/module-source-types.md) _(S12)_
- ✅ Passing **input variables** to a module and reading its **outputs** (`module.<name>.<output>`). → card 04 _(S12)_
- ✅ Module structure & best practices (`main.tf`, `variables.tf`, `outputs.tf`). → card 01 _(S12)_
- ✅ **Variable scope / isolation** — each module has its own scope; root can't see the child by default. → card 04 _(S12)_
- ✅ Public **Terraform Registry** — find and **pin** a module version. → cards 02·03 _(S12)_
- ⬜ `count` / `for_each` / `depends_on` on a module block (meta-args) — referenced in card 02; deepened with resource behavior in **S13**.

## 🔗 Related comparisons

- ✅ [Module source types](../../comparativas/module-source-types.md) — registry vs Git vs local.

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../04-configuration/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../06-state/README.md)
