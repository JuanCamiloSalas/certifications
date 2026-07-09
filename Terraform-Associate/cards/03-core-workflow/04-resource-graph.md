[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./03-terraform-plan.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./05-terraform-apply.md)

# Understanding the Resource Graph

> **Pitch (1 line):** Terraform builds a **dependency graph (DAG)** from resource references and walks it to decide **order** and **parallelism** — file order is irrelevant.

## 🎯 What the exam tests

- That order is decided by **dependencies, not the order you wrote blocks in**.
- **Implicit** (attribute reference) vs **explicit** (`depends_on`) dependencies — and to prefer implicit.
- That independent resources run **in parallel**, and destroy walks the graph **in reverse**.

## 🧠 Core (non-obvious bits)

- Terraform parses config + state into a **DAG**, then traverses it. Two resources with **no dependency** between them are created/destroyed **concurrently**.
- **Implicit dependency (preferred):** referencing another resource's attribute (e.g. `subnet_id = aws_subnet.a.id`) automatically orders `a` before this resource. No `depends_on` needed.
- **Explicit dependency:** use **`depends_on`** only when there's an ordering requirement but **no attribute reference** to express it (e.g. IAM policy must exist before an app runs).
- **Parallelism default = 10**; tune with **`-parallelism=n`** on plan/apply/destroy (mostly a debugging/throttling knob).
- **Destroy = reverse traversal:** dependents are destroyed before their dependencies.
- **`terraform graph`** emits the DAG in **DOT** format (pipe to Graphviz to visualize).

## 💻 Syntax / Example

```hcl
resource "aws_subnet" "a" {
  vpc_id = aws_vpc.main.id           # implicit dep: main → a
}

resource "aws_instance" "web" {
  subnet_id = aws_subnet.a.id        # implicit dep: a → web (no depends_on needed)

  depends_on = [aws_iam_role.app]    # explicit: needed, no attribute reference exists
}
```

```bash
terraform graph | dot -Tsvg > graph.svg   # visualize the DAG
terraform apply -parallelism=1             # serialize (debugging)
```

## ⚠️ Common traps

- **Don't add `depends_on` when an attribute reference already exists** — it's redundant and can over-constrain the graph.
- Reordering blocks in the file does **not** change execution order — only dependencies do.
- Overusing `depends_on` hurts parallelism (forces unnecessary serialization).

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./03-terraform-plan.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./05-terraform-apply.md)
