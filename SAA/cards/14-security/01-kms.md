[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../13-iam-advanced/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-kms-advanced.md)

# KMS — Key Management Service

<img src="../../assets/icons/kms.png" width="64">

> **Pitch (1 line):** AWS-managed encryption key store — create, control, and audit cryptographic keys used by virtually every AWS service for encryption at rest.

## 🎯 When the exam picks this

- "encrypt EBS volumes / S3 objects / RDS databases / DynamoDB" → **KMS (CMK)**
- "control who can use the encryption key" → **KMS key policy**
- "audit all key usage (who encrypted/decrypted what, when)" → **KMS + CloudTrail**
- "bring your own key material" → **KMS Customer Managed Key (CMK) with imported key material**

## 🧠 Core (non-obvious bits)

**Key types:**
| Type | Who manages it | Cost | Key rotation |
|---|---|---|---|
| **AWS Managed Key** | AWS | Free | Automatic (every year) |
| **Customer Managed Key (CMK)** | You | $1/month + API cost | Optional (auto or manual) |
| **Customer Provided Key (SSE-C)** | You (S3 only) | None | You manage externally |

**Encryption types in KMS:**
- **Symmetric (AES-256):** single key for encrypt + decrypt. Most services use this. Key never leaves KMS unencrypted.
- **Asymmetric (RSA, ECC):** public + private key pair. Public key downloadable; private key stays in KMS. Use for digital signatures or when clients outside AWS need to encrypt.

**Envelope Encryption (how KMS works at scale):**
1. KMS generates a **Data Encryption Key (DEK)** — used to encrypt your actual data (outside KMS, fast).
2. KMS encrypts the DEK with your CMK → you store the **encrypted DEK** alongside the ciphertext.
3. To decrypt: call KMS to decrypt the DEK, then decrypt data locally.
- Avoids calling KMS for every byte — only the key is sent to KMS.

**KMS Key Policy:**
- Every CMK has a key policy (like an S3 bucket policy). Without an explicit grant in the key policy, even the account root can't use the key.
- Must allow the account root or explicit IAM principals.

## 🔢 Numbers to memorize

- CMK: **$1/month** per key + **$0.03 per 10,000 API calls**
- KMS API limit: **~30,000 requests/s** (varies by region and key type — relevant for high-throughput workloads)

## ⚠️ Common traps

- KMS does NOT store your data — it only handles keys. Your data is encrypted/decrypted outside KMS using the DEK.
- AWS Managed Keys auto-rotate annually; Customer Managed Keys need rotation enabled explicitly.
- Deleting a CMK is destructive and irreversible — you lose all data encrypted under it.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../13-iam-advanced/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-kms-advanced.md)
