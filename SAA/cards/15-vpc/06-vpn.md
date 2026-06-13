[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-peering-tgw.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./07-direct-connect.md)

# Site-to-Site VPN & Client VPN

> **Pitch (1 line):** Site-to-Site VPN connects your on-premises data center to AWS over encrypted IPSec tunnels in minutes; Client VPN lets individual users connect to AWS resources from any device.

## 🎯 When the exam picks this

- "quick encrypted connection from on-premises to AWS (minutes to set up)" → **Site-to-Site VPN**
- "hybrid cloud: on-prem data center + AWS VPC, encrypted over internet" → **Site-to-Site VPN**
- "remote employees need to access private VPC resources from laptops" → **Client VPN**
- "accelerate VPN over the AWS global network instead of public internet" → **Accelerated Site-to-Site VPN (Global Accelerator)**

## 🧠 Core — Site-to-Site VPN

**Components:**
- **Virtual Private Gateway (VGW):** AWS-side VPN endpoint, attached to the VPC.
- **Customer Gateway (CGW):** represents your on-premises router/firewall. Contains the public IP and routing info.
- VPN connection: creates **two IPSec tunnels** (redundancy) between VGW and CGW.

**Key characteristics:**
- Traffic goes over the **public internet** (encrypted with IPSec AES-256).
- Setup time: **minutes**.
- Bandwidth: up to **1.25 Gbps per tunnel** (limited by internet link and VGW).
- **BGP** or static routing supported.
- Can use **Transit Gateway** as the VPN attachment point for multi-VPC VPN connectivity.

**Accelerated VPN:**
- Routes VPN traffic through **AWS Global Accelerator edge locations** → less internet hops, better latency/throughput.
- Only available when attaching to a Transit Gateway (not VGW).

## 🧠 Core — AWS Client VPN

- OpenVPN-based managed VPN service.
- Endpoint deployed in your VPC. Clients (Windows/Mac/Linux) connect via OpenVPN client.
- Authentication: Active Directory, SAML IdP, or mutual certificate authentication.
- Split tunnel: route only specific traffic through VPN (not all internet traffic).
- Use case: remote workers, developers needing private VPC access.

## 🔢 Numbers to memorize

- Site-to-Site VPN: **2 tunnels** per connection (active-passive or active-active)
- Bandwidth: **~1.25 Gbps** per tunnel

## ⚠️ Common traps

- VPN is over the internet — not a private line. For dedicated private connectivity, use Direct Connect.
- VPN setup takes minutes; Direct Connect takes weeks. Exam often asks about "quick hybrid connectivity" → VPN.
- Two tunnels don't double bandwidth — they're for redundancy (active-passive by default, active-active with ECMP on TGW).

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./05-peering-tgw.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./07-direct-connect.md)
