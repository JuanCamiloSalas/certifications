[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-lambda-vpc.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-step-functions.md)

# API Gateway

> **Pitch (1 line):** managed API front-door that handles auth, throttling, caching, and routing for REST, HTTP, and WebSocket APIs — the standard front-end for serverless back-ends.

## 🎯 When the exam picks this

- "expose a Lambda function as a public HTTP endpoint" → **API Gateway + Lambda**
- "real-time two-way communication (chat, notifications)" → **API Gateway WebSocket API**
- "rate-limit API calls, protect backend from spikes" → **API Gateway throttling**
- "cache API responses to reduce Lambda invocations" → **API Gateway caching**

## 🧠 Core (non-obvious bits)

**API types:**
- **REST API:** full feature set — request/response transformation, caching, usage plans, API keys, custom domain. More expensive.
- **HTTP API:** simpler, cheaper, faster — for Lambda + OIDC/JWT auth + simple proxy. No built-in caching.
- **WebSocket API:** maintains persistent two-way connections. Routes messages by action. Stores connection IDs.

**Endpoint types (REST API):**
- **Edge-Optimized:** requests routed through CloudFront POPs — lower latency for global clients.
- **Regional:** deployed in a region, no CloudFront — you can add your own CloudFront for more control.
- **Private:** only accessible from within a VPC via a VPC Endpoint (Interface endpoint for API Gateway).

**Authorization:**
- **IAM auth:** for AWS accounts/roles calling the API (uses SigV4). Good for internal services.
- **Cognito User Pool authorizer:** validates JWT from Cognito. Good for web/mobile apps.
- **Lambda authorizer (custom):** run custom code to validate any token/header. Most flexible.

**Throttling:**
- Account-level default: **10,000 req/s** with burst of **5,000**.
- Per-stage / per-method throttling configurable.
- Returns **429 Too Many Requests** when throttled.

**Caching:**
- Cache responses for 0–3600s. Cache capacity: 0.5 GB – 237 GB.
- Clients can bypass cache with `Cache-Control: max-age=0` header (if allowed).

## ⚠️ Common traps

- HTTP API doesn't support request/response transformations or caching — use REST API if you need those.
- "WebSocket" = API Gateway WebSocket API (not NLB, not ALB).
- Lambda authorizer returns an IAM policy — API Gateway evaluates it for every request (or caches the result).

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-lambda-vpc.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-step-functions.md)
