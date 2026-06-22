[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# 🃏 SAA Deck

> Flashcards for the SAA-C03 exam. Each file is a self-contained card. Use the **Prev / Next** buttons inside every card to navigate.

## 📚 Blocks

| # | Block | Course sec. |
|---|---|---|
| 01 | [EC2 (SAA-level)](./01-ec2-saa/README.md) | 6 |
| 02 | [Storage for EC2 (EBS, EFS, Instance Store)](./02-storage-ec2/README.md) | 7 |
| 03 | [ELB & ASG](./03-elb-asg/README.md) | 8 |
| 04 | [RDS & Aurora](./04-rds-aurora/README.md) | 9 |
| 05 | [Route 53](./05-route53/README.md) | 10-11 |
| 06 | [S3 advanced](./06-s3-avanzado/README.md) | 13-15 |
| 07 | [CDN & Edge (CloudFront, Global Accelerator)](./07-cdn/README.md) | 16-17 |
| 08 | [Decoupling (SQS, SNS, Kinesis, MQ)](./08-decoupling/README.md) | 18 |
| 09 | [Containers (ECS, EKS, Fargate, ECR)](./09-containers/README.md) | 19 |
| 10 | [Serverless (Lambda, API GW, Step Functions)](./10-serverless/README.md) | 20-21 |
| 11 | [Advanced DB + Data + ML](./11-bd-data-ml/README.md) | 22-24 |
| 12 | [Monitoring (CloudWatch, CloudTrail, X-Ray)](./12-monitoring/README.md) | 25 |
| 13 | [IAM advanced](./13-iam-advanced/README.md) | 26 |
| 14 | [Security & Encryption (KMS, Secrets, WAF, Shield)](./14-security/README.md) | 27 |
| 15 | [VPC & Networking](./15-vpc/README.md) | 28 |
| 16 | [DR & Migration](./16-dr-migration/README.md) | 29 |
| 17 | [Billing & Cost Management](./17-billing-cost/README.md) | — |

## 🧭 How to navigate

- **Mobile (GitHub app):** open a block, pick any card, and use the `Prev` / `Next` buttons to walk through the whole block.
- **Desktop:** you can also open the block's README to see all its cards listed.
- **Quick search:** GitHub's file finder (`t` on desktop) — type the service name.

## ➕ How to add a new card

1. Copy [`_TEMPLATE.md`](./_TEMPLATE.md) into the matching block folder.
2. Rename: `NN-short-name.md` (NN = next number in the block).
3. Update the prev/next buttons at the top and bottom of the new card.
4. Add the new card to the block's `README.md` table.
5. If the card is inserted in the middle, also update the `next` of the previous card and the `prev` of the following card.

## 📏 Quality rules

- **Language: English only** (the exam is English-only — cards mirror it).
- One topic = one card. Never split a single topic across two cards just for length — keep it together even if the card runs long. Split only when it's genuinely two topics.
- No transcribing slides. Only non-obvious facts or things that already tricked you in a Dojo.
- **Required sections:** Pitch, "When the exam picks this", "Core" — always. Numbers / "Easily confused with" only if applicable. Traps and Diagram are optional; don't force a diagram into every card.
- **Images:** Mermaid for conceptual diagrams; for real AWS diagrams, download the file into [`../assets/`](../assets/) and link locally (no fragile external URLs).
- Long versus comparisons live in [`../comparativas/`](../comparativas/), not here.
- When a card mentions numbers (limits, timeouts, sizes), keep them in a dedicated section so they're easy to find in the final review.

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
