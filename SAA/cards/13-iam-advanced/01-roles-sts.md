[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../12-monitoring/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-federation.md)

# IAM Roles & STS — Cross-Account and Temporary Credentials

<img src="../../assets/icons/iam.png" width="64">

> **Pitch (1 line):** roles + STS provide short-lived credentials that replace long-term access keys — the foundation for secure cross-account access, EC2 instance profiles, and federated identity.

## 🎯 When the exam picks this

- "EC2 needs to access S3 without hardcoding credentials" → **IAM Role (instance profile)**
- "allow Account A to access resources in Account B" → **Cross-account IAM Role + AssumeRole**
- "issue temporary credentials with limited duration" → **STS (Security Token Service)**
- "service X needs to call another AWS service" → **IAM Role attached to the service**

## 🧠 Core (non-obvious bits)

**IAM Roles:**
- A role is an identity with a trust policy (who can assume it) and permission policies (what it can do).
- **No permanent credentials** — when assumed, STS issues temporary credentials (Access Key ID + Secret Access Key + **Session Token**).
- **Types of principals that can assume a role:**
  - AWS services (EC2, Lambda, ECS tasks…) → **service roles / instance profiles**
  - IAM users in the same or another account → **cross-account access**
  - Web identities (Cognito, Google, Facebook) → **web identity federation**
  - SAML identity providers (corporate AD) → **SAML federation**

**Instance Profile:**
- Container that holds an IAM role and attaches it to an EC2 instance.
- App code calls the **EC2 metadata endpoint** (`169.254.169.254`) → IMDSv2 returns auto-rotating temp credentials.
- Never hardcode credentials on EC2 — always use an instance profile.

**STS (Security Token Service):**
- Global service that issues temporary security credentials.
- Key API calls:
  - **`AssumeRole`** — assume a role (cross-account or same-account).
  - **`AssumeRoleWithWebIdentity`** — for web identity federation (OIDC tokens).
  - **`AssumeRoleWithSAML`** — for corporate SAML federation.
  - **`GetSessionToken`** — for MFA-protected operations (adds MFA context to session).
- Credential duration: 15 minutes to 12 hours (default 1 hour for AssumeRole).

**Cross-account access pattern:**
1. Account B creates a role with a trust policy allowing Account A's principal.
2. Account A's user/service calls `sts:AssumeRole` specifying the role ARN in Account B.
3. STS issues temp credentials scoped to Account B's role — no permanent keys needed.

## ⚠️ Common traps

- Temp credentials from STS include a **Session Token** — you need all three (Access Key ID + Secret + Session Token) to authenticate.
- The trust policy controls **who can assume** the role; the permission policy controls **what the role can do**. Both must be correct.
- Roles do NOT have passwords — only users have passwords.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../12-monitoring/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-federation.md)
