[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-kms.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-secrets-ssm-acm.md)

# KMS Multi-Region Keys & CloudHSM

<img src="../../assets/icons/kms.png" width="64">

> **Pitch (1 line):** multi-region KMS keys let you encrypt in one region and decrypt in another without re-encrypting; CloudHSM gives you dedicated, FIPS-validated hardware you control.

## 🎯 When the exam picks this

- "encrypt in us-east-1, decrypt in eu-west-1 without cross-region API calls" → **KMS Multi-Region Key**
- "DynamoDB Global Tables with client-side encryption, multi-region" → **KMS Multi-Region Key**
- "FIPS 140-2 Level 3 compliance / full control of HSM hardware" → **CloudHSM**
- "symmetric encryption with customer-managed HSM, no AWS access to keys" → **CloudHSM**

## 🧠 Core — KMS Multi-Region Keys

- A primary key in one region + replicas in other regions. **Same key ID, same key material** across regions.
- Can encrypt in one region and decrypt in another — no need to re-encrypt.
- Replicas are independent KMS keys — you can apply different key policies per region.
- Use cases: active-active multi-region apps, DynamoDB Global Tables with client-side encryption, Aurora Global Database encryption.

**Not the same as replicating a key:** each multi-region replica can operate independently if the primary region goes down.

## 🧠 Core — CloudHSM

- Dedicated HSM (Hardware Security Module) cluster in your VPC — AWS provisions the hardware but **you control the keys entirely**. AWS has no access.
- **FIPS 140-2 Level 3 validated** (KMS is Level 2 — CloudHSM is one level higher).
- You manage users, keys, and partitions via the HSM client or SDK.
- Supports symmetric and asymmetric keys, SSL offloading, document signing.
- High availability: deploy a cluster of HSMs across multiple AZs.
- More expensive and operationally complex than KMS — use only when regulations demand it or AWS-managed keys aren't acceptable.

**KMS vs CloudHSM comparison:**

| | KMS | CloudHSM |
|---|---|---|
| **Key management** | AWS-managed (you set policies) | You fully manage |
| **FIPS level** | 140-2 Level 2 | 140-2 Level 3 |
| **AWS access to keys** | Yes (audited) | No |
| **Cost** | $1/key/month | ~$1.45/HSM/hour |
| **Integration with AWS services** | Native, seamless | Manual (via PKCS#11 / JCE) |

## ⚠️ Common traps

- CloudHSM is NOT managed by AWS — if you lose your HSM credentials, AWS cannot recover your keys.
- KMS Multi-Region keys are NOT automatic for all KMS keys — you must create them specifically as multi-region.
- "FIPS 140-2 Level 3" → CloudHSM. "FIPS 140-2 Level 2" → KMS. The exam may test this distinction.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-kms.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-secrets-ssm-acm.md)
