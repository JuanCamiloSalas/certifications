[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./06-terraform-destroy.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../04-configuration/README.md)

# `terraform validate`

> **Pitch (1 line):** checks the config is **syntactically valid and internally consistent** — **offline**: no provider/API calls, no state, no cost.

## 🎯 What the exam tests

- That `validate` checks **syntax + internal consistency** only — **not** the real world.
- That it makes **no API calls** and needs **no credentials/state**.
- That it **requires `init` first** (needs installed provider schemas), and how it differs from `fmt` and `plan`.

## 🧠 Core (non-obvious bits)

- Catches: **syntax errors, wrong argument types, missing required args, references to undeclared variables/resources.**
- Runs **fully offline** — no provider API calls, no backend/state access, no cost, no credentials.
- **Requires `terraform init` first:** it validates resource arguments against the **installed provider schemas**, so providers must already be downloaded.
- Does **NOT** catch runtime problems (a nonexistent AMI, an invalid CIDR the API rejects) — those only surface at **plan/apply**.
- **`-json`** gives machine-readable output for CI.

## 💻 Syntax / Example

```bash
terraform init        # required first — validate needs provider schemas
terraform validate    # offline syntax + consistency check
terraform validate -json   # machine-readable output (CI)
```

## 🚩 Flags & values to memorize

- **`-json`** — structured output for pipelines.
- Order matters: **`init` → `validate`** (validate fails with "provider not installed" otherwise).

## 🔄 Easily confused with

- **`fmt`** = style only (rewrites formatting). **`validate`** = correctness (offline). **`plan`** = real-world diff (reaches the cloud). → [glosario](../../glosario.md)

## ⚠️ Common traps

- `validate` passing does **not** mean `apply` will succeed — it never contacted the provider API.
- It is **not** a formatter — that's `fmt`.
- Fails before checking anything if you skipped `init`.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./06-terraform-destroy.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../04-configuration/README.md)
