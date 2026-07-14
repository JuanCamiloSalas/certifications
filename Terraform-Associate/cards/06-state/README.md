[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../05-modules/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)

# Block 06 — State management

> **Objetivo 6:** cómo Terraform rastrea la infra real. **Bloque crítico** — el comportamiento del state es donde más cae la gente.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Terraform State](./01-terraform-state.md) | `.tfstate` mapea config↔infra + metadata; secretos en texto plano; refresh; no funciona sin state _(S9)_ |
| 02 | [Backends & State Storage](./02-backends-and-state-storage.md) | Local vs remoto; backend en `terraform {}`; locking (`use_lockfile`, DynamoDB deprecated); `init` obligatorio _(S9)_ |
| 03 | [Inspecting State](./03-inspecting-state.md) | `state list` (direcciones) · `show` (todo) · `state show <addr>` (uno); legacy `mv`/`rm`/`pull`/`push` _(S9)_ |
| 04 | [State Drift & Refresh-Only](./04-state-drift-refresh-only.md) | Drift; revertir (`apply`) vs aceptar (`apply -refresh-only`); `plan -refresh-only`; perder el state _(S9)_ |
| 05 | [Workspaces (CLI)](./05-workspaces.md) | Varios states por config; `terraform.tfstate.d/`; `workspace list/new/select`; CLI vs HCP _(S9)_ |

> Más cards al cursar **S11** (refactoring del state: bloques `moved` / `removed` / `import`; ver también bloque `07`).

## 🎯 Suggested concepts to cover

- ✅ What `.tfstate` is and why it stores **secrets in plain text** → never commit it; use a remote backend. → card 01 _(S9)_
- ✅ **Local vs remote backend**; typical remote: **S3** (native locking) or **HCP Terraform**. → card 02 + [comparativa](../../comparativas/local-vs-remote-backend.md) _(S9)_
- ✅ **State locking** — prevents concurrent runs from corrupting state (`use_lockfile = true`; **DynamoDB deprecated**). → card 02 _(S9)_
- ✅ State commands: `state list`, `show`, `state show`, `state mv`, `state rm`, `state pull/push`. → card 03 _(S9)_
- ✅ Refresh-only mode — reconcile state with real infra (drift), revert vs accept. → card 04 _(S9)_
- ✅ **Workspaces** (CLI) — multiple states per config; `terraform.tfstate.d/`; CLI vs HCP. → card 05 + [comparativa](../../comparativas/cli-workspaces-vs-hcp-workspaces.md) _(S9)_
- ⬜ `terraform_remote_state` (data source) — read outputs of another state. _(no en S9)_
- ⬜ Sensitive data in state and how backends handle it (encryption at rest). _(tocado en cards 01/02; profundizar en S14)_
- ⬜ **State refactoring** blocks `moved` / `removed` / `import` — config-driven state ops. _(S11)_

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- Local vs remote backend
- state mv vs state rm vs import

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../05-modules/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)
