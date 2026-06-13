[![](https://img.shields.io/badge/<_Deck-FF4859?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)

# Block 01 — EC2 (SAA-level)

> What SAA adds on top of CCP-level EC2: **placement groups, hibernation, AMI lifecycle, advanced user data, Spot fleets**.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [Placement Groups](./01-placement-groups.md) | Cluster / Spread / Partition |
| 02 | [Instance Lifecycle & Data Persistence](./02-instance-lifecycle.md) | reboot/stop/terminate · EBS vs Instance Store |
| 03 | [Burstable (T family) & CPU Credits](./03-burstable-cpu-credits.md) | baseline/burst · Standard vs Unlimited |
| 04 | [Hibernation](./04-hibernation.md) | RAM → EBS · encrypted root · 60-day max |
| 05 | [AMI Lifecycle](./05-ami-lifecycle.md) | copy cross-region · sharing · encrypt via copy |
| 06 | [User Data & IMDSv2](./06-user-data-imdsv2.md) | bootstrap · SSRF protection · session token |
| 07 | [Spot Instances & Spot Fleet](./07-spot.md) | interruption · fleet strategies · persistent requests |
| 08 | [EC2 Image Builder](./08-image-builder.md) | automated AMI pipeline · build/test/distribute |

## 🎯 Suggested concepts to cover

- ✅ Placement groups (Cluster / Spread / Partition)
- ✅ Instance lifecycle & data persistence (reboot/stop/terminate, EBS vs Instance Store)
- ✅ Burstable T family & CPU credits (Standard vs Unlimited)
- ✅ Hibernation: requirements and use cases
- ✅ AMI: copy across regions, encryption
- ✅ EC2 user data and EC2 instance metadata service (IMDSv2)
- ✅ Spot instances + Spot fleets + Spot blocks
- ✅ EC2 Image Builder

## 🔗 Related comparisons

_(create when they appear in the deck)_

- Cluster vs Spread vs Partition placement groups
- Spot vs Reserved vs On-Demand vs Savings Plan

---

[![](https://img.shields.io/badge/<_Deck-FF4859?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
