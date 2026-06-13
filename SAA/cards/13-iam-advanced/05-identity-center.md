[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-permission-boundaries.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../14-security/README.md)

# IAM Identity Center & AWS Control Tower

<img src="../../assets/icons/iam-identity-center.png" width="64">

> **Pitch (1 line):** Identity Center = single-sign-on for all your AWS accounts and SAML apps from one place; Control Tower = automated multi-account setup with landing zones and guardrails.

## 🎯 When the exam picks this

- "single sign-on to multiple AWS accounts + business apps (Salesforce, Slack)" → **IAM Identity Center**
- "integrate corporate Active Directory with AWS SSO" → **IAM Identity Center + AD Connector / AWS Managed Microsoft AD**
- "automatically set up a secure multi-account environment with guardrails" → **Control Tower**
- "account vending machine — provision new accounts with pre-configured baselines" → **Control Tower**

## 🧠 Core — IAM Identity Center (formerly AWS SSO)

- **One login portal** for employees → access to any assigned AWS account + SAML-enabled apps.
- **Permission Sets:** define what access a user/group gets in an account (equivalent to IAM role). Created once, assigned to multiple accounts.
- **Identity sources:**
  - **IAM Identity Center built-in directory** — manage users/groups here directly.
  - **AWS Managed Microsoft AD** — full managed AD in AWS.
  - **AD Connector** — proxy to on-premises AD (no sync).
  - **External IdP (SAML 2.0)** — any SAML-compliant IdP (Okta, Azure AD).
- Works natively with **AWS Organizations** — assign access to OUs or individual accounts.
- Replaces the old "manual IAM role in each account" pattern for cross-account access.

## 🧠 Core — AWS Control Tower

- Sets up a **Landing Zone** — a well-architected multi-account environment in hours.
- Creates mandatory accounts: **Management**, **Log Archive**, **Audit**.
- **Guardrails:** pre-built governance rules. Two types:
  - **Preventive guardrails:** SCPs that block non-compliant actions.
  - **Detective guardrails:** AWS Config rules that detect and flag violations.
- **Account Factory:** self-service portal (or API) to provision new accounts with baselines pre-applied.
- Control Tower sits on top of Organizations — uses Organizations OUs + SCPs under the hood.

## ⚠️ Common traps

- IAM Identity Center ≠ Cognito: Identity Center = workforce SSO for employees accessing AWS/SaaS; Cognito = customer-facing app authentication.
- Control Tower ≠ Organizations: Organizations is the primitive (account grouping, billing, SCPs); Control Tower is an opinionated setup layer on top.
- Control Tower guardrails ≠ SCPs directly: preventive guardrails use SCPs, but detective ones use Config — don't confuse the enforcement mechanism.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-permission-boundaries.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../14-security/README.md)
