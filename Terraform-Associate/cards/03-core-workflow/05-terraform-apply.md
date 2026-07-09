[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./04-resource-graph.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./06-terraform-destroy.md)

# `terraform apply`

> **Pitch (1 line):** executes the plan to reach the desired state and **updates state**; it computes a fresh plan and **prompts for approval** unless you pass a saved plan or `-auto-approve`.

## 🎯 What the exam tests

- That `apply` **re-plans and prompts `yes`** by default — and how to skip it.
- The key difference between `apply` (fresh plan + prompt) and `apply tfplan` (**exact plan, no prompt, no re-diff**).
- `-auto-approve`, `-replace`, and that state is written **as it goes**.

## 🧠 Core (non-obvious bits)

- **No saved plan:** `apply` computes a new plan, shows it, and waits for you to type **`yes`**.
- **Saved plan (`terraform apply tfplan`):** applies *exactly* that plan — **no re-plan, no prompt.** Deterministic, but dangerous if the plan is stale.
- **State is updated per-resource** as they complete; if apply errors midway, state reflects what **succeeded** (partial apply) — fix and re-apply.
- **`-auto-approve`** skips the interactive `yes` (CI/CD).
- **`-replace=ADDR`** forces destroy+recreate of one resource — the modern replacement for the deprecated `terraform taint`.

## 💻 Syntax / Example

```bash
terraform apply                          # fresh plan + interactive approval
terraform apply -auto-approve            # skip the prompt (CI)
terraform apply tfplan                   # apply a saved plan (no prompt, no re-plan)
terraform apply -replace=aws_instance.web  # force recreate one resource
terraform apply -var-file=prod.tfvars    # pass variables (ignored when applying a saved plan)
```

## 🚩 Flags & values to memorize

- **`-auto-approve`** — no prompt. Applying a **saved plan file also skips the prompt** implicitly.
- **`-replace=ADDR`** — replaces `taint`/`untaint` (deprecated).
- **`-target`, `-var`, `-var-file`** — same as plan; **`-var*` are ignored** when you apply a saved plan (vars are already baked in).

## ⚠️ Common traps

- Applying a **saved plan does not prompt** — a stale plan can be applied blindly in automation.
- A partial (failed) apply leaves real resources created — re-running `apply` continues from state, it does **not** start clean.
- `-replace` is destructive by design (recreate) — check the plan first.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./04-resource-graph.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./06-terraform-destroy.md)
