[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-load-balancers.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-nlb-glb.md)

# ALB — Application Load Balancer

> **Pitch (1 line):** Layer 7 LB that routes HTTP/HTTPS by **path, host, headers, or query string** to typed target groups — the default choice for web applications.

## 🎯 When the exam picks this

- "route /api to one service, /images to another" → **path-based routing**
- "multiple domains behind one LB" → **host-based routing + SNI**
- "redirect HTTP to HTTPS at the LB" → **ALB redirect rule**
- "micro-services or containers on dynamic ports" → **ALB + ECS/dynamic port mapping**

## 🧠 Core (non-obvious bits)

- Routes to **target groups**: EC2 instances, ECS tasks, Lambda functions, private IPs — not directly to instances.
- **Routing rules** evaluated in priority order: conditions (path, host, header, query string, source IP) → actions (forward, redirect, fixed-response, authenticate).
- **SNI (Server Name Indication):** one ALB can host **multiple TLS certificates** for different domains — the client sends the hostname, ALB picks the right cert. (CLB cannot do SNI.)
- **Sticky sessions (application-based cookies):** ALB generates `AWSALB` cookie; you can also use your own app cookie. Stickiness is per target group, not per listener.
- **Client IP:** ALB terminates the connection; the backend sees the ALB's IP. Use `X-Forwarded-For`, `X-Forwarded-Port`, `X-Forwarded-Proto` to get the original client info.
- **Authentication:** native support for Cognito User Pools and OIDC providers — authenticate before forwarding.
- ALB **cannot** assign a static IP — use NLB if a fixed IP is required. (You can put a NLB in front of an ALB + assign Elastic IP to the NLB for a fixed IP with L7 routing.)

## 🔢 Numbers to memorize

- Connection draining (deregistration delay): **0–3600s** (default 300s)
- Idle timeout: default **60s**

## ⚠️ Common traps

- "static IP for whitelisting" → NOT ALB → NLB (or NLB in front of ALB).
- "WebSocket or gRPC" → ALB supports both natively.
- Sticky sessions break even distribution — only use when the app truly requires session affinity.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-load-balancers.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-nlb-glb.md)
