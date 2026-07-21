[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./17-secrets-env-vars-and-external-sources.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)

# Ephemeral Values & Write-only Arguments

> **Pitch (1 line):** Terraform **1.10+** secrets that live **only in memory** — never written to state or plan — the one approach that keeps a secret **out of state**.

## 🎯 What the exam tests

- That **ephemeral values** exist only in memory during a run, are **never written to state or plan**, and are recomputed each run.
- The marker: **`ephemeral = true`** on a variable (also ephemeral outputs, and the `ephemeral` resource block type).
- That ephemeral values **cannot** be used in a normal **resource argument** (resources must persist) → that's what **write-only arguments** are for.
- **Write-only arguments**: provider-defined resource args that accept a value **without persisting** it to state/plan.

## 🧠 Core (non-obvious bits)

- **Ephemeral values** (1.10+): calculated fresh each run, flushed after use, **redacted** in CLI/HCP UI. Usable in local values, provider blocks, ephemeral resources/variables/outputs, provisioner blocks, and **write-only arguments** — but **NOT** in a managed resource's regular arguments (error: "Invalid use of ephemeral value").
- **Ephemeral resources**: a **new block type** (`ephemeral`, not `data`/`resource`), syntax nearly identical to a data source; fetches at runtime, held in memory, opened/closed during execution, **never persisted**. Use for **fetching Vault secrets, temporary credentials, dynamic tokens**.
- **Write-only arguments**: let you pass a temporary secret **into a managed resource** without it landing in state/plan. Each provider defines which args are write-only; they usually pair with a **version** argument that, when bumped, re-sends the value.
- The chain: **ephemeral resource** (fetch secret) → **write-only argument** (feed it to the resource) → secret **never touches state**. → [Vault dynamic creds](./17-secrets-env-vars-and-external-sources.md)

## 💻 Syntax / Example

```hcl
variable "db_password" {
  type      = string
  ephemeral = true          # never written to state/plan (TF 1.10+)
}

# Ephemeral resource — fetch a secret at runtime, held only in memory:
ephemeral "random_password" "db" {
  length = 20
}

# Write-only argument — value passed but NOT persisted (provider-defined):
resource "aws_db_instance" "main" {
  password_wo         = ephemeral.random_password.db.result
  password_wo_version = 1     # bump to re-send the write-only value
}
```

## 🚩 Flags & values to memorize

- **`ephemeral = true`** → variable/output value kept out of state & plan (Terraform **1.10+**).
- Ephemeral values **can't** go in normal resource args → use **write-only arguments**.
- **`ephemeral`** block ≠ `data`/`resource` — never persisted.
- Write-only args are **provider-defined**, often with a `*_version` companion.

## ⚠️ Common traps

- Putting an ephemeral value in a normal resource argument → **error** ("resource instances must persist").
- Write-only arguments exist only where the **provider** defines them — not universal.
- Ephemeral is **1.10+** — older Terraform doesn't have it.

## 🔄 Easily confused with

- → [secret protection techniques](../../comparativas/secret-protection-techniques.md) (only ephemeral/write-only protects **state**)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./17-secrets-env-vars-and-external-sources.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../05-modules/README.md)
