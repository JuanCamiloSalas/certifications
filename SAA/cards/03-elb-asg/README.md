[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)

# Block 03 — ELB & Auto Scaling Group

> **Which load balancer for which scenario** + **scaling policies**. SAA requires the ALB / NLB / GLB difference to be second nature.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Load Balancers Overview](./01-load-balancers.md) | ALB/NLB/GLB/CLB, sticky sessions, cross-zone, connection draining |
| 02 | [ALB — Application Load Balancer](./02-alb.md) | Path/host/header routing, target groups, Lambda targets |
| 03 | [NLB & GLB](./03-nlb-glb.md) | TCP/UDP, static IPs, GLB for firewall appliances |
| 04 | [ELB Features](./04-elb-features.md) | SSL/SNI, access logs, WAF integration, health checks |
| 05 | [Auto Scaling Group](./05-asg.md) | Launch templates, scaling policies, lifecycle hooks, warm pools |

## 🎯 Suggested concepts to cover

- ALB: HTTP/HTTPS, path/host-based routing, redirects, target groups
- NLB: TCP/UDP/TLS, static IP per AZ, ultra-low latency
- GLB (Gateway LB): traffic to third-party appliances (firewalls)
- CLB: legacy, almost never the right answer
- Sticky sessions (application-based cookies vs duration-based)
- Cross-Zone Load Balancing (default per LB)
- SSL/TLS termination, SNI
- Connection draining / Deregistration delay
- ASG scaling policies (target tracking, step, simple)
- ASG: launch templates vs launch configurations
- ASG lifecycle hooks
- Multi-AZ ASG behavior

## 🔗 Related comparisons

- ALB vs NLB vs GLB vs CLB
- Target tracking vs Step vs Simple scaling
- Sticky sessions: handling in ALB vs NLB

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)
