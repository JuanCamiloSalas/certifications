[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../06-s3-avanzado/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-cloudfront-security.md)

# CloudFront — Distributions, Cache & Origins

> **Pitch (1 line):** AWS CDN that caches content at 400+ edge locations globally, reducing latency for end users and reducing load on your origin.

## 🎯 When the exam picks this

- "globally distribute content with low latency" → **CloudFront**
- "cache static assets (images, JS, CSS) closer to users" → **CloudFront**
- "reduce load on S3 or ALB" → **CloudFront**

## 🧠 Core (non-obvious bits)

**Origins:**
- **S3 bucket** (static files, static websites) — use **Origin Access Control (OAC)** to restrict direct S3 access.
- **ALB / EC2** — must have public IPs or be reachable from CloudFront IPs.
- **Custom HTTP origin** — any HTTP server.
- **Multiple origins:** one distribution can route different paths (`/api/*` → ALB, `/static/*` → S3) via **behaviors**.

**Cache:**
- CloudFront caches based on the **Cache-Control** and **Expires** headers from the origin, plus any configured **TTL** (min/default/max).
- **Cache invalidations:** force CloudFront to fetch fresh content. You can invalidate specific paths (`/images/*`). Cost: first 1,000 invalidations/month free.
- **Cache key:** by default, the URL path. You can include query strings, headers, and cookies in the cache key (increases cache misses if too granular).

**Origin Shield:**
- Optional extra caching layer between CloudFront edge locations and your origin — reduces origin requests further.

## 🔢 Numbers to memorize

- Edge locations: **400+** worldwide
- Default TTL: **86,400s** (24h)
- Max TTL: **31,536,000s** (1 year)
- Free cache invalidations/month: **1,000 paths**

## ⚠️ Common traps

- CloudFront caches responses — if you update an S3 object, users get the cached version until TTL expires or you invalidate.
- ALB origins must be **publicly accessible** (or use PrivateLink for private ALBs — advanced setup).
- Adding too many headers/cookies to the cache key hurts cache hit rate.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../06-s3-avanzado/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-cloudfront-security.md)
