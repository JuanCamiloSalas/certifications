[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-terraform-init.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-resource-graph.md)

# `terraform plan`

> **Pitch (1 line):** a **dry-run** — refreshes state, diffs desired config vs current state, and prints what it *would* create/change/destroy. Makes **no changes**.

## 🎯 What the exam tests

- That `plan` is **read-only** and refreshes state (reads real resources) before diffing.
- Reading the **change symbols** (`+ - ~ -/+`).
- **Saved plans** (`-out`) and what makes them special, plus `-target`, `-var`, `-detailed-exitcode`.

## 🧠 Core (non-obvious bits)

- Flow: **refresh state** (read real infra) → **diff** config vs state → print an **execution plan**. Never mutates infra.
- **Change symbols:**
  - `+` create · `-` destroy · `~` update in place
  - `-/+` **destroy then recreate** (replacement) · `<=` read (data source)
- **`-out=FILE`** saves the plan to disk; feeding it to `apply` guarantees Terraform applies *exactly* that plan (no re-diff, no surprises).
- **`-refresh-only`** (1.x) — plan just to detect **drift**, proposing state updates, not config changes.
- **`-target=ADDR`** narrows the plan to one resource/module — an escape hatch, not routine.

## 💻 Syntax / Example

```bash
terraform plan                          # preview against real state
terraform plan -out=tfplan              # save the plan for a deterministic apply
terraform plan -var="region=us-east-1"  # pass a variable
terraform plan -var-file=prod.tfvars    # pass a vars file
terraform plan -target=aws_instance.web # limit scope (use sparingly)
```

## 🚩 Flags & values to memorize

- **`-out=FILE`** → deterministic apply (`terraform apply FILE`).
- **`-detailed-exitcode`** → `0` = no changes, `1` = error, `2` = changes present (great for CI gates).
- **`-refresh-only`** → drift detection only.
- **`-target`, `-var`, `-var-file`** → same meaning across plan/apply/destroy.

## ⚠️ Common traps

- `plan` **does not** persist anything unless you pass `-out`; the on-screen plan is throwaway.
- A `-/+` (replace) can be destructive — read the plan, don't just approve.
- `plan` still reads real infra during refresh, so it **needs valid credentials** (unlike `validate`).

## 🔄 Easily confused with

- **`validate`** checks offline correctness (no cloud); **`plan`** computes a real-world diff. → [glosario](../../glosario.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-terraform-init.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./04-resource-graph.md)
