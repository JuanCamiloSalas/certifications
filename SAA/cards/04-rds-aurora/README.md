[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../05-route53/README.md)

# Bloque 04 — RDS, Aurora & ElastiCache

> Bases de datos relacionales gestionadas y cacheo en memoria. **Aurora es la estrella** del bloque y la que más cae.

## 🃏 Cards de este bloque

_Sin cards aún. Copia [`_TEMPLATE.md`](../_TEMPLATE.md) aquí para empezar._

| # | Card | Concepto |
|---|---|---|

## 🎯 Conceptos sugeridos a cubrir

- RDS read replicas (hasta 15, sync async, cross-region)
- RDS Multi-AZ (HA, NO escalado)
- RDS backup automático vs manual snapshots
- RDS encryption: en reposo (KMS) y en tránsito (SSL)
- RDS Proxy: caso de uso (Lambda + RDS, failover rápido)
- Aurora: arquitectura (1 writer + hasta 15 readers, storage compartido)
- Aurora endpoints: writer / reader / custom
- Aurora Serverless v1 vs v2
- Aurora Global Database (cross-region, < 1s replication, < 1 min DR failover)
- Aurora Machine Learning, Aurora Backtrack
- ElastiCache Redis vs Memcached
- ElastiCache patterns: lazy loading vs write-through, TTL

## 🔗 Comparativas relacionadas

- RDS vs Aurora (cuándo cada uno)
- RDS Multi-AZ vs Read Replica
- Aurora endpoints: writer vs reader vs custom
- ElastiCache Redis vs Memcached
- Aurora Serverless v1 vs v2

---

[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../03-elb-asg/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../05-route53/README.md)
