[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)

# Bloque 03 — ELB & Auto Scaling Group

> **Cuál load balancer en qué escenario** + **políticas de escalado**. El SAA exige tener interiorizada la diferencia ALB / NLB / GLB.

## 🃏 Cards de este bloque

_Sin cards aún. Copia [`_TEMPLATE.md`](../_TEMPLATE.md) aquí para empezar._

| # | Card | Concepto |
|---|---|---|

## 🎯 Conceptos sugeridos a cubrir

- ALB: HTTP/HTTPS, path/host-based routing, redirects, target groups
- NLB: TCP/UDP/TLS, IP estática por AZ, ultra baja latencia
- GLB (Gateway LB): tráfico para appliances de terceros (firewalls)
- CLB: legacy, casi nunca correcta en el examen
- Sticky sessions (cookies application vs duration based)
- Cross-Zone Load Balancing (default por LB)
- SSL/TLS termination, SNI
- Connection draining / Deregistration delay
- ASG: scaling policies (target tracking, step, simple)
- ASG: launch templates vs launch configurations
- ASG lifecycle hooks
- ASG con múltiples AZ

## 🔗 Comparativas relacionadas

- ALB vs NLB vs GLB vs CLB
- Target tracking vs Step vs Simple scaling
- Sticky sessions: dónde se manejan en ALB vs NLB

---

[![](https://img.shields.io/badge/<_Bloque_anterior-FF4859?style=for-the-badge)](../02-storage-ec2/README.md)
[![](https://img.shields.io/badge/Mazo-175074?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/Siguiente_bloque_>-FF4859?style=for-the-badge)](../04-rds-aurora/README.md)
