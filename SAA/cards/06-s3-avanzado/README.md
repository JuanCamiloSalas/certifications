[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../05-route53/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../07-cdn/README.md)

# Block 06 — S3 advanced

> What SAA adds on top of [CCP S3](../../../CCP/6_S3/README.md): **lifecycle, replication details, performance, encryption, access points, events**.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Lifecycle & Replication](./01-lifecycle-replication.md) | Transition rules, CRR vs SRR, delete marker replication |
| 02 | [S3 Encryption](./02-s3-encryption.md) | SSE-S3, SSE-KMS, SSE-C, DSSE-KMS, client-side, bucket keys |
| 03 | [S3 Object Lock](./03-s3-object-lock.md) | WORM, Compliance vs Governance, Glacier Vault Lock |
| 04 | [S3 Access Points](./04-s3-access-points.md) | Per-prefix/per-team policies, Multi-Region Access Points, Object Lambda |
| 05 | [S3 Performance](./05-s3-performance.md) | Multipart upload, Transfer Acceleration, byte-range fetches |
| 06 | [S3 Events & Pre-signed URLs](./06-s3-events-presigned.md) | Event notifications, EventBridge integration, pre-signed URLs |

## 🎯 Suggested concepts to cover

- Lifecycle rules: transitions vs expiration
- Replication: CRR vs SRR, requirements, replication of delete markers
- S3 Storage Lens
- S3 Analytics
- Encryption: SSE-S3, SSE-KMS, SSE-C, DSSE-KMS, client-side
- Bucket Keys (reduce KMS cost)
- S3 Object Lock + Glacier Vault Lock (WORM)
- S3 Access Points + Multi-Region Access Points
- S3 Object Lambda
- S3 Performance: multipart upload, byte-range fetches, S3 Transfer Acceleration
- Event Notifications → SNS / SQS / Lambda / EventBridge
- Requester Pays buckets
- Pre-signed URLs

## 🔗 Related comparisons

- SSE-S3 vs SSE-KMS vs SSE-C vs DSSE-KMS vs Client-side
- CRR vs SRR
- Storage classes (already in [CCP](../../../CCP/6_S3/README.md))
- Object Lock vs Vault Lock
- Multipart upload vs Transfer Acceleration

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../05-route53/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../07-cdn/README.md)
