[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Planning-175074?style=for-the-badge)](./planning_semana_final.md)

# Quiz dirigido — 40 preguntas SAA-C03 (para Gemini quiz mode)

> **INSTRUCTIONS FOR GEMINI (paste this with the questions):**
> Below are pre-written AWS Certified Solutions Architect – Associate (SAA-C03) practice questions **with their answers already provided**. Act ONLY as a quiz host: present each question one at a time exactly as written, wait for my answer, then reveal the **Answer** and the short explanation that I included. Do **not** invent new questions, do **not** rewrite these, and do **not** add long reasoning — just host the quiz and keep score. Some questions are "Select TWO".

> **Cómo usarlo:** hoy le pasas el **Set 1** (20 preguntas) y mañana el **Set 2** (20). Cada set está balanceado: Secure ×7 · Resilient ×6 · Cost ×4 · High-Performing ×3.
> Enfoque: tus dominios más débiles y de mayor peso (del folder `errors/`). Dificultad estilo TutorialsDojo, enunciados de longitud de examen real, en inglés.

---

# 🟦 SET 1 — HOY (20 preguntas)

**Q1.** A data pipeline in Account A must copy objects into an S3 bucket owned by Account B in the same AWS Organization. The security team requires access to be granted using identity-based and resource-based policies only, with no S3 ACLs. Which two actions together satisfy this? **(Select TWO)**
- A) Attach an IAM policy to the pipeline's role in Account A allowing `s3:PutObject`/`s3:GetObject` on Account B's bucket
- B) Add a bucket policy on Account B's bucket allowing the Account A role as principal
- C) Enable an S3 ACL granting the Account A canonical user write access
- D) Configure cross-region replication from Account A to Account B
- E) Use Amazon WorkDocs to share the objects

> **Answer: A & B** — Cross-account S3 = bucket policy (resource side) + IAM policy (principal side); ACLs are disallowed here.

**Q2.** A Lambda function must read and decrypt S3 objects encrypted with a customer managed KMS key. After deploying, it fails with `AccessDenied` on `kms:Decrypt`. What is the correct fix?
- A) Grant `kms:Decrypt` to the function's ARN in the KMS key policy
- B) Add `kms:Decrypt` to the Lambda execution role AND add a key policy statement granting that execution role
- C) Make the KMS key an AWS managed key
- D) Attach the decrypt permission to the S3 bucket policy

> **Answer: B** — KMS access needs the IAM role permission **and** a key policy grant; the principal is the execution role, not the function ARN.

**Q3.** A solutions architect must change permissions for 150 IAM users who all perform the same job function, applying the change to all of them without attaching the policy to each user and with the least ongoing effort. What should they do?
- A) Create an IAM role and have each user assume it
- B) Create an IAM group, add the users, and attach the policy to the group
- C) Use EventBridge Scheduler to apply the policy to each user nightly
- D) Create a permissions boundary on each user

> **Answer: B** — Managing permissions for many human users = IAM Group.

**Q4.** A web server runs in a public subnet whose network ACL denies all traffic by default. It must accept inbound HTTPS from the internet and respond correctly. Which two NACL rules are required? **(Select TWO)**
- A) Inbound allow TCP 443 from `0.0.0.0/0`
- B) Outbound allow TCP 443 to `0.0.0.0/0`
- C) Outbound allow TCP 1024-65535 to `0.0.0.0/0`
- D) Inbound allow TCP 1024-65535 from `0.0.0.0/0`
- E) No outbound rule is needed; NACLs are stateful

> **Answer: A & C** — NACLs are stateless: allow inbound 443 and the outbound ephemeral port range for the response.

**Q5.** A company serves private images from an S3 bucket through CloudFront. Objects must be retrievable only through CloudFront (never via direct S3 URLs) and only by users who have paid. Which two should they implement? **(Select TWO)**
- A) CloudFront signed URLs or signed cookies
- B) Origin Access Control (OAC) restricting the bucket to the distribution
- C) An S3 presigned URL handed to each user
- D) Enable S3 Transfer Acceleration
- E) A CloudFront function that rewrites the path

> **Answer: A & B** — OAC locks the origin to CloudFront; signed URLs/cookies control who may request. Presigned URLs are the S3-direct mechanism.

**Q6.** An enterprise with an existing on-premises Microsoft Active Directory wants employees to sign in once and access multiple AWS accounts in its Organization using their corporate credentials, with the least administrative overhead. What should the architect deploy?
- A) Separate IAM users in each account, federated manually
- B) IAM Identity Center integrated with AD Connector to the on-prem AD
- C) Amazon Cognito user pools for each account
- D) A SAML app per account in the on-prem AD only

> **Answer: B** — IAM Identity Center + AD Connector gives SSO across accounts reusing the corporate directory.

**Q7.** A central platform team must let business units create new AWS accounts that automatically come with pre-approved guardrails, logging, and baseline security, with minimal effort. Which service best fits?
- A) AWS Resource Access Manager (RAM)
- B) AWS Config aggregator
- C) AWS Control Tower with a Landing Zone
- D) AWS Service Catalog products only

> **Answer: C** — Control Tower Landing Zone provisions governed accounts with built-in guardrails/baselines.

**Q8.** An application connects to an RDS MySQL Multi-AZ database using its endpoint. During an AZ failure, which statement about connectivity is correct?
- A) The primary's IP address is reassigned to the application automatically
- B) The DNS CNAME endpoint is repointed to the standby; the app reconnects using the same endpoint
- C) The standby becomes readable and the app must switch to a new read endpoint
- D) The app must update its connection string to the standby's IP

> **Answer: B** — Multi-AZ failover flips the DNS CNAME to the standby; the endpoint stays the same. The standby is not readable.

**Q9.** A reporting workload is overwhelming a production RDS PostgreSQL instance with heavy read queries, degrading transactions. The team needs to offload reads without affecting writes, accepting slight replication lag. What should they add?
- A) Convert the instance to Multi-AZ
- B) Add one or more Read Replicas and point reporting at them
- C) Enable storage autoscaling
- D) Increase the backup retention period

> **Answer: B** — Read Replicas (async) scale reads; Multi-AZ is for HA and its standby isn't readable.

**Q10.** A compliance policy requires database backups retained for 90 days. The team currently relies on RDS automated backups. What is the correct approach?
- A) Set the automated backup retention to 90 days
- B) Use an AWS Backup plan with a 90-day retention rule
- C) Enable Multi-AZ to keep backups longer
- D) Take a single manual snapshot and rely on it

> **Answer: B** — Automated backups cap at 35 days; for longer retention use AWS Backup (or scheduled manual snapshots).

**Q11.** A production MySQL RDS instance keeps running low on disk during traffic spikes, risking an outage. The team wants storage to grow automatically with the least effort and no performance impact. What should they enable?
- A) Manually increase allocated storage each time
- B) Switch to Provisioned IOPS storage
- C) Enable RDS storage autoscaling with a maximum threshold
- D) Change the storage engine to MyISAM

> **Answer: C** — Storage autoscaling grows the volume automatically up to a max, with no downtime.

**Q12.** A company must migrate a 2 TB on-prem Oracle database to Amazon RDS with the absolute minimum downtime; the source stays in use until cutover. Which approach fits?
- A) Snapshot and restore into RDS
- B) AWS DMS with full load plus change data capture (CDC)
- C) Export to S3 and import during a maintenance window
- D) Use AWS DataSync to copy the data files

> **Answer: B** — DMS full load + CDC keeps source and target in sync for near-zero-downtime cutover.

**Q13.** An organization reaches AWS over Direct Connect for on-prem core services. It is adding several new AWS accounts that all need consistent, dedicated private connectivity with the least overhead. What should the architect use?
- A) A separate Direct Connect circuit per account
- B) Direct Connect Gateway with VPC peering between all accounts
- C) Direct Connect Gateway plus a Transit Gateway shared across the accounts
- D) Site-to-Site VPN CloudHub

> **Answer: C** — DX Gateway + Transit Gateway scales shared DX to many accounts/VPCs; VPC peering isn't transitive.

**Q14.** Finance wants to break down the monthly AWS bill by department and project to charge costs back internally. Which capability should be configured?
- A) AWS Budgets with SNS alerts
- B) Cost Allocation Tags activated in the billing console
- C) AWS Compute Optimizer
- D) Trusted Advisor cost checks

> **Answer: B** — Cost Allocation Tags categorize spend by dept/project; Budgets only alert.

**Q15.** A platform team needs to programmatically retrieve historical cost data and forecast future spend to feed an internal dashboard, with the least operational overhead. What should they use?
- A) AWS Budgets with an SQS integration
- B) The AWS Cost Explorer API with pagination
- C) Download monthly CSV billing reports and parse them
- D) Athena over raw CUR files built from scratch

> **Answer: B** — Cost Explorer API gives programmatic cost data and forecasting directly.

**Q16.** A company decommissioned EC2 workloads covered by Standard Reserved Instances. They want to stop incurring charges ASAP and recover cost. Which two actions help? **(Select TWO)**
- A) Stop the instances; RI billing ends immediately
- B) Terminate the instances to end on-demand usage
- C) Sell the unused Reserved Instances on the AWS Reserved Instance Marketplace
- D) List the instances for sale on Amazon.com
- E) Cancel the entire AWS account subscription

> **Answer: B & C** — Stopping does not end RI billing; terminate and recover cost by selling the RIs on the RI Marketplace.

**Q17.** Archived data in S3 Glacier Flexible Retrieval must be retrievable in under 15 minutes at any time, sustaining up to 150 MB/s of retrieval throughput. Which two should be configured? **(Select TWO)**
- A) Use Expedited retrievals
- B) Use Bulk retrievals
- C) Purchase provisioned retrieval capacity
- D) Use Standard retrievals
- E) Move the data to S3 Glacier Deep Archive

> **Answer: A & C** — Expedited gives 1-5 min retrieval; provisioned retrieval capacity guarantees Expedited throughput on demand.

**Q18.** A DynamoDB-backed application has read-heavy traffic with repeated reads of the same hot items, microsecond-latency requirements, and occasional throttling during spikes. Which two improve performance cost-effectively? **(Select TWO)**
- A) Add a DynamoDB Accelerator (DAX) cluster for the hot reads
- B) Enable Auto Scaling / raise provisioned capacity for the table
- C) Rely on auto scaling, which is already on by default
- D) Run ElastiCache on each client device
- E) Switch the table to a relational engine

> **Answer: A & B** — DAX gives microsecond cached reads; auto scaling/higher capacity handles throughput. Auto scaling is NOT on by default for provisioned tables.

**Q19.** An application must return only a filtered, redacted subset of a large CSV object in S3 to different callers, without downloading or duplicating the whole object. Which is the most efficient solution?
- A) S3 Object Lambda that transforms the object on GET, keyed by bucket and object key
- B) A nightly Glue job writing filtered copies
- C) S3 Select run by each client with no transformation logic
- D) CloudFront with a caching policy

> **Answer: A** — S3 Object Lambda transforms data on GET (by bucket + object key) without storing copies.

**Q20.** A company hosts many distinct domains (different root domains) behind a single Application Load Balancer and wants to add new domains over time without re-issuing one certificate each time. What should they do?
- A) Use one wildcard certificate on the listener
- B) Put CloudFront with a dedicated IP in front
- C) Use a single SAN certificate and re-issue it whenever a domain is added
- D) Upload multiple ACM certificates bound to the same HTTPS listener; the ALB selects the cert per client using SNI

> **Answer: D** — SNI lets one ALB listener host multiple certs and pick per hostname; wildcard only covers sub-domains of one domain, SAN needs re-issuing.

---

# 🟩 SET 2 — MAÑANA (20 preguntas)

**Q21.** A security team must guarantee that no one in specific member accounts of an AWS Organization can disable CloudTrail or leave the organization, even with full administrator IAM permissions in those accounts. What should they use?
- A) An IAM policy in each account denying the actions
- B) A Service Control Policy (SCP) attached to the relevant OU
- C) A permissions boundary on every role
- D) AWS Config rules that re-enable CloudTrail

> **Answer: B** — SCPs set the maximum permissions across accounts/OUs and override account-level admin.

**Q22.** An application needs to store database connection strings and a few API keys encrypted at rest and retrieve them at runtime, at the lowest cost, with no automatic rotation requirement. What should the architect choose?
- A) AWS Secrets Manager with rotation enabled
- B) SSM Parameter Store SecureString parameters encrypted with KMS
- C) Hard-code them in environment variables
- D) Store them in an encrypted DynamoDB table

> **Answer: B** — Parameter Store SecureString + KMS is cheaper than Secrets Manager when automatic rotation isn't needed.

**Q23.** A client uploads objects to S3 and wants S3 to manage the encryption keys (no customer-supplied keys). Which request header indicates server-side encryption with S3-managed or KMS keys?
- A) `x-amz-server-side-encryption`
- B) `x-amz-server-side-encryption-customer-key`
- C) `x-amz-server-side-encryption-customer-algorithm`
- D) `x-amz-acl`

> **Answer: A** — `x-amz-server-side-encryption` is for SSE-S3/SSE-KMS; the `-customer-*` headers are only for SSE-C (customer-provided keys).

**Q24.** A compliance requirement mandates that the KMS key material for data at rest be rotated automatically every year while keeping older data decryptable. What should the team enable?
- A) Manually create a new key every year and re-encrypt all data
- B) Enable automatic key rotation on the customer managed KMS key
- C) Delete and recreate the key annually
- D) Switch to SSE-C

> **Answer: B** — Automatic key rotation rotates the backing key material yearly while old data stays decryptable via retained key versions.

**Q25.** An EC2 instance's security group allows inbound TCP 443 from the internet but has no outbound rules except the default allow-all. A client makes an HTTPS request. Will the response reach the client, and why?
- A) No — an outbound rule for the ephemeral port is required
- B) Yes — security groups are stateful, so return traffic for an allowed inbound connection is automatically permitted
- C) No — security groups are stateless
- D) Yes — but only if a NACL ephemeral rule exists

> **Answer: B** — SGs are stateful; return traffic for an allowed connection is automatically permitted. (A NACL, being stateless, would need the ephemeral rule — but that's not what's asked.)

**Q26.** A company running Amazon EKS must encrypt Kubernetes secrets stored in etcd using envelope encryption with keys they control, to meet a compliance audit. What should they configure?
- A) Enable EKS secrets envelope encryption using a customer managed KMS key
- B) Store secrets in plaintext ConfigMaps
- C) Use SSE-S3 on the cluster
- D) Enable CloudHSM for the worker nodes

> **Answer: A** — EKS supports envelope encryption of Kubernetes secrets in etcd with a KMS key.

**Q27.** A team needs a cross-region read replica of an encrypted RDS database for disaster recovery. What is true about encryption for the replica?
- A) The replica cannot be encrypted in another region
- B) The cross-region replica is encrypted, using a KMS key in the destination region
- C) Encryption must be disabled on the source first
- D) The replica shares the exact same key ARN as the source region

> **Answer: B** — Replicas of an encrypted DB are encrypted; a cross-region replica uses a KMS key in the destination region (KMS keys are regional).

**Q28.** A multi-region application must serve traffic from all regions simultaneously and automatically stop sending traffic to a region that becomes unhealthy, maximizing fault tolerance. Which Route 53 configuration fits best?
- A) Active-passive failover routing
- B) Active-active using a weighted routing policy with health checks
- C) Simple routing with multiple values
- D) Geolocation routing with a single default record

> **Answer: B** — All regions serving + auto-drop unhealthy = active-active (weighted/multivalue) with health checks; failover keeps a standby idle.

**Q29.** A financial application needs a database spanning two regions for DR, with sub-second replication lag and the ability to promote a secondary region in under a minute (very low RPO/RTO). Which should the architect choose?
- A) RDS Multi-AZ
- B) Aurora Global Database
- C) A cross-region RDS read replica
- D) DynamoDB global tables

> **Answer: B** — Aurora Global Database gives cross-region replication (~1s lag) and fast (<1 min) region promotion for DR.

**Q30.** An application must remain fully available even if one Availability Zone fails, requiring at least 6 healthy instances at all times across 3 AZs. How should the Auto Scaling Group be configured for HA at the lowest risk?
- A) Desired 6 across 1 AZ
- B) Desired 9 spread across 3 AZs so 6 remain if one AZ fails
- C) Desired 6 across 2 AZs
- D) Desired 3 across 3 AZs

> **Answer: B** — To keep 6 after losing one of 3 AZs, run 9 (3 per AZ) so a full AZ loss still leaves 6.

**Q31.** A team must automate the creation and retention of EBS snapshots on a daily schedule with tag-based targeting and the least operational overhead. Which service should they use?
- A) AWS Backup with a custom Lambda
- B) Amazon Data Lifecycle Manager (DLM)
- C) A cron job on each EC2 instance
- D) CloudWatch Events invoking manual snapshots

> **Answer: B** — DLM automates EBS snapshot creation/retention by tags with minimal effort.

**Q32.** Two EC2 instances run a custom active-passive service inside a VPC. On failure of the active node, the private IP must move to the standby so clients using that private IP keep working. What mechanism achieves this?
- A) Reassign an Elastic IP between the instances
- B) Move a secondary Elastic Network Interface (ENI) holding the private IP to the standby instance
- C) Use Route 53 failover with public records
- D) Change the subnet route table

> **Answer: B** — A secondary ENI (carrying the private IP) can be detached and reattached to the standby; Elastic IP is public, not the private-IP failover mechanism.

**Q33.** Which two statements about VPC subnets and CIDR are correct? **(Select TWO)**
- A) Each subnet resides in exactly one Availability Zone
- B) A VPC CIDR block can range from /16 to /28
- C) A VPC CIDR block can range from /16 to /27
- D) A subnet can span multiple AZs for high availability
- E) New subnets never associate with any route table

> **Answer: A & B** — A subnet maps to one AZ; the VPC/subnet CIDR range is /16 to /28.

**Q34.** A company must move 50 TB of rarely accessed on-prem archive files to the cheapest S3 storage for long-term retention, transferring over the network. What is the most cost-effective approach?
- A) Use DataSync to write directly to S3 Glacier Deep Archive
- B) Upload to S3 Standard, then add a lifecycle rule to Deep Archive later
- C) Use S3 Transfer Acceleration to S3 Standard
- D) Ship the files on physical media

> **Answer: A** — DataSync can land data directly in Glacier Deep Archive, avoiding paying for Standard storage first. (Over-the-network rules out Snow.)

**Q35.** Which two statements about EC2 billing are correct? **(Select TWO)**
- A) You are billed for a Reserved Instance during its term even if the instance is terminated
- B) An On-Demand instance preparing to hibernate (`stopping`) is billed during that period
- C) A stopped On-Demand instance is billed for compute
- D) A Spot instance in the `stopping` state is always billed
- E) Reserved Instances are free once purchased

> **Answer: A & B** — RIs are billed for the committed term regardless; hibernating On-Demand is billed during `stopping`. Stopped instances aren't billed for compute (only EBS).

**Q36.** A company wants to reduce compute costs by committing to a consistent amount of spend per hour for 1 year, while keeping flexibility to change instance families, sizes, and regions. Which pricing model fits best?
- A) Standard Reserved Instances locked to one instance type
- B) Compute Savings Plans
- C) Spot Instances
- D) On-Demand

> **Answer: B** — Compute Savings Plans commit to $/hour and apply flexibly across families, sizes, regions (and Fargate/Lambda).

**Q37.** EC2 instances in private subnets download large volumes of data from S3, and the company wants to avoid NAT Gateway data-processing charges for this S3 traffic. What should be configured?
- A) An S3 interface endpoint (PrivateLink) with hourly + data charges
- B) An S3 gateway VPC endpoint, which has no additional charge and keeps traffic off the NAT Gateway
- C) A second NAT Gateway
- D) A VPC peering connection to S3

> **Answer: B** — An S3 gateway endpoint is free and routes S3 traffic privately, avoiding NAT Gateway data charges.

**Q38.** A partner must whitelist a fixed set of static IP addresses to reach an application, which requires ultra-low-latency Layer 4 handling of millions of TCP connections. Which load balancer fits?
- A) Application Load Balancer
- B) Network Load Balancer with Elastic IPs
- C) Classic Load Balancer
- D) Gateway Load Balancer

> **Answer: B** — NLB operates at L4, handles massive TCP throughput, and supports static/Elastic IPs for whitelisting (ALB has no static IP).

**Q39.** A read-heavy web application repeatedly runs the same expensive database queries, driving up latency. The team wants a managed in-memory cache to store query results and reduce DB load. Which service fits?
- A) Amazon ElastiCache (Redis/Memcached)
- B) Amazon DynamoDB
- C) Amazon Athena
- D) AWS Glue

> **Answer: A** — ElastiCache provides managed in-memory caching to offload repeated reads from the database.

**Q40.** An HPC workload needs a high-throughput, low-latency parallel file system for compute, with the underlying data set durably stored in S3 and processed at scale. Which storage fits best?
- A) Amazon FSx for Windows File Server
- B) EBS gp3 volumes
- C) Amazon EFS
- D) Amazon FSx for Lustre linked to an S3 bucket

> **Answer: D** — FSx for Lustre is the HPC parallel file system and integrates with S3 for the data set.

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
