[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../01-ec2-saa/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../03-elb-asg/README.md)

# Block 02 — Storage for EC2

> **EBS, EFS, Instance Store, FSx.** The block with the highest density of "which storage fits this workload?" questions.

## 🃏 Cards in this block

| # | Card | Concept |
|---|---|---|
| 01 | [EBS Volume Types](./01-ebs-volume-types.md) | gp2/gp3/io1/io2/st1/sc1 · IOPS & throughput limits |
| 02 | [EBS Snapshots](./02-ebs-snapshots.md) | incremental · FSR · Archive · Recycle Bin |
| 03 | [EBS Multi-Attach](./03-ebs-multi-attach.md) | io1/io2 · same AZ · 16 instances · cluster-aware FS |
| 04 | [EBS Encryption](./04-ebs-encryption.md) | KMS · at-rest + in-transit · encrypt existing volume |
| 05 | [EFS](./05-efs.md) | NFS · Linux · multi-AZ · performance & throughput modes |
| 06 | [Instance Store](./06-instance-store.md) | max IOPS · ephemeral · survives reboot only |
| 07 | [FSx (all variants)](./07-fsx.md) | Windows / Lustre / NetApp ONTAP / OpenZFS |

## 🎯 Suggested concepts to cover

- ✅ EBS volume types (gp2 vs gp3, io1 vs io2, st1, sc1)
- ✅ EBS snapshots: incremental, cross-region copy, FSR (Fast Snapshot Restore)
- ✅ EBS Multi-Attach (io1/io2 only)
- ✅ EBS encryption in transit and at rest
- ✅ EFS: Standard vs IA, performance modes, throughput modes
- ✅ Instance Store: when and why (ephemeral)
- ✅ FSx for Windows, Lustre, NetApp ONTAP, OpenZFS
- AMI lifecycle from EBS → covered in block 01 ([card 05](../01-ec2-saa/05-ami-lifecycle.md))

## 🔗 Related comparisons

- EBS vs EFS vs Instance Store
- EFS vs FSx (variants)
- gp2 vs gp3 (when to migrate)
- FSx Lustre vs FSx for Windows vs FSx NetApp

---

[![](https://img.shields.io/badge/<_Prev_block-FF4859?style=for-the-badge)](../01-ec2-saa/README.md)
[![](https://img.shields.io/badge/Deck-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Next_block_>-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
