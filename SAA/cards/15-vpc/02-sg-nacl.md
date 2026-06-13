[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-vpc-foundations.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-nat-bastion.md)

# Security Groups vs NACLs

> **Pitch (1 line):** Security Groups are stateful instance-level firewalls; NACLs are stateless subnet-level firewalls — both control traffic but work at different layers and with different logic.

## 🎯 When the exam picks this

- "block a specific IP from reaching the VPC" → **NACL** (SGs don't have explicit deny)
- "allow inbound 443 without an explicit outbound rule" → **Security Group** (stateful — return traffic auto-allowed)
- "firewall at the subnet boundary" → **NACL**
- "firewall on individual EC2 instances / ENIs" → **Security Group**

## 🧠 Core (non-obvious bits)

| | Security Group | NACL |
|---|---|---|
| **Scope** | Instance / ENI | Subnet |
| **State** | **Stateful** (return traffic auto-allowed) | **Stateless** (must allow both directions) |
| **Rule types** | Allow only (no deny) | Allow and **Deny** |
| **Rule evaluation** | All rules evaluated | Rules evaluated **in order** (lowest number first) |
| **Default (custom)** | Deny all inbound, allow all outbound | Allow all inbound and outbound (rule 100 *) |
| **Association** | 1–5 SGs per ENI, 1 SG → many ENIs | 1 NACL per subnet, 1 NACL → many subnets |

**Stateful (SG) example:**
- Allow inbound port 443 → response traffic (ephemeral ports) is automatically allowed outbound. No outbound rule needed.

**Stateless (NACL) example:**
- Allow inbound port 443 → you MUST also allow outbound ephemeral ports (1024-65535) for the response to flow back.

**Ephemeral ports:**
- Clients use random high ports (1024-65535) for responses. NACLs must allow outbound traffic on this range.

**Default NACL:**
- Allows ALL inbound and outbound traffic.
- Custom NACLs start with an implicit DENY ALL — you must add explicit allow rules.

## ⚠️ Common traps

- SGs cannot deny — if you need to block a specific IP, use a NACL.
- NACL rules are numbered — a DENY at rule 100 overrides an ALLOW at rule 200 for the same traffic.
- NACLs apply at subnet boundary — traffic between instances in the same subnet bypasses NACLs.
- Ephemeral ports must be open in NACLs for stateless response traffic.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-vpc-foundations.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-nat-bastion.md)
