[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./06-moved-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)

# `removed` Block

> **Pitch (1 line):** tells Terraform to **stop managing** a resource **without destroying it** — the declarative replacement for `terraform state rm`.

## 🎯 What the exam tests

- The syntax with **`lifecycle { destroy = false }`** — that's what keeps the real resource **running** while dropping it from state.
- That you **must also delete the `resource` block** from the config.
- The difference vs `moved`: `moved` relocates within state (still managed) · `removed` drops it from state (no longer managed).
- That plain deletion (no `removed` block) makes Terraform **destroy** the resource.

## 🧠 Core (non-obvious bits)

- **`destroy = false` is the whole point:** it says "forget this from state but **leave the real infra alone**". Without it you'd be back to destroying.
- **Two required moves:** (1) remove the `resource` block from config, (2) add a `removed` block pointing at its **old address**.
- Use it to **hand off ownership** to another team or take a critical resource under **manual control** while keeping it alive.
- Declarative equivalent of **`terraform state rm`** (which also doesn't destroy) — but version-controlled and reviewable in a PR.
- **Workflow:** delete the resource block + add `removed` → `plan` → `apply` → **delete the `removed` block** afterward.

## 💻 Syntax / Example

```hcl
# database.tf — the resource block is DELETED and replaced by:
removed {
  from = google_sql_database_instance.prd_db_1

  lifecycle {
    destroy = false   # drop from state, but KEEP the real database running
  }
}
```

## ⚠️ Common traps

- **Just deleting the `resource` block (no `removed` block) → Terraform DESTROYS it.** The `removed` block + `destroy = false` is what keeps it.
- A `removed` block while the `resource` block **still exists** is contradictory — you must remove the resource block too.
- `removed` ≠ `moved`: removed **stops management**; moved **keeps management** at a new address.

## 🔄 Easily confused with

- → [moved vs removed vs import](../../comparativas/refactoring-moved-removed-import.md) · CLI equivalent `terraform state rm` in [inspecting-state](./03-inspecting-state.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./06-moved-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../07-maintain/README.md)
