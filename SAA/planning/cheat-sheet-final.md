[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Planning-175074?style=for-the-badge)](./planning_semana_final.md)

# 🎯 Cheat-Sheet Final — víspera del examen (SAA-C03)

> Una página. Tus rojos vigentes. Léela esta noche y de un vistazo el lunes antes de entrar.
> **Umbral: 720/1000 (~72%).** TutorialsDojo es más duro que el examen real.

---

## 🔴 SECURE (30% del examen — tu fuga principal, 90→71→65)

| Escenario | Respuesta |
|---|---|
| SSO con AD corporativo existente | **IAM Identity Center + AD Connector** (+ SCP) |
| Cuentas nuevas con guardrails/baselines preaprobados | **Control Tower Landing Zone** (no RAM, no Config) |
| Lambda debe descifrar con KMS | `kms:decrypt` en el **execution role** + key policy concede **al role** (no al ARN) |
| Permisos para muchos usuarios IAM | **IAM Group** (roles se asumen, no agrupan humanos) |
| Acceso cross-account a S3 | **bucket policy** (recurso) **+ IAM policy** (principal) |
| NACL (stateless) permitir respuesta | abrir **puertos efímeros 1024–65535 outbound**. SG = stateful (auto) |
| Contenido privado solo vía CloudFront | **OAC** (bloquea origen) **+ signed URLs/cookies** (quién accede) |
| Config app cifrada y barata | **SSM Parameter Store SecureString + KMS** (más barato que Secrets Manager) |
| Header de cifrado en S3 | `x-amz-server-side-encryption` (SSE-S3/KMS). Los `-customer-*` son solo **SSE-C** |

---

## 🟠 RESILIENT (26% — crónico, solo hay que pasar de 60%)

| Escenario | Respuesta |
|---|---|
| Failover RDS Multi-AZ | el **CNAME (DNS) se repunta al standby**; la IP no cambia. Standby NO es legible |
| Multi-AZ vs Read Replica | Multi-AZ = HA (sync, failover) · Read Replica = escalar lecturas (async) |
| Retención de backup RDS > 35 días | **AWS Backup** (automáticos topan en 35 días) |
| RDS se queda sin disco, mínimo esfuerzo | **storage autoscaling** (no resize manual, no PIOPS) |
| Migrar con mínimo downtime / sync continua on-prem | **DMS full load + CDC** |
| DX a muchas cuentas/VPCs | **DX Gateway + Transit Gateway** (peering NO es transitivo) |
| Redundancia DX | **2º DX al mismo VPC + VPN site-to-site de respaldo** |
| Automatizar snapshots EBS, simple | **Data Lifecycle Manager (DLM)** (no AWS Backup) |
| Failover de IP privada | **ENI secundaria** que se mueve de instancia (no Elastic IP) |
| All-active + drop unhealthy en Route 53 | **Active-Active + Weighted** (Failover = active-passive) |
| Stop/Start de EC2 | puede **cambiar de host físico** → Instance Store se borra; EIP/ENI/IP privada se mantienen |

---

## 🌐 NETWORKING / Route 53 (dentro de Resilient/Secure)

- **Geolocation** = reglas por ubicación (compliance) · **Geoproximity** = distancia + **bias dial** · **Latency** = menor RTT · **Weighted** = % de tráfico.
- **Failover** = active-passive (health check obligatorio en el primario).
- **IP estática para whitelisting** = **NLB** (ALB no tiene IP fija).
- **Acceso privado a S3/DynamoDB desde VPC** = **gateway endpoint** (no interface, no NACL).
- **VPC CIDR**: /16 (65.536) → /28 (16). Subnet = **1 AZ**. Subnet nueva → main route table.
- **Alcanzable desde Internet** = IP pública **+** route table → **IGW** **+** SG/NACL permiten.

---

## 💸 COST (20%) y otros gatillos

- **Costo por departamento** = **Cost Allocation Tags** (Budgets = solo alertas).
- **Costo programático + forecast** = **Cost Explorer API**.
- **RIs decomisionadas** = **terminate + vender en RI Marketplace** (parar NO corta el cobro).
- **Glacier < 15 min + throughput** = **Expedited + provisioned retrieval capacity**.
- **TB sobre línea lenta** = transferencia offline (**Snowball**), no Transfer Acceleration.
- **Archivo on-prem → directo a Glacier Deep Archive** vía **DataSync**.
- **ALB muchos dominios SSL** = **SNI** (no wildcard). **Transformar S3 en GET** = **S3 Object Lambda**.

---

## 🧠 TÁCTICA DE EXAMEN (lo que más puntos te ha costado)

- **"Select TWO":** tu fallo es acertar una y picar **un distractor plausible**. Valida **cada opción marcada por separado**, no por "suena bien".
- **~2 min/pregunta.** Marca dudas y sigue. Tienes **+30 min ESL** — úsalos, no corras.
- **Frases gatillo:** cost-effective · highly available · lowest latency · decouple · least privilege · synchronous → **Multi-AZ**.
- Llega **AM y descansado** (tus mejores notas lo fueron). **Domingo = descanso total.**

---

*Foco de la víspera: recuperar **Secure** (30% del examen). Resilient ya repunta solo. High-Performing está sólido — no lo toques.*

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
