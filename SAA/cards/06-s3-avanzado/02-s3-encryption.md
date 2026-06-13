[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-lifecycle-replication.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-s3-object-lock.md)

# S3 Encryption & Bucket Keys

> **Pitch (1 line):** five encryption options for S3 at rest — pick based on who manages the keys; Bucket Keys cut KMS API costs dramatically.

## 🎯 When the exam picks this

- "AWS manages the key, simplest setup" → **SSE-S3**
- "use my own KMS key, audit key usage" → **SSE-KMS**
- "I supply and manage the key, AWS never sees it" → **SSE-C**
- "compliance requires double encryption" → **DSSE-KMS**
- "encrypt before sending to S3, key never leaves client" → **Client-side encryption**

## 🧠 Core (non-obvious bits)

| Option | Key owner | Where encryption happens | Notes |
|---|---|---|---|
| **SSE-S3** | AWS | Server-side | Default. AES-256. Header: `x-amz-server-side-encryption: AES256` |
| **SSE-KMS** | You (CMK) | Server-side | Audit trail in CloudTrail. Header: `aws:kms`. KMS API call per object read/write. |
| **SSE-C** | You | Server-side | You send the key in every request (HTTPS mandatory). AWS never stores the key. |
| **DSSE-KMS** | You (CMK) | Server-side (double) | Two layers of KMS encryption. For strict compliance. |
| **Client-side** | You | Client-side | You encrypt before upload; S3 sees only ciphertext. |

**S3 Bucket Keys:**
- When using **SSE-KMS**, every GET/PUT calls KMS ($$). Bucket Keys create a short-lived **data key** at the bucket level — reduces KMS API calls by up to **99%** and lowers cost dramatically.
- Enabled at the bucket level. Recommended to enable for any SSE-KMS bucket with significant traffic.

**Enforcing encryption:**
- Bucket policy: deny PUT requests without the encryption header → forces encryption on all uploads.
- Default encryption: set SSE-S3 or SSE-KMS as the default — objects uploaded without a header get this encryption.

## ⚠️ Common traps

- SSE-C requires HTTPS — HTTP is rejected.
- SSE-KMS has a KMS quota limit — heavy traffic can hit it (Bucket Keys solve this).
- "client-side encryption" means AWS sees only ciphertext — even AWS cannot decrypt it.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-lifecycle-replication.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-s3-object-lock.md)
