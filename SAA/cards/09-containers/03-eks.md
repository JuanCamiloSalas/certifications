[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-ecs-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-ecr-fargate.md)

# Amazon EKS — Managed Kubernetes

> **Pitch (1 line):** managed **Kubernetes** control plane on AWS — use when you already run Kubernetes on-premises or need Kubernetes-native ecosystem (Helm, operators, multi-cloud portability).

## 🎯 When the exam picks this

- "lift and shift existing Kubernetes workloads to AWS" → **EKS**
- "need Kubernetes API / Helm charts / Kubernetes-native tooling" → **EKS**
- "containers, but team doesn't need Kubernetes" → **ECS** (simpler)

## 🧠 Core (non-obvious bits)

**Node (Worker) types:**
- **Managed Node Groups:** AWS provisions and manages EC2 nodes (launches, patches, scales) in an ASG. You choose instance type.
- **Self-Managed Nodes:** you create and register EC2 instances manually. Full control, full responsibility.
- **Fargate (EKS):** serverless pods — no nodes to manage. AWS handles the host for each pod.

**EKS vs ECS:**

| | ECS | EKS |
|---|---|---|
| Orchestrator | AWS-native | Kubernetes |
| Learning curve | Lower | Higher (K8s expertise required) |
| Ecosystem | AWS-centric | Kubernetes-native (Helm, operators) |
| Multi-cloud portability | ❌ | ✅ (Kubernetes everywhere) |
| Use case | New AWS-first apps | K8s lift-and-shift, multi-cloud |

**EKS Anywhere:** run EKS on your on-premises infrastructure.

**Logging / Monitoring:**
- Integrate with **CloudWatch Container Insights** for metrics and logs.
- **CloudWatch Logs** for control plane logs.

## ⚠️ Common traps

- "containers on AWS" alone is NOT enough to pick EKS — if the question doesn't mention Kubernetes or migration, default to ECS/Fargate.
- EKS Fargate doesn't support DaemonSets or privileged containers.
- EKS managed nodes still run on EC2 — you pay for the EC2 even if pods don't use all resources.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-ecs-advanced.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-ecr-fargate.md)
