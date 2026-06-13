[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-organizations-scps.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-identity-center.md)

# IAM Permission Boundaries & Advanced Policy Evaluation

<img src="../../assets/icons/iam.png" width="64">

> **Pitch (1 line):** permission boundaries cap what an IAM principal can do (even if their identity policy allows more) — used to safely delegate IAM permission management without privilege escalation.

## 🎯 When the exam picks this

- "allow developers to create IAM roles, but only with limited permissions (can't create admin roles)" → **Permission Boundary**
- "what is the effective permission when multiple policies apply?" → **Policy evaluation logic**
- "delegate IAM administration without allowing privilege escalation" → **Permission Boundary**

## 🧠 Core (non-obvious bits)

**Permission Boundary:**
- An IAM managed policy attached to a **user or role** that sets the **maximum permissions** the principal can have.
- Effective permissions = **Identity Policy ∩ Permission Boundary** (both must allow).
- Does NOT grant permissions on its own — it only restricts.
- Use case: grant a developer `iam:CreateRole` but attach a boundary that prevents them from creating roles with more than read-only S3 permissions.

**Policy Evaluation Logic (simplified for exam):**

```
1. Explicit DENY anywhere → DENY (always wins)
2. AWS Organizations SCP → must allow
3. Resource-based policy → can grant access without identity policy (same account)
4. Permission Boundary → must allow (if set)
5. Session Policy → must allow (if using AssumeRole with session policies)
6. Identity Policy → must allow
→ If all pass → ALLOW
```

**Resource-based policies (same-account exception):**
- For services that support them (S3, SQS, Lambda resource policies), if the **resource-based policy** grants access to a principal in the same account, that principal can access the resource even if their identity policy doesn't explicitly allow it (implicit deny overridden by resource policy).
- Cross-account: both the resource-based policy AND the identity policy must allow.

**Session Policies:**
- Passed inline when calling `AssumeRole`. Can only restrict, not expand, the role's permissions.
- Useful for fine-grained temporary access within a session.

## ⚠️ Common traps

- Explicit DENY always wins — even if another policy allows it.
- Permission boundaries ≠ SCPs: boundaries apply to a specific user/role; SCPs apply to an entire account.
- For cross-account S3 access: both the bucket policy (resource-based) and the caller's IAM policy must allow.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-organizations-scps.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-identity-center.md)
