[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../02-fundamentals/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../04-configuration/README.md)

# Block 03 — Core workflow & CLI

> **Objetivo 3:** el ciclo Write → Plan → Apply y los comandos centrales. **Bloque pesado** — aquí caen muchas preguntas precisas de comandos y flags.

## 🃏 Cards in this block

_(none yet — copy [`../_TEMPLATE.md`](../_TEMPLATE.md) to start)_

| # | Card | Concept |
|---|---|---|
| — | — | — |

## 🎯 Suggested concepts to cover

- ⬜ The workflow: **Write → Plan → Apply** (and `destroy`).
- ⬜ `terraform init` — downloads providers/modules, initializes the backend. Mandatory first.
- ⬜ `terraform plan` — preview; `apply` — execute; `destroy` — tear down. Flags: `-auto-approve`, `-target`, `-var`, `-var-file`.
- ⬜ Saved plans: `terraform plan -out=tfplan` then `terraform apply tfplan`.
- ⬜ **Providers**: `required_providers`, version constraints (`~>`, `>=`, `=`), `alias` for multiple configs.
- ⬜ `.terraform.lock.hcl` (dependency lock file) — what it pins and why to commit it.
- ⬜ `terraform fmt` (format) and `terraform validate` (syntax/consistency, **does not** contact providers).

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- plan vs apply vs refresh
- validate vs plan (what each checks)

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../02-fundamentals/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../04-configuration/README.md)
