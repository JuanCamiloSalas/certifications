[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-waf-shield.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../15-vpc/README.md)

# Detection & Threat Security Services

<img src="../../assets/icons/guardduty.png" width="64">

> **Pitch (1 line):** four services that watch for threats without you writing queries — GuardDuty (account-level threats), Inspector (EC2/container vulnerabilities), Macie (S3 sensitive data), Detective (investigation).

## 🎯 When the exam picks this

- "detect compromised EC2 instances phoning home / unusual API calls / cryptocurrency mining" → **GuardDuty**
- "automatically scan EC2 and Lambda for OS vulnerabilities (CVEs)" → **Inspector**
- "detect PII / sensitive data stored in S3 buckets" → **Macie**
- "investigate security findings, visualize who did what and when" → **Detective**

## 🧠 Core

**GuardDuty:**
- Intelligent threat detection — analyzes **VPC Flow Logs, DNS logs, CloudTrail events** without you enabling them separately.
- Machine learning detects anomalies: unusual API calls, crypto mining, C2 callbacks, brute force, data exfiltration patterns.
- **Multi-account:** one account is the delegated admin; findings aggregated from all member accounts.
- Findings → EventBridge → trigger automated response (Lambda, SNS, Step Functions).
- Enable with one click — no agents, no log collection config needed.

**Inspector:**
- **Automated vulnerability management** for EC2 (OS packages, network reachability) and Lambda functions and container images in ECR.
- Requires the **SSM Agent** on EC2 (not a separate Inspector agent since Inspector v2).
- Continuously re-scans when new CVEs are published or software changes.
- Findings include severity (Critical/High/Medium/Low) and a remediation recommendation.
- Inspector ≠ GuardDuty: Inspector = known CVE vulnerabilities; GuardDuty = behavioral/threat anomalies.

**Macie:**
- ML-powered service that discovers and protects **sensitive data in S3** (PII, financial data, credentials, health records).
- Scans S3 buckets and classifies objects. Generates findings for exposed sensitive data.
- Useful for GDPR, HIPAA, and other compliance regimes.

**Detective:**
- **Security investigation** tool — not a detector. Aggregates and visualizes data from GuardDuty, CloudTrail, VPC Flow Logs to help you understand the root cause of a finding.
- Answers "how did this happen, what resources were involved, what was the blast radius?"

## ⚠️ Common traps

- GuardDuty and Macie are detectors, not preventers — they alert but don't block.
- Inspector is vulnerability management, not threat detection — it doesn't look for active attacks.
- Detective requires GuardDuty to be enabled (it sources findings from GuardDuty).
- "Sensitive data in S3" → Macie. "Malicious activity in account" → GuardDuty. Don't confuse them.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-waf-shield.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../15-vpc/README.md)
