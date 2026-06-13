[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-nat-bastion.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-peering-tgw.md)

# VPC Endpoints — Gateway & Interface

<img src="../../assets/icons/privatelink.png" width="64">

> **Pitch (1 line):** VPC endpoints let EC2 and other resources access AWS services (S3, DynamoDB, etc.) privately — without traversing the internet or needing a NAT Gateway.

## 🎯 When the exam picks this

- "access S3 or DynamoDB from a private subnet without internet / NAT Gateway" → **VPC Gateway Endpoint**
- "access any other AWS service (SQS, Secrets Manager, KMS…) privately" → **VPC Interface Endpoint (PrivateLink)**
- "reduce NAT Gateway data processing costs for S3 traffic" → **Gateway Endpoint (free)**
- "private connectivity to a SaaS vendor's service in another VPC" → **PrivateLink**

## 🧠 Core (non-obvious bits)

**Two types:**

| | Gateway Endpoint | Interface Endpoint (PrivateLink) |
|---|---|---|
| **Services** | **S3 and DynamoDB only** | All other AWS services + 3rd-party SaaS |
| **How it works** | Adds a route in the route table | Creates an ENI (private IP) in your subnet |
| **Cost** | **Free** | Per hour + per GB (cost varies) |
| **DNS** | No DNS change | Creates private DNS — resolves to ENI IP |
| **Security Groups** | N/A | Can attach SGs to the ENI |
| **Scope** | VPC-wide (via route table) | Subnet-specific ENI |

**Gateway Endpoint:**
- Add a prefix list entry to the route table. Traffic to S3/DynamoDB goes via the endpoint, not the internet.
- Policy can restrict which buckets or tables are accessible through the endpoint.

**Interface Endpoint (PrivateLink):**
- Creates an ENI in your subnet with a private IP.
- Private DNS option: resolves the service's public DNS (e.g., `sqs.us-east-1.amazonaws.com`) to the private ENI IP — apps use the same endpoint URL, no code changes.
- Used for: SQS, SNS, CloudWatch, Secrets Manager, KMS, EC2 API, SSM, etc.

**PrivateLink (Endpoint Services):**
- Expose YOUR service to other VPCs via a Network Load Balancer + PrivateLink — consumers create an Interface Endpoint to reach your NLB. No VPC peering needed; traffic stays on AWS backbone.

## ⚠️ Common traps

- Gateway Endpoints are only for **S3 and DynamoDB** — everything else needs Interface Endpoints.
- Interface Endpoints cost money; Gateway Endpoints are free — prefer Gateway for S3/DynamoDB.
- DNS resolution must be enabled in the VPC (`enableDnsSupport`, `enableDnsHostnames`) for private DNS to work with Interface Endpoints.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-nat-bastion.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-peering-tgw.md)
