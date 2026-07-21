[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-workspaces.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./07-removed-block.md)

# `moved` Block

> **Pitch (1 line):** tells Terraform you **renamed or relocated** a resource — it rewrites the **state address** to the new one **without destroying/recreating** the real infrastructure.

## 🎯 What the exam tests

- The syntax: **`moved { from = <old-addr>  to = <new-addr> }`** — both are resource **addresses**.
- That **without** a `moved` block, renaming a resource makes Terraform plan **`1 to add, 1 to destroy`** (recreate) → downtime/data loss.
- That it's the **declarative, version-controlled** replacement for `terraform state mv` — runs inside plan/apply.
- That it can move a resource **into/out of a module**, or **rename a whole module**.

## 🧠 Core (non-obvious bits)

- `from`/`to` take **resource addresses**, including module paths: `to = module.storage.aws_s3_bucket.data`, or an entire module `module.old_app → module.new_app`.
- **You must also rename the actual `resource` block** — the `moved` block only fixes the **state**; it doesn't rename anything by itself.
- **Safe plan:** with the block in place, `plan` shows a **move** (0 add / 0 destroy), not a replace.
- **Workflow:** rename the resource block → add `moved` → `plan` (validate) → `apply` (updates state) → **delete the `moved` block** afterward.
- Keep the block until every state/collaborator has applied the move; then remove it (harmless to leave).

## 💻 Syntax / Example

```hcl
# You renamed aws_instance.server  ->  aws_instance.web_server
resource "aws_instance" "web_server" {
  # ...same config as before...
}

moved {
  from = aws_instance.server
  to   = aws_instance.web_server
}

# Move a resource INTO a module:
moved {
  from = aws_s3_bucket.data
  to   = module.storage.aws_s3_bucket.data
}

# Rename an entire module:
moved {
  from = module.old_app
  to   = module.new_app
}
```

## ⚠️ Common traps

- Renaming a resource **without** a `moved` block → Terraform **destroys + recreates** it (`1 to add, 1 to destroy`).
- `moved` rewrites **state only** — you still have to rename the `resource` block itself.
- It never touches real infra; if a question says `moved` recreates/destroys, it's wrong.

## 🔄 Easily confused with

- → [moved vs removed vs import](../../comparativas/refactoring-moved-removed-import.md) · CLI equivalent `terraform state mv` in [inspecting-state](./03-inspecting-state.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-workspaces.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./07-removed-block.md)
