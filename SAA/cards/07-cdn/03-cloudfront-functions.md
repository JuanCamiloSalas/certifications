[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-cloudfront-security.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-global-accelerator.md)

# CloudFront Functions vs Lambda@Edge

> **Pitch (1 line):** two ways to run code at the edge — CloudFront Functions for lightweight, sub-ms request/response manipulation; Lambda@Edge for heavier logic that needs more time, memory, or external calls.

## 🎯 When the exam picks this

- "rewrite URL, add security headers, redirect at the edge" → **CloudFront Functions**
- "A/B testing, user authentication, external API call at the edge" → **Lambda@Edge**
- "run logic globally with lowest possible latency at every edge location" → **CloudFront Functions**

## 🧠 Core (non-obvious bits)

| | CloudFront Functions | Lambda@Edge |
|---|---|---|
| Runtime | JavaScript (ES5) | Node.js, Python |
| Max exec time | **< 1ms** | **5s** (viewer) / **30s** (origin) |
| Max memory | **2 MB** | **128 MB** (viewer) / **10 GB** (origin) |
| Network access | ❌ | ✅ |
| Request/Response | Viewer only | Viewer + Origin |
| Scale | Millions req/s natively | Scales but slower to provision |
| Pricing | Cheaper | More expensive |

**Trigger points (where in the CloudFront request lifecycle):**
- **Viewer request:** after CloudFront receives the request from the user — before cache check.
- **Viewer response:** before CloudFront sends the response back to the user.
- **Origin request:** before CloudFront forwards the request to the origin — only Lambda@Edge.
- **Origin response:** after CloudFront receives the response from the origin — only Lambda@Edge.

**CloudFront Functions** only run at **viewer request/response**.
**Lambda@Edge** runs at all four trigger points.

**Origin Failover:**
- Configure a **primary** and a **secondary** origin for a behavior. If the primary returns 5xx (or a configured list of error codes), CloudFront automatically retries with the secondary.
- Use case: S3 primary → S3 replica as backup.

## ⚠️ Common traps

- "make an external API call at the edge" → CloudFront Functions can't (no network); Lambda@Edge can.
- Lambda@Edge runs in the closest **regional edge cache** (not every POP), so latency is slightly higher than CloudFront Functions.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-cloudfront-security.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-global-accelerator.md)
