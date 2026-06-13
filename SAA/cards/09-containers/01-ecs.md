[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../08-decoupling/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-ecs-advanced.md)

# ECS — Fundamentals & Launch Types

<img src="../../assets/icons/ecs.png" width="64">

> **Pitch (1 line):** AWS's container orchestrator — define tasks, run them on EC2 (you manage servers) or Fargate (serverless, AWS manages the host) in a cluster.

## 🎯 When the exam picks this

- "run Docker containers on AWS without managing Kubernetes" → **ECS**
- "serverless containers, no EC2 to manage" → **ECS + Fargate**
- "containers on EC2 with more control over the host" → **ECS + EC2 launch type**

## 🧠 Core (non-obvious bits)

**Key concepts:**
- **Task Definition:** blueprint for your container(s) — image, CPU, memory, ports, environment variables, IAM role, logging.
- **Task:** a running instance of a task definition (like a "pod" in Kubernetes).
- **Service:** maintains a desired count of running tasks, integrates with ALB, enables auto scaling.
- **Cluster:** logical grouping of tasks/services.

**Launch Types:**

| | EC2 Launch Type | Fargate |
|---|---|---|
| Host management | You manage EC2 instances | AWS manages the host |
| Cost model | Pay for EC2 instances (even idle) | Pay per vCPU/memory per second |
| Control | More (SSH access, instance types) | Less (no access to host) |
| Use case | Long-running, cost-sensitive, GPU | Serverless, microservices, variable load |

**ECS Anywhere:** run ECS tasks on your **on-premises** servers (registers them as external instances in the cluster).

## ⚠️ Common traps

- Task Definition ≠ Service: a Task Definition is a blueprint; a Service is what runs and maintains tasks over time.
- EC2 launch type: you pay for the EC2 even if no tasks are running on it.
- Fargate doesn't support GPU workloads — use EC2 launch type for GPU.

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../08-decoupling/README.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./02-ecs-advanced.md)
