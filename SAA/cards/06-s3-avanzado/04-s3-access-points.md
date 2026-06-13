[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-s3-object-lock.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-s3-performance.md)

# S3 Access Points & Object Lambda

> **Pitch (1 line):** Access Points simplify per-team/per-app access control on shared buckets; Object Lambda lets you transform objects on-the-fly as they are retrieved — no copies needed.

## 🎯 When the exam picks this

- "different teams/apps need different access to the same bucket, complex bucket policy" → **S3 Access Points**
- "serve different views of the same object to different consumers (e.g., redact PII)" → **S3 Object Lambda**
- "globally distribute S3 requests across regions with a single endpoint" → **Multi-Region Access Points**

## 🧠 Core (non-obvious bits)

**S3 Access Points:**
- Each Access Point has its own **DNS hostname**, its own **access point policy** (IAM-like), and can be scoped to a specific **prefix** in the bucket.
- Simplify bucket policy management: instead of one giant bucket policy with 50 conditions, create one Access Point per team/app with its own simple policy.
- Can restrict access to a specific **VPC** (VPC-only access point) — traffic never leaves the VPC.
- The **bucket policy** must delegate control to Access Points (allow access from any access point, or specific ones).

**S3 Multi-Region Access Points:**
- Single global endpoint that routes requests to the nearest S3 bucket replica (uses AWS global accelerator backbone).
- Supports **replication** — write to one region, replicated to others. Reads served from the closest copy.
- Use case: global apps, latency reduction, cross-region failover.

**S3 Object Lambda:**
- Intercepts a GET request, sends the object through a **Lambda function** that transforms it, and returns the transformed output to the caller.
- Use cases: redact PII before returning data to analytics teams, resize images on the fly, convert formats.
- No copies of the transformed objects — all transformation is on-the-fly per request.

## ⚠️ Common traps

- Access Points don't replace bucket policies — the bucket policy must allow the access point.
- Multi-Region Access Points ≠ CloudFront — MRAP routes S3 requests; CloudFront caches content.
- Object Lambda adds Lambda invocation cost and latency per GET.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-s3-object-lock.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-s3-performance.md)
