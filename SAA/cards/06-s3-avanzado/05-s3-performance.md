[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-s3-access-points.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-s3-events-presigned.md)

# S3 Performance — Multipart, Byte-Range & Transfer Acceleration

> **Pitch (1 line):** three upload/download optimizations — multipart breaks large uploads into parallel chunks, byte-range fetches parallelize downloads, and Transfer Acceleration routes uploads through CloudFront edge locations.

## 🎯 When the exam picks this

- "upload a 5 GB file reliably / in parallel" → **Multipart Upload**
- "download only part of a large file (e.g., first 100 MB)" → **Byte-Range Fetch**
- "speed up uploads from users distributed globally" → **S3 Transfer Acceleration**

## 🧠 Core (non-obvious bits)

**Multipart Upload:**
- Recommended for objects **> 100 MB**; required for objects **> 5 GB**.
- Splits the object into parts, uploads them in parallel, then S3 assembles them.
- If a part fails, only that part needs to be re-uploaded.
- Parts can be between **5 MB and 5 GB** (last part can be smaller).
- Incomplete multipart uploads accumulate charges — use a **Lifecycle rule** to abort and clean up old incomplete multipart uploads.

**Byte-Range Fetch:**
- Download a specific byte range of an object (e.g., only the first 250 bytes for a file header).
- Can parallelize downloads: split a large object into ranges and download each concurrently.
- If one range download fails, only that range is retried.

**S3 Transfer Acceleration:**
- Uploads go to the **nearest CloudFront edge location** over the public internet, then travel to S3 via AWS's private backbone network.
- Useful when users are far from the S3 bucket region.
- No change to the app code — just use the Transfer Acceleration endpoint (`.s3-accelerate.amazonaws.com`).
- Must be enabled per bucket. Small extra cost per GB transferred.

## 🔢 Numbers to memorize

- Multipart recommended: **> 100 MB**
- Multipart required: **> 5 GB**
- Single object max size in S3: **5 TB**
- S3 baseline performance: **3,500 PUT/COPY/POST/DELETE** and **5,500 GET/HEAD** per second **per prefix**.

## ⚠️ Common traps

- Multipart is an upload optimization; byte-range is a download optimization — they're complementary.
- Incomplete multipart uploads charge storage — always clean up with a lifecycle rule.
- Transfer Acceleration helps with global uploads to one region; CloudFront helps with global reads/distribution.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-s3-access-points.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-s3-events-presigned.md)
