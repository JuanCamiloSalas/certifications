[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# 🃏 Mazo SAA

> Flashcards de estudio para el SAA-C03. Cada archivo es una card autocontenida. Navega con los botones **Anterior / Siguiente** dentro de cada card.

## 📚 Bloques

| # | Bloque | Sec. curso | Estado |
|---|---|---|---|
| 01 | [EC2 SAA-level](./01-ec2-saa/) | 6 | ✅ visto |
| 02 | [Storage EC2 (EBS, EFS, Instance Store)](./02-storage-ec2/) | 7 | ✅ visto |
| 03 | [ELB & ASG](./03-elb-asg/) | 8 | ✅ visto |
| 04 | [RDS & Aurora](./04-rds-aurora/) | 9 | ✅ visto |
| 05 | [Route 53](./05-route53/) | 10-11 | ✅ visto |
| 06 | [S3 avanzado](./06-s3-avanzado/) | 13-15 | ✅ visto |
| 07 | [CDN & Edge (CloudFront, Global Accelerator)](./07-cdn/) | 16-17 | ✅ visto |
| 08 | [Decoupling (SQS, SNS, Kinesis, MQ)](./08-decoupling/) | 18 | 🔄 en curso |
| 09 | [Containers (ECS, EKS, Fargate, ECR)](./09-containers/) | 19 | 📅 |
| 10 | [Serverless (Lambda, API GW, Step Functions)](./10-serverless/) | 20-21 | 📅 |
| 11 | [BD avanzadas + Data + ML](./11-bd-data-ml/) | 22-24 | 📅 |
| 12 | [Monitoring (CloudWatch, CloudTrail, X-Ray)](./12-monitoring/) | 25 | 📅 |
| 13 | [IAM avanzado](./13-iam-avanzado/) | 26 | 📅 |
| 14 | [Security & Cifrado (KMS, Secrets, WAF, Shield)](./14-security-cifrado/) | 27 | 📅 |
| 15 | [VPC & Networking](./15-vpc/) | 28 | 📅 |
| 16 | [DR & Migration](./16-dr-migration/) | 29 | 📅 |

## 🧭 Cómo navegar

- **Mobile (GitHub app):** entra a un bloque, abre cualquier card, y usa los botones `Anterior` / `Siguiente` para recorrer el bloque entero.
- **Desktop:** además puedes ir al README de un bloque para ver todas sus cards listadas.
- **Búsqueda rápida:** usa el buscador de GitHub (`t` en desktop) y escribe el servicio.

## ➕ Cómo crear una nueva card

1. Copia [`_TEMPLATE.md`](./_TEMPLATE.md) dentro de la carpeta del bloque.
2. Renombra: `NN-nombre-corto.md` (NN = siguiente número en el bloque).
3. Ajusta los botones de navegación arriba y abajo (prev / next).
4. Actualiza el `README.md` del bloque añadiendo el link.
5. Si introduces una card en medio, también actualiza el `next` de la card anterior y el `prev` de la siguiente.

## 📏 Reglas de calidad

- Una card debe entrar sin scroll en celular. Si pasa de ~120 líneas → dividir.
- Sin transcribir slides. Solo lo no obvio o lo que ya confundió en un Dojo.
- Los versus largos viven en [`../comparativas/`](../comparativas/), no aquí.
- Si una card menciona números (límites, timeouts, tamaños), van en una sección dedicada para que sean fáciles de cazar en el repaso final.

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
