[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../02-fundamentals/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../04-configuration/README.md)

# Block 03 — Core workflow & CLI

> **Objetivo 3:** el ciclo Write → Plan → Apply y los comandos centrales. **Bloque pesado** — aquí caen muchas preguntas precisas de comandos y flags.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [The Core Terraform Workflow](./01-terraform-workflow.md) | Write → Plan → Apply loop; init bootstraps, destroy tears down |
| 02 | [`terraform init`](./02-terraform-init.md) | Downloads providers/modules, inits backend, writes lock file |
| 03 | [`terraform plan`](./03-terraform-plan.md) | Read-only dry-run; change symbols; saved plans (`-out`) |
| 04 | [Understanding the Resource Graph](./04-resource-graph.md) | DAG, implicit vs explicit deps, parallelism |
| 05 | [`terraform apply`](./05-terraform-apply.md) | Executes plan; prompt vs `-auto-approve`; saved plan; `-replace` |
| 06 | [`terraform destroy`](./06-terraform-destroy.md) | `apply -destroy`; reverse graph; only affects tracked state |
| 07 | [`terraform validate`](./07-terraform-validate.md) | Offline syntax/consistency; needs init; vs fmt vs plan |
| 08 | [The Terraform CLI](./08-terraform-cli.md) | Command anatomy; `-help`; `-install-autocomplete`; `-chdir`; single-dash flags |
| 09 | [Environment variables](./09-environment-variables.md) | `TF_VAR_*` (low precedence); `TF_LOG`/`TF_LOG_PATH`; provider creds |

## 🎯 Suggested concepts to cover

- ✅ The workflow: **Write → Plan → Apply** (and `destroy`). → card 01
- ✅ `terraform init` — downloads providers/modules, initializes the backend. Mandatory first. → card 02
- ✅ `terraform plan` — preview; `apply` — execute; `destroy` — tear down. Flags: `-auto-approve`, `-target`, `-var`, `-var-file`. → cards 03/05/06
- ✅ Saved plans: `terraform plan -out=tfplan` then `terraform apply tfplan`. → cards 03/05
- ✅ Resource graph: DAG, implicit vs explicit (`depends_on`) deps, `-parallelism`. → card 04 _(S4 lecture 30)_
- ✅ `.terraform.lock.hcl` (dependency lock file) — what it pins and why to commit it. → card 02
- ✅ `terraform validate` (syntax/consistency, **does not** contact providers). → card 07 _(S4 lecture 35)_
- ✅ CLI anatomy (`terraform <subcommand> [options]`), `-help`, `-install-autocomplete`, `-chdir`. → card 08 _(S5 CLI)_
- ✅ Environment variables: `TF_VAR_*`, `TF_LOG`/`TF_LOG_PATH`, provider creds. → card 09 _(S5 CLI)_
- ✅ `terraform fmt` (format) — lives in [02/06 HCL basics](../02-fundamentals/06-hcl-basics.md); re-shown in S5, not re-carded.
- ⬜ **Providers**: `required_providers`, version constraints (`~>`, `>=`, `=`), `alias` for multiple configs. _(not in S5 slides — expected later, likely S6/S7)_

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- plan vs apply vs refresh
- validate vs plan (what each checks)

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../02-fundamentals/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../04-configuration/README.md)
