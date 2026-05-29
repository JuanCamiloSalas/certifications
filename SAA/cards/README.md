[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# 🃏 SAA Deck

> Flashcards for the SAA-C03 exam. Each file is a self-contained card. Use the **Prev / Next** buttons inside every card to navigate.

## 📚 Blocks

| # | Block | Course sec. | Status |
|---|---|---|---|
| 01 | [EC2 (SAA-level)](./01-ec2-saa/) | 6 | ✅ done |
| 02 | [Storage for EC2 (EBS, EFS, Instance Store)](./02-storage-ec2/) | 7 | ✅ done |
| 03 | [ELB & ASG](./03-elb-asg/) | 8 | ✅ done |
| 04 | [RDS & Aurora](./04-rds-aurora/) | 9 | ✅ done |
| 05 | [Route 53](./05-route53/) | 10-11 | ✅ done |
| 06 | [S3 advanced](./06-s3-avanzado/) | 13-15 | ✅ done |
| 07 | [CDN & Edge (CloudFront, Global Accelerator)](./07-cdn/) | 16-17 | ✅ done |
| 08 | [Decoupling (SQS, SNS, Kinesis, MQ)](./08-decoupling/) | 18 | 🔄 in progress |
| 09 | [Containers (ECS, EKS, Fargate, ECR)](./09-containers/) | 19 | 📅 |
| 10 | [Serverless (Lambda, API GW, Step Functions)](./10-serverless/) | 20-21 | 📅 |
| 11 | [Advanced DB + Data + ML](./11-bd-data-ml/) | 22-24 | 📅 |
| 12 | [Monitoring (CloudWatch, CloudTrail, X-Ray)](./12-monitoring/) | 25 | 📅 |
| 13 | [IAM advanced](./13-iam-avanzado/) | 26 | 📅 |
| 14 | [Security & Encryption (KMS, Secrets, WAF, Shield)](./14-security-cifrado/) | 27 | 📅 |
| 15 | [VPC & Networking](./15-vpc/) | 28 | 📅 |
| 16 | [DR & Migration](./16-dr-migration/) | 29 | 📅 |

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

- A card must fit without scroll on mobile. If it grows past ~120 lines → split it.
- No transcribing slides. Only non-obvious facts or things that already tricked you in a Dojo.
- Long versus comparisons live in [`../comparativas/`](../comparativas/), not here.
- When a card mentions numbers (limits, timeouts, sizes), keep them in a dedicated section so they're easy to find in the final review.

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
