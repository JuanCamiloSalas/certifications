[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../14-security-cifrado/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../16-dr-migration/README.md)

# Block 15 — VPC & Networking

> **The biggest block in the SAA course (3h 31min).** "If you fail VPC, you fail SAA. If you master VPC, the exam is mostly secured."

## 🃏 Cards in this block

_No cards yet. Copy [`_TEMPLATE.md`](../_TEMPLATE.md) here to start._

| # | Card | Concept |
|---|---|---|

## 🎯 Suggested concepts to cover

### Foundations
- VPC, subnets (public vs private), CIDR blocks
- Route tables, main route table
- Internet Gateway (IGW)
- NAT Gateway vs NAT Instance (NAT Instance is legacy)
- Security Groups (stateful) vs Network ACLs (stateless)
- Bastion host pattern

### Endpoints & private connectivity
- VPC Endpoints: Gateway (S3, DynamoDB) vs Interface (PrivateLink)
- VPC Peering (no transitive)
- Transit Gateway (TGW): hub-and-spoke, transitive
- AWS PrivateLink
- VPN: Site-to-Site, Client VPN
- Direct Connect: dedicated vs hosted, virtual interfaces (VIFs)
- Direct Connect Gateway

### Advanced networking
- VPC Flow Logs: ACCEPT/REJECT/ALL, destinations
- IPv6 in VPC
- Egress-only Internet Gateway (IPv6 only)
- AWS Network Firewall
- Reachability Analyzer, Network Access Analyzer
- VPC sharing (with AWS Organizations / RAM)

## 🔗 Related comparisons

- Security Group vs NACL (STATEFUL vs STATELESS)
- VPC Peering vs Transit Gateway
- VPC Endpoint Gateway vs Interface
- Site-to-Site VPN vs Direct Connect
- NAT Gateway vs NAT Instance
- PrivateLink vs VPC Peering

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../14-security-cifrado/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../16-dr-migration/README.md)
