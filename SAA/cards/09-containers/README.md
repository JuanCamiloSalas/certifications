[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../08-decoupling/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../10-serverless/README.md)

# Block 09 — Containers

> **ECS, EKS, Fargate, ECR.** The exam tests launch-type decisions, not task-definition syntax.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [ECS Fundamentals](./01-ecs.md) | Cluster, task definition, service, launch types, IAM roles |
| 02 | [ECS Advanced](./02-ecs-advanced.md) | Placement strategies, auto scaling, dynamic port mapping, Fargate storage |
| 03 | [EKS](./03-eks.md) | Managed Kubernetes, node groups, Fargate on EKS, use cases |
| 04 | [ECR & Fargate](./04-ecr-fargate.md) | Image registry, vulnerability scanning, serverless containers |

## 🎯 Suggested concepts to cover

- ECS: cluster, task definition, service, task
- ECS launch types: EC2 vs Fargate
- ECS task placement strategies (binpack, random, spread)
- ECS task placement constraints
- ECS service auto scaling (CPU, memory, ALB request count)
- IAM roles for tasks (Task Role vs Task Execution Role)
- ECS + ALB: dynamic port mapping
- EKS: managed Kubernetes, use case (K8s lift & shift)
- EKS launch types: managed node groups, self-managed nodes, Fargate
- ECR: Docker image registry, IAM integration
- Fargate: serverless containers, no EC2 management

## 🔗 Related comparisons

- ECS vs EKS vs Fargate
- ECS EC2 launch type vs Fargate launch type
- ECR vs Docker Hub
- Task Role vs Task Execution Role

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../08-decoupling/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../10-serverless/README.md)
