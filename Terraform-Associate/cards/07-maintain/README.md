[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../06-state/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../08-hcp-terraform/README.md)

# Block 07 — Maintain infrastructure

> **Objetivo 7:** mantener infra existente — import, replace, workspaces, provisioners y comandos de utilidad.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [`import` block](./01-import-block.md) | Adopt existing infra; `to`/`id`; write resource first / `-generate-config-out`; vs `terraform import` CLI _(S11)_ |
| 02 | [`depends_on`](./02-depends-on.md) | Explicit dependency when no attribute reference; list of resources; last resort _(S13)_ |
| 03 | [`lifecycle`](./03-lifecycle.md) | `create_before_destroy` · `prevent_destroy` · `ignore_changes` · `replace_triggered_by` _(S13)_ |

> `moved` / `removed` (refactor del state) viven en el bloque **[`06-state`](../06-state/README.md)** (objetivo 6); los tres comparados en la [comparativa](../../comparativas/refactoring-moved-removed-import.md).
> **Validación** (variable validation, pre/postconditions, checks) de S13 vive en **[`04-configuration/14`](../04-configuration/14-custom-conditions-and-validation.md)** (objetivo 4 — es escribir config). `precondition`/`postcondition` se escriben dentro de `lifecycle` pero se tratan allí.

## 🎯 Suggested concepts to cover

- ✅ `terraform import` — bring existing resources under management (**`import` block** 1.5+ + CLI). → card 01 _(S11)_
- ⬜ `-replace=ADDR` (replaces the old `taint`/`untaint` flow) — force recreate a resource.
- ✅ **Meta-arguments** `depends_on` + `lifecycle` (`create_before_destroy`, `prevent_destroy`, `ignore_changes`, `replace_triggered_by`). → cards 02·03 _(S13)_ · `count`/`for_each` viven en [`04/12-13`](../04-configuration/README.md).
- ⬜ **CLI workspaces** (`terraform workspace new/select/list`) — multiple states from one config. (≠ HCP workspaces.) _(ya cardeado en [`06/05`](../06-state/05-workspaces.md))_
- ⬜ Utility commands: `terraform console`, `fmt`, `validate`, `graph`, `output`, `show`, `state`.
- ⬜ **Provisioners** (last resort): `local-exec` / `remote-exec`; creation-time vs destroy-time (`when = destroy`).

## 🔗 Related comparisons

- ✅ [moved vs removed vs import](../../comparativas/refactoring-moved-removed-import.md) — refactoring blocks + CLI vs declarative.

_(still to create in [`../../comparativas/`](../../comparativas/) when they appear)_

- count vs for_each _(ya existe: [comparativa](../../comparativas/count-vs-for-each.md))_
- CLI workspaces vs HCP Terraform workspaces _(ya existe: [comparativa](../../comparativas/cli-workspaces-vs-hcp-workspaces.md))_
- local-exec vs remote-exec

---

[![](https://img.shields.io/badge/<_Prev_block-7B42BC?style=for-the-badge)](../06-state/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../08-hcp-terraform/README.md)
