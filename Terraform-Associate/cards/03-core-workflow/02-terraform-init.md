[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-terraform-workflow.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-terraform-plan.md)

# `terraform init`

> **Pitch (1 line):** initializes the working directory — **downloads providers & modules, configures the backend, and writes the lock file**. Safe to re-run; never touches real infra.

## 🎯 What the exam tests

- That `init` is **mandatory before plan/apply**, and **what it creates** (`.terraform/`, `.terraform.lock.hcl`).
- **When you must re-run it** (new provider/module, changed backend, upgrading versions).
- The purpose of `-upgrade`, `-reconfigure`, `-migrate-state`, `-backend-config`.

## 🧠 Core (non-obvious bits)

- Downloads **providers** into `.terraform/providers/` and **modules** into `.terraform/modules/` (both are local caches — not committed).
- Creates/updates **`.terraform.lock.hcl`** — the dependency lock file pinning provider versions + checksums. **Commit it** so teammates/CI get identical versions.
- **Initializes the backend** (where state lives). Switching backend requires re-init.
- **Idempotent & safe:** makes **no changes to real infrastructure**; re-running is harmless.
- Re-run `init` after **adding a provider or module**, or **changing backend config** — otherwise you get a "provider not installed" / "backend not initialized" error.

## 💻 Syntax / Example

```bash
terraform init                          # download providers/modules, init backend
terraform init -upgrade                 # bump providers/modules to newest allowed by constraints (updates lock)
terraform init -reconfigure             # reconfigure backend, ignore saved settings
terraform init -migrate-state           # move existing state to a new backend
terraform init -backend-config=prod.tfbackend   # inject backend settings from a file
```

## 🚩 Flags & values to memorize

- **`-upgrade`** — the only way `init` will bump versions and rewrite the lock; without it, existing lock/versions are kept.
- **`-reconfigure`** vs **`-migrate-state`** — reconfigure *discards* saved backend state association; migrate *copies* existing state to the new backend.
- **`-backend-config=<file|key=value>`** — supply partial backend config at init time.
- **`-input=false`** — fail instead of prompting (CI).

## ⚠️ Common traps

- "Provider not installed" / "module not installed" → you added something and forgot to re-run `init`.
- `init` **does not apply anything** — it only prepares the directory.
- The lock file pins versions; a plain `init` **won't** upgrade past it — you need `-upgrade`.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-terraform-workflow.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-terraform-plan.md)
