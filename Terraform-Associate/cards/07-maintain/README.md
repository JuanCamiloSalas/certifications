[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../06-state/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../08-hcp-terraform/README.md)

# Block 07 — Maintain infrastructure

> **Objetivo 7:** mantener infra existente — import, replace, workspaces, provisioners y comandos de utilidad.

## 🃏 Cards in this block

_(none yet — copy [`../_TEMPLATE.md`](../_TEMPLATE.md) to start)_

| # | Card | Concept |
|---|---|---|
| — | — | — |

## 🎯 Suggested concepts to cover

- ⬜ `terraform import` — bring existing resources under management (and the `import` block, 1.5+).
- ⬜ `-replace=ADDR` (replaces the old `taint`/`untaint` flow) — force recreate a resource.
- ⬜ **Meta-arguments**: `count` (numeric index) vs `for_each` (map/set, stable keys); `depends_on`; `lifecycle` (`create_before_destroy`, `prevent_destroy`, `ignore_changes`).
- ⬜ **CLI workspaces** (`terraform workspace new/select/list`) — multiple states from one config. (≠ HCP workspaces.)
- ⬜ Utility commands: `terraform console`, `fmt`, `validate`, `graph`, `output`, `show`, `state`.
- ⬜ **Provisioners** (last resort): `local-exec` / `remote-exec`; creation-time vs destroy-time (`when = destroy`).

## 🔗 Related comparisons

_(create in [`../../comparativas/`](../../comparativas/) when they appear)_

- count vs for_each
- CLI workspaces vs HCP Terraform workspaces
- local-exec vs remote-exec

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../06-state/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../08-hcp-terraform/README.md)
