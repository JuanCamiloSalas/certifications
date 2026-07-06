[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-iac-benefits.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../02-fundamentals/README.md)

# Declarative vs Imperative

> **Pitch (1 line):** declarative = describe *what* the end result should be; imperative = script *how* to get there step by step.

## 🎯 What the exam tests

- That **Terraform is declarative** — you declare desired state, Terraform figures out the steps.
- Telling the two apart from a description: "Step 1 build VM, Step 2 configure, Step 3 attach network" = imperative; "I want an EC2 instance with these properties" = declarative.

## 🧠 Core (non-obvious bits)

- **Declarative:** you never write the ordering/logic; Terraform builds the dependency graph and computes the plan.
- **Imperative:** you own the sequence of commands (shell scripts, some config-mgmt playbooks).
- Because it's declarative, re-running the same config is **idempotent** — no changes if reality already matches.

## 💻 Syntax / Example

```hcl
# DECLARATIVE: state the outcome. No "create then attach then start".
resource "aws_instance" "app" {
  ami           = "ami-123456"
  instance_type = "t3.micro"
}
# vs IMPERATIVE (pseudo): run_command("create vm"); run_command("attach nic"); ...
```

## ⚠️ Common traps

- If a question describes explicit ordered steps to reach a result → that's **imperative**, NOT Terraform.
- "Desired state" is the declarative giveaway phrase.

---

[![](https://img.shields.io/badge/<_Prev-7B42BC?style=for-the-badge)](./02-iac-benefits.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-7B42BC?style=for-the-badge)](../02-fundamentals/README.md)
</content>
