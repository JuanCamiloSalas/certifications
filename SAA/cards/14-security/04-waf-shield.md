[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-secrets-ssm-acm.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-detection-services.md)

# WAF, Shield & Firewall Manager

> **Pitch (1 line):** WAF filters malicious HTTP(S) traffic at Layer 7; Shield protects against DDoS at Layers 3/4/7; Firewall Manager centrally manages both across accounts.

## 🎯 When the exam picks this

- "block SQL injection / XSS / bad bots in web traffic" → **WAF**
- "block specific IPs or countries" → **WAF (IP set or geo match rule)**
- "rate-limit requests from a single IP" → **WAF rate-based rule**
- "protect against DDoS attacks" → **Shield Standard** (free) or **Shield Advanced** (paid)
- "manage WAF rules and Shield across all accounts in the organization" → **Firewall Manager**

## 🧠 Core — WAF (Web Application Firewall)

- Deployed in front of: **CloudFront, ALB, API Gateway, AppSync, Cognito User Pool**.
- **Web ACL:** container for rules. Each rule can ALLOW, BLOCK, or COUNT matching requests.
- **Rule types:**
  - **AWS Managed Rule Groups:** prebuilt (Core Rule Set, Known Bad Inputs, SQL Injection, etc.).
  - **Custom rules:** IP sets, geo match, string match, regex, rate-based rules.
- **Rate-based rules:** block IPs exceeding N requests per 5 minutes (DDoS mitigation + bot control).
- **WAF logs** → S3, CloudWatch Logs, or Kinesis Firehose for analysis.

## 🧠 Core — Shield

| | Shield Standard | Shield Advanced |
|---|---|---|
| **Cost** | Free (always on) | $3,000/month per org |
| **Protection** | L3/L4 DDoS (SYN floods, reflection attacks) | L3/L4 + L7, access to DDoS Response Team (DRT) |
| **Scope** | All AWS customers automatically | Opt-in for critical resources |
| **Cost protection** | None | Reimburses scaling costs from DDoS |
| **Targets** | EC2, ELB, CloudFront, Route 53 | Same + WAF, Global Accelerator |

- **Shield Advanced + WAF:** Shield Advanced can automatically create WAF rules during an L7 DDoS attack.

## 🧠 Core — Firewall Manager

- Centrally manage **WAF Web ACLs, Shield Advanced, VPC Security Groups, Network Firewall, Route 53 Resolver DNS Firewall** across all accounts in an AWS Organization.
- Requires AWS Organizations.
- **Policies** define rules and are automatically applied to all (current and future) accounts in scope.

## ⚠️ Common traps

- WAF is Layer 7 (HTTP/HTTPS) — it cannot block raw TCP/UDP floods. Use Shield or NACLs for L3/L4.
- Shield Standard is automatic and free — you don't configure it. Shield Advanced requires an explicit subscription.
- WAF on CloudFront must be in **us-east-1** — same as CloudFront certificates.
- Firewall Manager requires an Organizations management account or a delegated admin.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-secrets-ssm-acm.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-detection-services.md)
