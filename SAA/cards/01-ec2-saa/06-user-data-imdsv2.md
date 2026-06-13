[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-ami-lifecycle.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./07-spot.md)

# EC2 User Data & IMDSv2

> **Pitch (1 line):** **User Data** bootstraps an instance on first launch (runs as root, once); **IMDSv2** is the secure way for the instance itself to query its own metadata (IP, IAM role credentials, etc.).

## 🎯 When the exam picks this

- "run a script automatically when the instance first starts" → **EC2 User Data**
- "instance needs to know its own public IP / availability zone / IAM credentials at runtime" → **Instance Metadata Service (IMDS)**
- "protect against SSRF attacks targeting the metadata endpoint" → **IMDSv2** (session-oriented)

## 🧠 Core (non-obvious bits)

**User Data:**
- Runs **once**, on **first boot only**, as the **root** user.
- To run on every boot → use a different mechanism (cron, cloud-init modules).
- Max size: **16 KB** (base64-encoded). Larger scripts → store in S3, download via User Data.
- Visible (and editable while stopped) at `http://169.254.169.254/latest/user-data`.

**IMDSv1 vs IMDSv2:**
- **IMDSv1** (old): simple GET to `http://169.254.169.254/latest/meta-data/` — no auth, vulnerable to SSRF.
- **IMDSv2** (current best practice): requires a **session token** obtained via a PUT request first; token is then passed in every metadata GET. Defeats SSRF (attacker can't forge the PUT).
- You can **enforce IMDSv2** at instance or account level (`HttpTokens = required`).
- Key metadata paths:
  - `…/meta-data/public-ipv4` — public IP
  - `…/meta-data/iam/security-credentials/<role>` — temporary IAM credentials
  - `…/meta-data/placement/availability-zone` — current AZ

## 🔢 Numbers to memorize

- User Data max size: **16 KB**
- IMDS endpoint (link-local, not routable outside the instance): **169.254.169.254**

## ⚠️ Common traps

- User Data runs **only on first launch** — changes after launch don't re-run automatically.
- IMDS is only reachable **from inside the instance** (169.254.x.x link-local). Not accessible from outside.
- IMDSv2 is NOT automatically enforced — you must explicitly set `HttpTokens = required`.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-ami-lifecycle.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./07-spot.md)
