[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-terraform-apply.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./07-terraform-validate.md)

# `terraform destroy`

> **Pitch (1 line):** destroys **all resources tracked in state**; it's just an apply whose plan is "delete everything" — i.e. `terraform apply -destroy`.

## 🎯 What the exam tests

- That `destroy` == **`apply -destroy`** and prompts for confirmation unless `-auto-approve`.
- That it only affects **resources in state** — never manually-created infra.
- `-target` to destroy a subset, and that it walks the graph in **reverse**.

## 🧠 Core (non-obvious bits)

- Destroys everything in the current state/config. **Equivalent to `terraform apply -destroy`.**
- **Prompts for `yes`**; **`-auto-approve`** skips it.
- Walks the dependency graph in **reverse order** (dependents die before their dependencies).
- **`-target=ADDR`** destroys only a subset — use sparingly.
- **Only manages tracked resources:** anything created outside Terraform (console, other tooling) is untouched.
- To remove a **single** resource permanently: delete/comment its block and `apply` (preferred over `destroy -target`, which leaves config intact so the next `apply` recreates it).

## 💻 Syntax / Example

```bash
terraform destroy                          # prompt then delete everything in state
terraform destroy -auto-approve            # skip the prompt (CI / ephemeral envs)
terraform destroy -target=aws_instance.web # destroy a subset only
terraform apply -destroy                   # exactly what `destroy` runs under the hood
```

## ⚠️ Common traps

- `destroy` **only touches resources in state** — it will not clean up resources you created by hand.
- `destroy -target` doesn't change config, so a later plain `apply` will **recreate** the resource — to remove it for good, edit the config.
- No undo: once approved, resources are gone (rely on state/backups, not Terraform).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./05-terraform-apply.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./07-terraform-validate.md)
