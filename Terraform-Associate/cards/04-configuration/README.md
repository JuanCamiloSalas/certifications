[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)

# Block 04 — Read & write configuration

> **Objetivo 4:** variables, outputs, data sources, expresiones y funciones. **Bloque pesado** — sintaxis HCL pura, ideal para cards con snippets.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Resource referencing](./01-resource-referencing.md) | Attribute references → implicit dependencies _(seen in S3)_ |
| 02 | [File structure & organization](./02-file-structure.md) | All `.tf` merged; conventional filenames; state/lock/gitignore; blast radius _(S6)_ |
| 03 | [Provider block](./03-provider-block.md) | `provider "…"`; auth via env vars; one provider→many resources; `alias` _(S7)_ |
| 04 | [Resource & data blocks](./04-resource-and-data-blocks.md) | resource (create) vs data (read); type/name; naming rules _(S7)_ |
| 05 | [Variable block & types](./05-variable-block.md) | `variable`; description/type/default; string/number/bool/list/map/set _(S7)_ |
| 06 | [Variable precedence](./06-variable-precedence.md) | Assign values + order (default < env < tfvars < auto.tfvars < `-var`) _(S7)_ |
| 07 | [Output block](./07-output-block.md) | `output`; value/description/sensitive; module integration; interpolation _(S7)_ |
| 08 | [Terraform block & version constraints](./08-terraform-block.md) | `required_version` · `required_providers` · `backend`; `=`/`>=`/`~>` _(S7)_ |
| 09 | [Built-in functions](./09-built-in-functions.md) | `name(args)`; no user-defined fns; type/numeric/string/collection/CIDR; `terraform console` _(S10)_ |
| 10 | [Dynamic values](./10-dynamic-values.md) | Interpolation `${…}`; data sources are read-only; compose var+local+data _(S10)_ |
| 11 | [Local values](./11-locals.md) | `locals {}` (define) vs `local.` (ref); computed inside; not settable from outside _(S10)_ |
| 12 | [`count` meta-argument](./12-count-meta-argument.md) | N copies by index; `count.index`; reindex gotcha; `cond ? 1 : 0` _(S10)_ |
| 13 | [`for_each` meta-argument](./13-for_each-meta-argument.md) | Map/set → per-key; `each.key`/`each.value`; stable keys; `toset(list)` _(S10)_ |

> Más cards al cursar **S14** (securing configs: `sensitive`, secrets handling).
> **S10 "Making Code Reusable"** entra aquí (no en el bloque 05): es lenguaje de configuración —functions, interpolación, locals, `count`/`for_each`— del objetivo 4, no módulos.

## 🎯 Suggested concepts to cover

- ✅ **File structure**: all `.tf` merged; conventional filenames; state/lock/gitignore; blast radius. → card 02 _(S6)_
- ✅ **Provider block**: `provider "…"`, auth via env vars, `alias` / `provider =`. → card 03 _(S7)_
- ✅ **Resource & data blocks**: create vs read; type/name; naming rules. → card 04 _(S7)_
- ✅ **Input variables**: `type`, `default`, `description`; primitive + collection types. → card 05 _(S7)_ · `validation`/`sensitive` deepened in S14.
- ✅ **Variable precedence** (low→high): defaults → `TF_VAR_*` → `terraform.tfvars` → `*.auto.tfvars` → `-var`/`-var-file`. → card 06 _(S7)_
- ✅ **Outputs**: `value`, `sensitive`, `description`; consumed by parent modules. → card 07 _(S7)_
- ✅ **Terraform block**: `required_version`, `required_providers`, `backend`; version constraints `=`/`>=`/`~>`. → card 08 _(S7)_
- ✅ Resource addressing & **references** (`resource.name.attr`), implicit dependencies. → card 01
- ✅ **Types & complex structures**: string/number/bool, list, map, set. → card 05 _(object/tuple not in S7)_
- ✅ **Local values** (`locals` define / `local.` ref) and when to use them vs variables. → card 11 _(S10)_
- ✅ **Built-in functions** (`name(args)`; no user-defined; type/numeric/string/collection/CIDR) — test with `terraform console`. → card 09 _(S10)_
- ✅ **Dynamic values / interpolation** (`${…}`, compose var+local+data; data sources read-only). → card 10 _(S10)_
- ✅ **Meta-arguments `count` / `for_each`** (index vs stable keys). → cards 12·13 _(S10)_ · [comparativa](../../comparativas/count-vs-for-each.md)
- ⬜ Dynamic blocks; more expressions (conditionals `? :`, `for` expressions, splat `[*]`). _(not in S10)_

## 🔗 Related comparisons

- ✅ [count vs for_each](../../comparativas/count-vs-for-each.md) — numeric index vs stable keys.

_(still to create in [`../../comparativas/`](../../comparativas/) when they appear)_

- Input variables vs locals vs outputs
- list vs set vs map vs object

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../03-core-workflow/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)
