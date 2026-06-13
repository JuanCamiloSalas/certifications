[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-ecs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-eks.md)

# ECS Advanced — IAM Roles, Task Placement & ALB Integration

<img src="../../assets/icons/ecs.png" width="64">

> **Pitch (1 line):** two IAM roles (Task Role vs Execution Role), task placement strategies, and dynamic port mapping with ALB are the SAA-level details that trip up candidates.

## 🎯 When the exam picks this

- "container needs to call S3 / DynamoDB" → **Task Role** (not Execution Role)
- "ECS agent needs to pull image from ECR / write CloudWatch logs" → **Task Execution Role**
- "run one task per EC2 instance" → **distinctInstance placement constraint**
- "multiple containers on the same host, ALB selects the port" → **dynamic port mapping**

## 🧠 Core (non-obvious bits)

**IAM Roles:**
- **Task Role:** assigned to the **running container** — grants the container permissions to call AWS services (S3, DynamoDB, etc.). Like an EC2 instance profile but for tasks.
- **Task Execution Role:** used by the **ECS agent** on the host — grants permission to pull images from ECR, write logs to CloudWatch, and access Secrets Manager/SSM for secrets injection. NOT the container's role.

**Task Placement (EC2 launch type only — Fargate manages placement):**
- **Strategies** (best-effort):
  - `binpack` — pack tasks as densely as possible (minimize instance count, save cost).
  - `spread` — distribute tasks evenly across AZs or instances (maximize HA).
  - `random` — random placement.
- **Constraints** (hard rules):
  - `distinctInstance` — each task must run on a different EC2 instance.
  - `memberOf` — task must run on instances matching a cluster query expression (e.g., instance type, AZ).

**Dynamic Port Mapping (EC2 + ALB):**
- Container defines a `containerPort` but leaves `hostPort` as 0. ECS assigns a random host port at runtime.
- The ALB target group discovers the actual port via ECS service registration — no static port config needed.
- Allows multiple tasks of the same service to run on the **same EC2 instance**.

## ⚠️ Common traps

- "container can't access S3" → check Task Role, not Execution Role.
- "ECS agent can't pull image from ECR" → check Task Execution Role.
- Task placement strategies are EC2 launch type only — Fargate handles its own bin-packing.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-ecs.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-eks.md)
