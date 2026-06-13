[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-nlb-glb.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-asg.md)

# ELB Cross-Features (Cross-Zone LB, SSL/SNI, Sticky Sessions, Connection Draining)

> **Pitch (1 line):** shared ELB behaviors that appear in scenario questions regardless of LB type — know the defaults and the gotchas.

## 🎯 When the exam picks this

- "uneven distribution across AZs" → enable **Cross-Zone Load Balancing**
- "multiple domains / certs on one LB" → **SNI**
- "user sessions must hit the same backend" → **sticky sessions**
- "graceful backend removal without dropping connections" → **Connection Draining**

## 🧠 Core (non-obvious bits)

**Cross-Zone Load Balancing:**
- When enabled, each LB node distributes traffic evenly across **all registered targets in all AZs**, not just its own AZ.
- Default: **ON for ALB** (free), **OFF for NLB and GLB** (costs money when enabled).

**SSL/TLS & SNI:**
- **SSL termination at the LB** decrypts traffic — backend gets plain HTTP. LB needs the cert.
- **SNI** lets one LB listener serve **multiple certs for multiple domains** using the hostname in the TLS ClientHello. Supported by ALB and NLB; NOT by CLB.
- For end-to-end encryption: terminate at LB AND re-encrypt to backend (HTTPS target group).

**Sticky Sessions (Session Affinity):**
- ALB: **application-based** (`AWSALB` or custom app cookie) or **duration-based**.
- NLB: stickiness based on source IP.
- Problem: if a target goes down, sticky users lose their session anyway.

**Connection Draining (Deregistration Delay):**
- Time the LB waits for in-flight requests to complete before deregistering an unhealthy or removed target.
- ALB/NLB: `0–3600s` (default **300s**). Set to low value if you want fast scale-in; set to 0 to skip.

## ⚠️ Common traps

- Cross-zone LB is free for ALB but costs extra for NLB — exam may test the defaults.
- Disabling sticky sessions doesn't require a restart; it takes effect for new connections.
- Connection draining is NOT the same as a health check — it's a grace period for existing connections only.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./03-nlb-glb.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./05-asg.md)
