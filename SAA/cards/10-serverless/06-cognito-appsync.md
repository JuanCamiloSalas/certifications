[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-step-functions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)

# Cognito (User Pools vs Identity Pools) & AppSync

> **Pitch (1 line):** Cognito User Pools handle **authentication** (who are you?); Identity Pools handle **authorization** (what AWS resources can you access?). AppSync is managed GraphQL.

## 🎯 When the exam picks this

- "add sign-up / sign-in to a mobile or web app" → **Cognito User Pool**
- "users authenticated via Google/Facebook need temporary AWS credentials" → **Identity Pool**
- "API Gateway authorization with JWT from Cognito" → **User Pool authorizer**
- "managed GraphQL API" → **AppSync**

## 🧠 Core (non-obvious bits)

**Cognito User Pool (CUP):**
- A user directory — handles registration, login, MFA, password policies.
- Returns **JWT tokens** (ID token, Access token, Refresh token) on successful authentication.
- Supports **federation** with social IdPs (Google, Facebook, Apple) and enterprise IdPs (SAML, OIDC).
- Integrates natively with **API Gateway** and **ALB** as an authorizer.

**Cognito Identity Pool (CIP):**
- Takes an identity (from CUP JWT, social login, SAML, or even unauthenticated guests) and exchanges it for **temporary AWS credentials** via **STS AssumeRoleWithWebIdentity**.
- The app then calls AWS services directly using those temporary credentials.
- Use case: mobile app that needs to read from S3 or write to DynamoDB directly (not via a backend API).

**Combined flow (most common):**
```
User signs in → Cognito User Pool (JWT) → Cognito Identity Pool (swap JWT for AWS creds) → App calls S3/DynamoDB directly
```

**AppSync:**
- Managed **GraphQL** API service.
- Data sources: DynamoDB, Lambda, RDS, HTTP APIs, OpenSearch.
- Real-time subscriptions via WebSocket.
- Authorization: Cognito User Pools, API keys, IAM, OIDC.

## ⚠️ Common traps

- User Pool = authentication (login); Identity Pool = temporary AWS credentials (authorization to AWS). They solve different problems.
- "federate social login and then access S3 directly" → need **both**: User Pool (federation) → Identity Pool (creds).
- AppSync ≠ API Gateway: AppSync is specifically GraphQL; API Gateway is REST/HTTP/WebSocket.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-step-functions.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)
