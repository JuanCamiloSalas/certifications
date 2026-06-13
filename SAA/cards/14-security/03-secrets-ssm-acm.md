[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-kms-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-waf-shield.md)

# Secrets Manager, SSM Parameter Store & ACM

<img src="../../assets/icons/secrets-manager.png" width="64">

> **Pitch (1 line):** three services for managing secrets and certificates — Secrets Manager for auto-rotating credentials, SSM Parameter Store for config/secrets at lower cost, ACM for TLS certificates.

## 🎯 When the exam picks this

- "automatically rotate RDS database password every 30 days without code changes" → **Secrets Manager**
- "store database connection strings, API keys — auto-rotation required" → **Secrets Manager**
- "store configuration values (non-secret) or secrets without rotation" → **SSM Parameter Store**
- "provision and auto-renew TLS/SSL certificates for ALB / CloudFront / API Gateway" → **ACM**

## 🧠 Core — Secrets Manager

- Stores secrets (DB passwords, API keys, OAuth tokens) encrypted with KMS.
- **Auto-rotation:** built-in rotation for RDS, Redshift, DocumentDB, and custom Lambda-based rotation for anything else. Rotation happens without downtime — new secret created and old one updated.
- Integrates natively with RDS — Lambda rotator updates the DB password and the secret in one operation.
- Cost: ~$0.40/secret/month + $0.05 per 10,000 API calls. More expensive than SSM.
- Replicate secrets across regions for multi-region apps.

## 🧠 Core — SSM Parameter Store

- Store configuration data and secrets. Hierarchical naming (e.g., `/myapp/prod/db-password`).
- Two tiers:
  - **Standard:** free, max 4 KB per parameter, no rotation.
  - **Advanced:** $0.05/parameter/month, max 8 KB, parameter policies (expiration, auto-notification).
- **SecureString type:** encrypts value with KMS — functionally similar to Secrets Manager for non-rotated secrets.
- No built-in auto-rotation — use EventBridge + Lambda if needed.

**Secrets Manager vs SSM Parameter Store:**
| | Secrets Manager | SSM Parameter Store |
|---|---|---|
| **Auto-rotation** | Built-in | Manual (custom Lambda) |
| **Cost** | ~$0.40/secret/month | Free (standard) |
| **Best for** | DB passwords, API keys (must rotate) | App config, non-rotating secrets |

## 🧠 Core — ACM (AWS Certificate Manager)

- Provision, manage, and auto-renew **TLS/SSL certificates** for use with AWS services.
- **Free** for certificates used with ALB, CloudFront, API Gateway, and other integrated services.
- **Cannot export ACM certificates** — they can only be attached to AWS services, not installed on EC2 directly. For EC2, use ACM Private CA or import your own cert.
- Public certificates auto-renew. Private CA requires ACM Private CA (paid service).

## ⚠️ Common traps

- Secrets Manager auto-rotation triggers a Lambda — if the Lambda can't reach the DB or the secret ARN is wrong, rotation fails silently.
- SSM Parameter Store doesn't natively rotate — if the exam says "automatic rotation," pick Secrets Manager.
- ACM certs are region-specific **except for CloudFront** — CloudFront requires the cert to be in **us-east-1** (N. Virginia) regardless of where the distribution is.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-kms-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-waf-shield.md)
