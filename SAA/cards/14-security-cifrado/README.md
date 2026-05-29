[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../13-iam-avanzado/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../15-vpc/README.md)

# Block 14 — Security & Encryption

> **KMS, Secrets Manager, Parameter Store, WAF, Shield, GuardDuty, Macie, Inspector.** The exam asks "which service detects/protects what?".

## 🃏 Cards in this block

_No cards yet. Copy [`_TEMPLATE.md`](../_TEMPLATE.md) here to start._

| # | Card | Concept |
|---|---|---|

## 🎯 Suggested concepts to cover

### Encryption & Keys
- KMS: symmetric vs asymmetric, AWS-managed vs customer-managed (CMK)
- KMS key policy and grants
- Envelope encryption, data keys
- KMS multi-region keys
- CloudHSM (dedicated, FIPS 140-2 Level 3)
- Secrets Manager: automatic rotation, RDS integration
- Systems Manager Parameter Store: hierarchy, versioning
- ACM (Certificate Manager): public vs private CA

### Perimeter protection
- WAF: web ACLs, rules, managed rule groups
- Shield Standard (free) vs Shield Advanced ($3k/month, DDoS Response Team)
- AWS Firewall Manager

### Detection
- GuardDuty (threat detection: VPC Flow Logs, DNS, CloudTrail)
- Macie (PII / sensitive data in S3)
- Inspector (vulnerabilities on EC2, ECR, Lambda)
- Detective (incident investigation)
- Security Hub (aggregator)

## 🔗 Related comparisons

- Secrets Manager vs Parameter Store
- KMS CMK vs AWS-managed key
- Shield Standard vs Advanced
- GuardDuty vs Macie vs Inspector vs Detective (you WILL confuse these)
- WAF vs Shield vs Network Firewall

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../13-iam-avanzado/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../15-vpc/README.md)
