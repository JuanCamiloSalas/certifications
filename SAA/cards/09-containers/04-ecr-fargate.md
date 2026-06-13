[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-eks.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../10-serverless/README.md)

# ECR & Fargate

<img src="../../assets/icons/ecr.png" width="64">

> **Pitch (1 line):** ECR is the managed Docker registry integrated with IAM; Fargate is the serverless compute engine that removes the need to manage any host for ECS or EKS tasks.

## 🎯 When the exam picks this

- "store and manage Docker images on AWS" → **ECR**
- "run containers without managing EC2 instances" → **Fargate**
- "scan container images for vulnerabilities" → **ECR image scanning**

## 🧠 Core (non-obvious bits)

**ECR (Elastic Container Registry):**
- **Private registry** per AWS account/region. Also has a **public gallery** (ECR Public).
- Images are backed by **S3** — stored durably, encrypted at rest.
- **IAM-based access control** — no separate login system. Authenticate with `aws ecr get-login-password`.
- **Image scanning:** basic scanning (on push, free) or **enhanced scanning** with Amazon Inspector (continuous, finds OS and package vulnerabilities).
- **Lifecycle policies:** automatically expire old images (e.g., keep only the last 10 tagged images).
- **Cross-region / cross-account replication** supported.

**Fargate:**
- Serverless compute for **ECS** (and **EKS**) — no EC2 instances to provision or manage.
- You define CPU and memory per task — Fargate provisions the right host transparently.
- Pay per **vCPU/second + GB-memory/second** consumed by your tasks (not idle capacity).
- Each Fargate task runs in its own **microVM** with an ENI — isolated at the hypervisor level.
- Supports **EFS** for persistent shared storage (S3 for object storage, no EBS attach for Fargate).

## ⚠️ Common traps

- ECS + Fargate doesn't support EBS volumes — use EFS for persistent shared storage, or ephemeral storage within the task.
- ECR lifecycle policies expire images automatically — if not set, old images accumulate and cost storage.
- ECR image push requires IAM authentication (`aws ecr get-login-password | docker login`).

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-eks.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../10-serverless/README.md)
