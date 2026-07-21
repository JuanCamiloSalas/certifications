[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./14-custom-conditions-and-validation.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./16-sensitive-variables-and-outputs.md)

# Securing Secrets — where they leak & the layered defense

> **Pitch (1 line):** a secret you hand to Terraform leaks into **logs/plan output**, the **state file**, and **version control** — protect all three with layered techniques.

## 🎯 What the exam tests

- The **three leak surfaces**: logs & console output, the **state file** (plaintext JSON), and **version control** (`.tfvars`/`.tf`/git history).
- That leaking is **not a bug** — Terraform needs the value to manage infra; the goal is to *protect* it.
- That the techniques are **layers** that combine — no single one covers everything.

## 🧠 Core (non-obvious bits)

- **Where secrets end up:**
  - **Logs/Console** — `terraform plan`/`apply` output, provider error messages, CI/CD build logs, saved plan files (`-out`).
  - **State** — `terraform.tfstate` stores resource attributes as **plaintext JSON** (local or remote).
  - **Version control** — hardcoded values in `.tf`, committed `.tfvars`, and **permanent** git history.
- **The layered toolkit** (each covers a different surface):
  - **`sensitive = true`** → hides values in **output/logs** (not state). → [sensitive variables & outputs](./16-sensitive-variables-and-outputs.md)
  - **Env vars / external sources** → keep secrets out of **files/git**. → [env vars & external sources](./17-secrets-env-vars-and-external-sources.md)
  - **Ephemeral values / write-only args** → keep secrets out of **state**. → [ephemeral & write-only](./18-ephemeral-values-and-write-only-arguments.md)
  - **Remote encrypted state + access control** → protect the **state** at rest. → [securing state](../06-state/08-securing-state-files.md)
- No technique is "encryption of everything" — you stack them.

## ⚠️ Common traps

- Marking a variable `sensitive` does **not** keep it out of **state** — only out of logs.
- Env vars / external sources keep secrets out of **git**, but the value **still lands in state** (unless ephemeral/write-only).
- Committed `.tfvars` and git history are **forever** — rotate any secret that was ever committed.

## 🔄 Easily confused with

- → [secret protection techniques (what protects what)](../../comparativas/secret-protection-techniques.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./14-custom-conditions-and-validation.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./16-sensitive-variables-and-outputs.md)
