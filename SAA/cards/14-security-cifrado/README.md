[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../13-iam-avanzado/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../15-vpc/README.md)

# Bloque 14 — Security & Cifrado

> **KMS, Secrets Manager, Parameter Store, WAF, Shield, GuardDuty, Macie, Inspector.** El examen pregunta "¿qué servicio detecta/protege qué?".

## 🃏 Cards de este bloque

_Sin cards aún. Copia [`_TEMPLATE.md`](../_TEMPLATE.md) aquí para empezar._

| # | Card | Concepto |
|---|---|---|

## 🎯 Conceptos sugeridos a cubrir

### Cifrado y claves
- KMS: symmetric vs asymmetric, AWS managed vs customer managed (CMK)
- KMS key policy y grants
- Envelope encryption, data keys
- KMS multi-region keys
- CloudHSM (dedicated, FIPS 140-2 Level 3)
- Secrets Manager: rotación automática, integración con RDS
- Systems Manager Parameter Store: jerarquía, versionado
- ACM (Certificate Manager): public vs private CA

### Protección perímetro
- WAF: web ACLs, rules, managed rule groups
- Shield Standard (gratis) vs Shield Advanced ($3k/mes, DDoS Response Team)
- AWS Firewall Manager

### Detección
- GuardDuty (threat detection: VPC Flow Logs, DNS, CloudTrail)
- Macie (PII / datos sensibles en S3)
- Inspector (vulnerabilidades en EC2, ECR, Lambda)
- Detective (investigación de incidentes)
- Security Hub (agregador)

## 🔗 Comparativas relacionadas

- Secrets Manager vs Parameter Store
- KMS CMK vs AWS managed key
- Shield Standard vs Advanced
- GuardDuty vs Macie vs Inspector vs Detective (los confundes seguro)
- WAF vs Shield vs Network Firewall

---

[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../13-iam-avanzado/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../15-vpc/README.md)
