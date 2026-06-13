[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-federation.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-permission-boundaries.md)

# AWS Organizations & SCPs

<img src="../../assets/icons/organizations.png" width="64">

> **Pitch (1 line):** Organizations groups multiple AWS accounts under one management structure; SCPs are guardrails that cap the maximum permissions of every identity in an account — even root.

## 🎯 When the exam picks this

- "prevent any account in the company from launching EC2 in us-east-1" → **SCP**
- "centrally manage billing and governance for all AWS accounts" → **AWS Organizations**
- "enforce that all accounts use specific regions only" → **SCP with Deny on NotStringEquals region condition**
- "consolidated billing across many accounts" → **Organizations + master account**

## 🧠 Core (non-obvious bits)

**Structure:**
- **Management account (root):** owns the Organization, creates/invites member accounts. Cannot be restricted by SCPs.
- **Organizational Units (OUs):** group accounts. SCPs applied to an OU affect all accounts in it.
- Hierarchy: Root → OUs → Accounts. SCPs inherit down.

**Service Control Policies (SCPs):**
- JSON policies that set the **maximum permissions** allowed in an account.
- SCPs do NOT grant permissions — they only **restrict** what can be granted by IAM policies within the account.
- **Effective permissions = IAM policy ∩ SCP.** If the SCP denies it, no IAM policy can allow it.
- Applies to all IAM users, roles, and even **root user** in member accounts (but not the management account itself).
- Default: FullAWSAccess SCP — no restrictions. You must explicitly deny.

**Common SCP patterns:**
- Deny all actions outside specific regions: `Condition: aws:RequestedRegion NotIn [allowed regions]`
- Deny leaving the Organization: deny `organizations:LeaveOrganization`
- Require tags on resource creation.

**Other Organization features:**
- **Consolidated Billing:** all accounts' usage combined → volume discounts, single bill.
- **AWS Organizations + CloudTrail:** organization trail captures events from all accounts.
- **Delegated administrator:** certain services (GuardDuty, Security Hub, Macie) can be centrally managed from a designated member account.

## ⚠️ Common traps

- SCPs do NOT affect the **management account** — only member accounts.
- An SCP Allow on its own does nothing — it just sets the ceiling. The IAM policy in the account still needs to explicitly allow the action.
- Detaching the FullAWSAccess SCP from an account effectively blocks everything — the account becomes unusable.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-federation.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-permission-boundaries.md)
