[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../09-containers/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)

# Block 10 — Serverless

> **Lambda, API Gateway, Step Functions, AppSync.** The block with the most numeric limits to memorize (timeouts, memory, payload).

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Lambda Fundamentals](./01-lambda-fundamentals.md) | Invocation types, limits, layers, destinations, Lambda@Edge |
| 02 | [Lambda Concurrency](./02-lambda-concurrency.md) | Reserved vs provisioned, throttling, cold starts |
| 03 | [Lambda + VPC](./03-lambda-vpc.md) | ENI provisioning, internet access pattern, RDS Proxy |
| 04 | [API Gateway](./04-api-gateway.md) | REST vs HTTP vs WebSocket, endpoints, auth, throttling |
| 05 | [Step Functions](./05-step-functions.md) | Standard vs Express, states, error handling, use cases |
| 06 | [Cognito & AppSync](./06-cognito-appsync.md) | User Pools vs Identity Pools, GraphQL managed service |

## 🎯 Suggested concepts to cover

- Lambda limits (15 min timeout, 10 GB memory, 6 MB sync payload, 256 KB async, 512 MB-10 GB `/tmp` ephemeral storage)
- Lambda triggers: sync vs async vs poll-based (event source mappings)
- Lambda concurrency: reserved vs provisioned, cold starts
- Lambda destinations (success/failure)
- Lambda layers
- Lambda@Edge vs CloudFront Functions
- Lambda + VPC (ENI, scaling)
- API Gateway: REST vs HTTP vs WebSocket
- API Gateway endpoints: Edge-optimized vs Regional vs Private
- API Gateway authorization: IAM, Cognito, Lambda authorizer
- API Gateway throttling and caching
- API Gateway integrations (Lambda, HTTP, AWS service, Mock)
- Step Functions: Standard vs Express
- Step Functions: states, error handling, parallel, map
- AppSync: managed GraphQL
- Cognito User Pools vs Identity Pools

## 🔗 Related comparisons

- Lambda vs ECS Fargate vs EC2
- API Gateway REST vs HTTP vs WebSocket
- Step Functions Standard vs Express
- Lambda@Edge vs CloudFront Functions
- Cognito User Pool vs Identity Pool

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../09-containers/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../11-bd-data-ml/README.md)
