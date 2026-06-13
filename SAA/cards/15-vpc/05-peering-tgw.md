[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-vpc-endpoints.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-vpn.md)

# VPC Peering & Transit Gateway

<img src="../../assets/icons/transit-gateway.png" width="64">

> **Pitch (1 line):** VPC Peering connects two VPCs directly (non-transitive); Transit Gateway is a managed hub that connects many VPCs and on-premises networks via a single attachment point.

## 🎯 When the exam picks this

- "connect two VPCs so resources can communicate" → **VPC Peering**
- "connect dozens of VPCs to each other and on-premises (hub-and-spoke)" → **Transit Gateway**
- "peering between different accounts or regions" → **VPC Peering** (cross-account/region supported)
- "shared services VPC accessible from many spoke VPCs" → **Transit Gateway**

## 🧠 Core — VPC Peering

- Private routing between **two VPCs** (same or different account, same or different region).
- **Non-transitive:** if A peers with B and B peers with C, A cannot reach C through B. Each pair needs its own peering connection.
- Requirements: no overlapping CIDR blocks (no re-use of the same IP range).
- Must update route tables in **both** VPCs to point the other VPC's CIDR at the peering connection.
- No bandwidth limits. Low latency. AWS backbone traffic.

**Peering limitations:**
- No edge-to-edge routing (can't use peering to route to an IGW, VPN, or Direct Connect that's in the peer VPC).
- Non-transitive by design — at scale, N VPCs require N*(N-1)/2 peering connections (O(N²) complexity).

## 🧠 Core — Transit Gateway (TGW)

- **Managed hub** — attach VPCs, VPNs, and Direct Connect gateways. All attached networks can communicate through the TGW.
- **Transitive routing:** A → TGW → B → TGW → C. No full mesh required.
- Supports:
  - **Route tables on TGW** — segment traffic (e.g., dev VPCs can't reach prod VPCs).
  - **Multicast** (only AWS service supporting this natively).
  - **Cross-region peering** (TGW to TGW peer in another region).
  - **Cross-account sharing** via AWS Resource Access Manager (RAM).
- Bandwidth: up to 50 Gbps per VPC attachment (burst).

**TGW vs VPC Peering:**
| | VPC Peering | Transit Gateway |
|---|---|---|
| **Scale** | Two VPCs | Thousands of VPCs |
| **Transitivity** | Non-transitive | Transitive |
| **Cost** | Free (data transfer costs apply) | Per attachment + per GB |
| **Complexity** | Simple (two-party) | More setup, more power |

## ⚠️ Common traps

- VPC Peering requires **non-overlapping CIDRs** — plan your IP space carefully.
- "Connect 10 VPCs" → Transit Gateway (not 45 peering connections).
- TGW is NOT free — billed per attachment-hour and per GB. For two VPCs, peering is cheaper.
- Edge-to-edge routing is not supported in peering — a peered VPC's IGW is not accessible to the other VPC.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-vpc-endpoints.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-vpn.md)
