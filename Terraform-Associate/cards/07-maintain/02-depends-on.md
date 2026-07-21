[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-import-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-lifecycle.md)

# `depends_on` (explicit dependencies)

> **Pitch (1 line):** forces a create/destroy **order** between resources when there's **no attribute reference** to imply it — the manual fallback to Terraform's automatic dependency graph.

## 🎯 What the exam tests

- **Implicit vs explicit**: a reference like `aws_instance.web.id` creates an **implicit** dependency automatically; `depends_on` creates an **explicit** one manually.
- That `depends_on` is a **last resort** — use references whenever possible.
- The value shape: a **list of resources/modules** (`[aws_iam_role_policy.example]`), **not** attributes.

## 🧠 Core (non-obvious bits)

- Use it only for a **hidden** dependency — order matters but nothing in the config references the other resource (e.g. an app needs an IAM policy to exist first, but never reads any of its attributes). → [resource-referencing](../04-configuration/01-resource-referencing.md)
- **Takes whole objects, not attributes:** `depends_on = [aws_s3_bucket.data]`, never `aws_s3_bucket.data.arn`.
- Works on **resources, data sources, and modules**.
- **Overuse hurts:** it makes Terraform conservative — more things wait, and changes can force broader updates. Prefer implicit references.

## 💻 Syntax / Example

```hcl
resource "aws_iam_role_policy" "example" {
  # ...grants permissions the app needs, but the app never references it...
}

resource "aws_instance" "app" {
  ami           = "ami-12345"
  instance_type = "t3.micro"

  depends_on = [aws_iam_role_policy.example]   # list of RESOURCES, not attributes
}
```

## ⚠️ Common traps

- If a resource **references** another's attribute, you **don't need** `depends_on` — the reference already orders them.
- `depends_on` points at the **resource** (`aws_x.y`), never an **attribute** (`aws_x.y.id`).

## 🔄 Easily confused with

- **Implicit dependency (reference)** vs **explicit (`depends_on`)** → [resource-referencing](../04-configuration/01-resource-referencing.md)

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./01-import-block.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./03-lifecycle.md)
