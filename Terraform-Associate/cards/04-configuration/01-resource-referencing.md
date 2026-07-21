[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-file-structure.md)

# Resource Referencing

> **Pitch (1 line):** reference one resource's attributes from another to share data and let Terraform build the dependency graph automatically.

## 🎯 What the exam tests

- That referencing an attribute (`aws_vpc.main.id`) creates an **implicit dependency** — no manual ordering needed.
- The address form: `<type>.<name>.<attribute>` for resources; `data.<type>.<name>.<attr>` for data sources.

## 🧠 Core (non-obvious bits)

- Referencing attributes wires resources together; Terraform infers order from the references (implicit dependency).
- Everything can reference everything: resource → resource, data → resource, variable → resource, resource → output.
- You reference **attributes** (often only known after apply, like an `id`), and Terraform sequences creation accordingly.
- Use `depends_on` only when a dependency exists but **isn't expressed** through a reference (explicit dependency).

## 💻 Syntax / Example

```hcl
resource "aws_vpc" "main" {
  cidr_block = "10.0.0.0/16"
}

resource "aws_subnet" "app" {
  vpc_id     = aws_vpc.main.id   # ← reference → implicit dependency on the VPC
  cidr_block = "10.0.1.0/24"
}

# Data source reference:
data "aws_ami" "ubuntu" { most_recent = true, owners = ["099720109477"] }

resource "aws_instance" "web" {
  ami = data.aws_ami.ubuntu.id   # ← data.<type>.<name>.<attr>
  instance_type = "t3.micro"
}
```

## ⚠️ Common traps

- A reference is an **implicit** dependency — prefer it over [`depends_on`](../07-maintain/02-depends-on.md); use `depends_on` only for hidden dependencies.
- Reference syntax has **no `${}`** in modern HCL for a bare reference — `aws_vpc.main.id`, not `"${aws_vpc.main.id}"`.

---

[![](https://img.shields.io/badge/<_Block-7B42BC?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-7B42BC?style=for-the-badge)](./02-file-structure.md)
</content>
