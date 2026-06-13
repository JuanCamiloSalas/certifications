[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-cloudfront.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-cloudfront-functions.md)

# CloudFront Security — OAC, Signed URLs/Cookies & Geo Restriction

<img src="../../assets/icons/cloudfront.png" width="64">

> **Pitch (1 line):** lock down who can access your CloudFront distribution — OAC restricts origin access, signed URLs/cookies gate individual files or whole sites, geo restriction blocks countries.

## 🎯 When the exam picks this

- "only allow CloudFront to access S3, not direct S3 URLs" → **Origin Access Control (OAC)**
- "give a paying user access to a specific video file" → **Signed URL**
- "give a subscriber access to all files in a premium section" → **Signed Cookie**
- "block users from a specific country" → **Geo Restriction (allowlist / blocklist)**

## 🧠 Core (non-obvious bits)

**OAC (Origin Access Control):**
- The modern replacement for OAI (Origin Access Identity — legacy).
- Grants CloudFront a special identity that S3 recognizes. The **S3 bucket policy** allows only this identity.
- Direct S3 URLs to the object are blocked (bucket is private); only the CloudFront URL works.
- OAC supports S3 SSE-KMS encryption — OAI did not.

**Signed URLs vs Signed Cookies:**

| | Signed URL | Signed Cookie |
|---|---|---|
| Scope | One specific object | Multiple objects / whole prefix |
| Use case | Single file access (download link) | Subscriber/premium area |
| URL change | Yes (query string added) | No (cookie in browser) |

- Both are generated using a **CloudFront key pair** (separate from S3 pre-signed URLs — different service, different signing key).
- Set an **expiry** on both.

**Geo Restriction:**
- **Allowlist:** only listed countries can access.
- **Blocklist:** listed countries are blocked.
- Uses a third-party geolocation database — not 100% accurate (VPNs can bypass).

## ⚠️ Common traps

- CloudFront signed URLs ≠ S3 pre-signed URLs: different signing keys, different scope.
- OAI is legacy — new architectures should use OAC.
- Geo restriction is a CloudFront-level feature; for application-level geo logic, use Lambda@Edge.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-cloudfront.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-cloudfront-functions.md)
