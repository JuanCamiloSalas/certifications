[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# Cluster vs Spread vs Partition (EC2 Placement Groups)

> **Cluster** = lowest latency (one rack). **Spread** = max isolation for a few critical instances. **Partition** = fault tolerance for large distributed apps.

## Decision table

| | Cluster | Spread | Partition |
|---|---|---|---|
| Goal | Performance (latency / throughput) | Isolation (no shared hardware) | Fault tolerance at scale |
| Placement | Same AZ, same rack | Each instance on a distinct rack | Groups of racks ("partitions"), each isolated |
| AZ span | Single AZ | Multi-AZ | Multi-AZ |
| Network | Up to 10 Gbps between instances (Enhanced Networking) | Standard | Standard |
| Failure blast radius | Whole group (single rack) | 1 instance | 1 partition |
| Scale limit | Many (capacity-bound) | **7 instances per AZ** | **7 partitions per AZ**, hundreds of instances |
| Partition-aware | No | No | Yes (AWS exposes each instance's partition) |
| Typical use | HPC, tightly-coupled compute | Few critical, isolated instances | HDFS, HBase, Cassandra, Kafka |

## When the exam picks each
- **Cluster:** "lowest latency", "highest network throughput between instances", "tightly-coupled HPC".
- **Spread:** "critical instances that must NOT share hardware", "few instances, each isolated".
- **Partition:** "large distributed app", "HDFS / HBase / Cassandra / Kafka", "app already replicates data across many instances".

## Common traps
- "Low latency **AND** high availability" → Cluster gives latency but **not** HA (single rack fails → all down). If both are required, spread across AZs.
- "Few critical instances, each isolated" → **Spread**, not Partition.
- "Many instances, app that already replicates" → **Partition**, because Spread's 7-instance-per-AZ cap is too low.
- Moving an instance in/out of a placement group requires it to be **stopped** (CLI/SDK).
- For Cluster, launch all instances of the **same type, all at once**, to avoid insufficient-capacity errors.

## Linked cards
- [EC2 Placement Groups](../cards/01-ec2-saa/01-placement-groups.md)

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
