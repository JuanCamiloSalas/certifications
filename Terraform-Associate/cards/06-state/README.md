[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../05-modules/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)

# Block 06 — State management

> **Objetivo 6:** cómo Terraform rastrea la infra real. **Bloque crítico** — el comportamiento del state es donde más cae la gente.

## 🃏 Cards in this block

_(none yet — copy [`../_TEMPLATE.md`](../_TEMPLATE.md) to start)_

| # | Card | Concept |
|---|---|---|
| — | — | — |

## 🎯 Suggested concepts to cover

- ⬜ What `.tfstate` is and why it stores **secrets in plain text** → never commit it; use a remote backend.
- ⬜ **Local vs remote backend**; typical remote: **S3 + DynamoDB** (locking) or **HCP Terraform**.
- ⬜ **State locking** — prevents concurrent runs from corrupting state.
- ⬜ State commands: `state list`, `state show`, `state mv`, `state rm`, `state pull/push`.
- ⬜ `terraform refresh` / refresh-only plan — reconcile state with real infra (drift).
- ⬜ `terraform_remote_state` (data source) — read outputs of another state.
- ⬜ Sensitive data in state and how backends handle it (encryption at rest).
- ⬜ `terraform init -migrate-state` when switching backends.

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- Local vs remote backend
- state mv vs state rm vs import

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../05-modules/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)
