[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-rds.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-aurora.md)

# RDS Proxy

<img src="../../assets/icons/rds.png" width="64">

> **Pitch (1 line):** a fully managed connection pooler that sits between your app and RDS/Aurora, dramatically reducing connection overhead — critical for serverless workloads (Lambda + RDS).

## 🎯 When the exam picks this

- "Lambda functions opening too many DB connections" → **RDS Proxy**
- "reduce DB failover time" → **RDS Proxy** (cuts failover from ~1–2 min to seconds)
- "pool and share DB connections" → **RDS Proxy**

## 🧠 Core (non-obvious bits)

- Sits between the application and the DB endpoint. Apps connect to the **proxy endpoint**, not directly to the DB.
- Maintains a **warm pool** of DB connections — Lambda invocations reuse them instead of opening new ones on every call. Lambda's ephemeral nature would otherwise exhaust DB connection limits instantly.
- On **Multi-AZ failover**, the proxy reconnects to the new primary without the app noticing — reduces failover time from ~60–120s to **<30s**.
- **IAM authentication + Secrets Manager** enforced at the proxy — no DB credentials in code.
- Supported engines: MySQL, PostgreSQL, MariaDB, SQL Server, Aurora MySQL, Aurora PostgreSQL.
- Deployed in the **VPC** — only accessible from within the VPC (no public endpoint).

## ⚠️ Common traps

- RDS Proxy does NOT reduce query latency — it reduces connection latency and failover time.
- The proxy does NOT support all DB features (e.g., some stored procedure calls may behave differently).
- "Lambda + RDS without proxy" → will hit connection limits under concurrency spikes.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-rds.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-aurora.md)
