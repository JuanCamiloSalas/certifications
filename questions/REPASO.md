[![](https://img.shields.io/badge/<-FF4859?style=for-the-badge)](../README.md)
[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](../README.md)

# Repaso de simulacro CCP — puntos débiles

**Resultado:** 83% (54/65) — Aprobado (umbral 70%)

| Dominio | Peso AWS | Puntaje | Prioridad |
|---------|----------|---------|-----------|
| **Cloud Technology and Services** | **34%** | **77%** | 🔴 **MÁXIMA** |
| **Security and Compliance** | **30%** | 89% | 🟡 Media |
| **Cloud Concepts** | 24% | 92% | 🟢 Baja |
| **Billing, Pricing, and Support** | 12% | 80% | 🟡 Media |

> [!IMPORTANT]
> El orden de este README está hecho para enfocar primero los dominios con **mayor peso × menor puntaje**.

---

# 🔴 1. Cloud Technology and Services (34%)

## 1.1 Desacoplar y aplicaciones event-driven → **EventBridge** (no SNS)

**Pregunta tipo (Q25):** *"¿Qué servicio AWS te permite construir aplicaciones event-driven y desacoplar componentes?"*

| Servicio | Cuándo es la respuesta |
|---|---|
| **Amazon EventBridge** | **Aplicaciones event-driven**, regla → destino, eventos de AWS o aplicaciones |
| **Amazon SQS** | **Cola de mensajes** (productores/consumidores, desacoplar trabajo) |
| **Amazon SNS** | **Pub/Sub** — un emisor a múltiples suscriptores |
| **Amazon Kinesis** | **Streaming en tiempo real** de grandes volúmenes de datos |

> [!TIP]
> **Sugerencia de examen:** la palabra clave **"event-driven"** + **"decouple components"** = **EventBridge**. Si dice solo **"decouple"** sin event-driven, casi siempre es **SQS**. **SNS** = pub/sub (notificar a muchos a la vez).

## 1.2 Despliegue híbrido on-premises → **Systems Manager + CodeDeploy**

**Pregunta tipo (Q27):** *"Empresa con arquitectura híbrida quiere desplegar app web a servidores on-premises. ¿Qué servicios usar? (Select TWO)"*

- ✅ **AWS Systems Manager** — gestiona instancias **EC2 e on-premises** (ejecución de comandos, parches, inventario). Híbrido por excelencia.
- ✅ **AWS CodeDeploy** — despliega código a **EC2, Lambda, ECS y servidores on-premises**.
- ❌ **Elastic Beanstalk** — solo despliega en infra **AWS**, no on-premises.
- ❌ **CloudFormation** — provisiona infra AWS, no aplica a servidores on-prem.

> [!TIP]
> **Sugerencia de examen:** si dice **"on-premises"** + **"deploy"**, los dos servicios son **Systems Manager** (gestión) y **CodeDeploy** (despliegue de código). **Elastic Beanstalk NO funciona en on-prem**.

## 1.3 EC2: opciones de compra y licencias

**Pregunta tipo (Q48):** *"¿Qué opción de compra EC2 te permite usar tus licencias existentes (BYOL) y cumplir requisitos de compliance?"*

| Opción | Cuándo |
|---|---|
| **Dedicated Host** | **Servidor físico dedicado**, **visibilidad de sockets/cores**, ideal para **BYOL** (Bring Your Own License) y compliance |
| **Dedicated Instance** | Hardware dedicado **pero sin visibilidad del host físico**. No sirve para BYOL por socket |
| **Reserved Instance** | Compromiso de 1-3 años, descuento — no relacionado con licencias |
| **On-Demand** | Pago por uso, sin compromiso |

> [!TIP]
> **Sugerencia de examen:** **"licencias existentes" / "BYOL" / "por socket o core"** → **Dedicated Host**. Si solo dice "hardware dedicado sin BYOL" → Dedicated Instance.

## 1.4 Reserved Instances — tipos

**Pregunta tipo (Q20):** *"Necesitas lanzar EC2 que va a cambiar familia, SO y tenancy 3 meses después del trial. ¿Qué tipo de RI?"*

| Tipo de RI | Cuándo |
|---|---|
| **Standard RI** | Mayor descuento, **no permite cambiar familia/SO/tenancy** |
| **Convertible RI** | Permite **cambiar familia, SO, tenancy** (con menor descuento) |
| **Scheduled RI** | Para uso en **horarios específicos recurrentes** (descontinuado) |

> [!TIP]
> **Sugerencia de examen:** si la pregunta menciona **"cambiar familia/SO/tenancy"** → **Convertible RI**. Si es flexible en **familia entera + región** → EC2 Instance Savings Plan. Si es flexible en **todo + Fargate/Lambda** → Compute Savings Plan.

## 1.5 Bases de datos: SQL Server rápido y eficiente → **RDS + EC2**

**Pregunta tipo (Q57):** *"Equipo necesita SQL Server en AWS rápido y eficiente. (Select TWO)"*

- ✅ **Amazon RDS (for SQL Server)** — gestionado, listo en minutos
- ✅ **Amazon EC2** — instala SQL Server tú mismo (control total)
- ❌ **Amazon Aurora** — compatible **MySQL/PostgreSQL únicamente**, NO SQL Server
- ❌ **Aurora Backtrack** — feature de Aurora, no aplica
- ❌ **Redshift** — data warehouse, no OLTP

> [!TIP]
> **Sugerencia de examen:** **Aurora ≠ SQL Server**. Aurora solo soporta **MySQL y PostgreSQL**. Para **SQL Server, Oracle, MariaDB** → **RDS** (gestionado) o **EC2** (autogestión).

## 1.6 Conexión on-premises ↔ VPC: VPN

**Pregunta tipo (Q63):** *"¿Qué se usa para resolver la conexión entre tu VPN on-premises y tu VPC?"*

- **Virtual Private Gateway (VGW)** — el lado AWS de la VPN
- **Customer Gateway (CGW)** — el lado on-premises de la VPN
- ❌ **Egress-Only Internet Gateway** — solo para tráfico **IPv6 saliente** desde VPC
- ❌ **NAT Gateway** — para que instancias privadas salgan a Internet
- ❌ **VPC Peering** — conectar VPCs entre sí

> [!TIP]
> **Sugerencia de examen:** **VPN site-to-site** = **VGW (lado AWS)** + **CGW (lado on-prem)**. **Egress-Only IGW** es solo para **IPv6 saliente**, no confundir con VPN.

## 1.7 Application Load Balancer (ALB) — features clave

**Pregunta tipo (Q1):** *"¿Qué ELB soporta path-based, host-based routing y WebSockets bidireccional?"*

- ✅ **ALB** — Capa 7 (HTTP/HTTPS), **path-based, host-based, WebSockets, HTTP/2, redirecciones**
- ❌ **NLB** — Capa 4 (TCP/UDP), ultra-baja latencia, IP estática
- ❌ **Gateway LB** — para appliances de red (firewalls, IDS/IPS) en Capa 3
- ❌ **CLB** — legacy, no usar

> [!TIP]
> **Sugerencia de examen:** **routing por path/host + WebSockets + HTTP** → **ALB**. **TCP/UDP + millones de req/s + IP fija** → **NLB**. **Appliances de red** → **Gateway LB**.

---

# 🟡 2. Security and Compliance (30%)

## 2.1 Modelo de Responsabilidad Compartida — responsabilidad **única del cliente**

**Pregunta tipo (Q42):** *"¿Cuál de las siguientes es responsabilidad **únicamente del cliente**?"*

**Cliente (security IN the cloud):**
- ✅ **Service and Communications Protection / Zone Security** (segmentación de red, NACL, SG)
- ✅ Datos del cliente (encriptación, clasificación)
- ✅ Gestión de IAM (usuarios, roles, MFA)
- ✅ Configuración del SO **invitado** (en EC2)
- ✅ Configuración de la red (VPC, SG, NACL)
- ✅ Awareness & Training (entrenamiento de empleados — pero esto AWS también ofrece, por eso no es "solely")

**AWS (security OF the cloud):**
- 🔵 **Patching del host OS** (hipervisor)
- 🔵 Hardware, software, instalaciones físicas
- 🔵 Servicios gestionados (RDS, S3 a nivel de infraestructura)

**Compartidas:**
- 🟡 **Configuration Management** — AWS configura la infra, cliente configura sus apps
- 🟡 Patch Management — AWS parcha la infra, cliente parcha el SO de EC2
- 🟡 Awareness & Training

> [!TIP]
> **Sugerencia de examen:** si la pregunta dice **"solely"** o **"únicamente el cliente"**, descarta lo que sea compartido (Config Management, Patch Mgmt, Training). **Patching del host OS** es siempre **AWS**. **Seguridad de zona / segmentación de red** es siempre **cliente**.

---

# 🟢 3. Cloud Concepts (24%)

## 3.1 Beneficio financiero de migrar a AWS → **CAPEX → OPEX**

**Pregunta tipo (Q36):** *"¿Cuál es un beneficio financiero clave de migrar de on-prem a AWS?"*

✅ **Reemplazar gastos de capital iniciales (CAPEX) con bajos costes variables (OPEX).**

- **CAPEX** = inversión grande inicial (servidores, datacenter)
- **OPEX** = gasto operativo recurrente, variable, según uso

> [!TIP]
> **Sugerencia de examen:** Cloud = **CAPEX → OPEX**. Pagas **solo por lo que usas**, sin compra inicial de hardware. Memoriza el orden: **upfront CAPEX → low variable OPEX**.

## 3.2 Edge Locations — beneficios

**Pregunta tipo (Q65):** *"¿Cuáles son beneficios de las Edge Locations? (Select TWO)"*

- ✅ **Caching que reduce la carga en los servidores origen** (CloudFront cachea contenido)
- ✅ **Mejora el rendimiento entregando contenido más cerca de los usuarios** (baja latencia)
- ❌ Edge computing devices (eso es Snowball Edge / Snowcone)
- ❌ Object storage escalable (eso es S3)

> [!TIP]
> **Sugerencia de examen:** **Edge Locations = CloudFront**. Beneficios = **cache + latencia baja**. **NO confundir** con Snow Family (edge computing devices físicos).

---

# 🟡 4. Billing, Pricing, and Support (12%)

## 4.1 Categorizar y rastrear costes detalladamente → **Cost Allocation Tags**

**Pregunta tipo (Q45):** *"¿Qué te permite categorizar y rastrear tus costes AWS a nivel detallado?"*

| Servicio | Para qué |
|---|---|
| **Cost Allocation Tags** | **Categorizar y rastrear** costes detalladamente por proyecto, departamento, equipo |
| **AWS Budgets** | **Alertas** cuando se supera un presupuesto |
| **Consolidated Billing** | Una factura para múltiples cuentas |
| **Cost Explorer** | **Visualizar** y prever costes |
| **AWS CUR** | El **dataset más completo** de facturación |

> [!TIP]
> **Sugerencia de examen:** **"categorizar y rastrear costes detalladamente"** → **Cost Allocation Tags**. **"alertas al superar presupuesto"** → **Budgets**.

## 4.2 Beneficios de Consolidated Billing

**Pregunta tipo (Q16, Q51):**

✅ **Beneficios reales:**
- **Volume pricing** — descuentos por volumen al combinar uso de todas las cuentas
- **Compartir RI y Saving Plans** entre cuentas de la organización
- **Una sola factura** para todas las cuentas
- **Un único método de pago**

❌ **Trampas comunes:**
- "One member account paying charges of all master accounts" — **invertido**: la **master/management** paga, no un member
- "$1 every month" — falso
- "AISPL accounts consolidation" — AISPL (India) **no se puede consolidar** con cuentas globales

> [!TIP]
> **Sugerencia de examen:** Consolidated Billing = **1 factura + descuentos por volumen + compartir RI/SP**. La **cuenta maestra (management)** es la que paga, no al revés. **AISPL no se consolida** con AWS global.

## 4.3 AWS Professional Services vs TAM vs Concierge

**Pregunta tipo (Q30):** *"¿Qué canal ofrece engagements pagados en áreas de práctica especializadas para adopción cloud?"*

| Servicio | Qué hace |
|---|---|
| **AWS Professional Services** | **Engagements pagados** especializados, **proyectos consulting** para adopción cloud |
| **AWS Technical Account Manager (TAM)** | **Asignado a tu cuenta** en planes Enterprise. Asesoría continua, NO ejecuta proyectos |
| **Concierge Support** | Equipo de soporte de **facturación y cuenta** (Business/Enterprise) |
| **AWS Enterprise Support** | El **plan de soporte**, no un servicio profesional |

> [!TIP]
> **Sugerencia de examen:** **"paid engagements" / "specialty practices" / "consulting projects"** → **AWS Professional Services**. **TAM** = persona asignada para asesoría, no ejecuta proyectos.

## 4.4 Trusted Advisor — las 5 categorías

**Pregunta tipo (Q10):** *"¿Cuáles son las 5 categorías de Trusted Advisor? (Select TWO)"*

Las **5 categorías** son:
1. **Cost Optimization** (Optimización de costes)
2. **Performance** (Rendimiento)
3. **Security** (Seguridad)
4. **Fault Tolerance** (Tolerancia a fallos)
5. **Service Limits** (Límites de servicio / Service Quotas)

❌ NO son: Infrastructure, Instance Usage, Storage Capacity

> [!TIP]
> **Sugerencia de examen — mnemotécnico "CPSF-L":** **C**ost · **P**erformance · **S**ecurity · **F**ault Tolerance · service **L**imits.

---

# Resumen — qué memorizar antes del examen

| Confusión típica | Respuesta correcta |
|---|---|
| Event-driven + decouple | **EventBridge** (no SNS) |
| Decouple solo (sin event-driven) | **SQS** |
| Pub/Sub | **SNS** |
| Deploy a on-premises | **Systems Manager + CodeDeploy** (no Beanstalk) |
| BYOL / licencias por socket | **Dedicated Host** (no Dedicated Instance) |
| Cambiar familia/SO/tenancy en RI | **Convertible RI** |
| SQL Server en AWS | **RDS for SQL Server + EC2** (NO Aurora) |
| VPN on-prem ↔ VPC | **VGW + CGW** (no Egress-Only IGW) |
| ALB vs NLB | ALB = HTTP/path/host/WebSocket; NLB = TCP/UDP/IP fija |
| Solely customer responsibility | **Zone Security / network segmentation** |
| Solely AWS responsibility | **Patching del host OS** |
| CAPEX vs OPEX | Cloud = **CAPEX → OPEX** |
| Edge Locations | Cache + latencia (CloudFront) |
| Categorizar costes detallado | **Cost Allocation Tags** (no Budgets) |
| Consolidated Billing | **1 factura + volume pricing + compartir RI/SP** |
| Specialty consulting paid | **AWS Professional Services** |
| 5 categorías Trusted Advisor | **C**ost · **P**erformance · **S**ecurity · **F**ault Tolerance · service **L**imits |
