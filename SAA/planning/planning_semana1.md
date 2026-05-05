# Semana 1 (5-10 mayo) - EC2 SAA + Storage + ELB/ASG + RDS + Route 53

> **Foco:** Bloques A (Fundamentos avanzados) + B (BD básicas) + C (Route 53/Arquitecturas)
> **Hito al cierre:** dominio sólido de EC2 nivel SAA, EBS/EFS, ELB/ASG, RDS y Route 53
> **Tiempo liberado:** ~6h por saltar secciones 3, 4, 5 (cubiertas en CCP)

## ⏭️ Secciones saltadas esta semana

- ~~Sec 3: Empezando con AWS~~
- ~~Sec 4: IAM y CLI de AWS~~
- ~~Sec 5: Fundamentos de EC2~~

> **Nota:** revisa el índice de cada una antes del lunes para confirmar que no hay subtemas nuevos. Si aparece algo desconocido (ej: nuevos tipos de instancias EC2 que no hayas visto), ve solo ese subtema puntual.

## 🎯 Objetivos de la semana

- ✅ Completar secciones 6, 7, 8, 9, 10, 11
- ✅ Construir primeras notas comparativas (3 tipos)
- ✅ Hands-on real con EC2 nivel SAA, EBS/EFS, ELB/ASG y RDS
- ✅ Hacer al menos 80 preguntas Dojo topic-based (no simulacro completo)
- ✅ Cerrar la semana con una arquitectura web HA desplegada manualmente
- ✅ Aprovechar las 6h liberadas para profundizar en hands-on

## 📅 Plan día por día

### 🟦 Lunes 5 de mayo - EC2 nivel SAA + arranque (4-5h)

**Contenido:**
- [ ] Sección 6: EC2 - Nivel Solutions Architect Associate (51 min)
- [ ] Inicio Sección 7: Almacenamiento de instancias EC2 (~30-40 min del 1h 21m)

**Hands-on (1.5h):**
- [ ] Lanzar instancia EC2 con diferentes tipos (t2.micro, t3.small) - comparar
- [ ] Configurar Placement Groups (Cluster, Spread, Partition) y entender cuándo usar cada uno
- [ ] Probar Spot Instances y Spot Fleet
- [ ] Crear AMI custom desde una instancia configurada
- [ ] Lanzar nueva instancia desde tu AMI
- [ ] Configurar User Data para instalar Apache automáticamente

**Apuntes a construir en `notes/01-ec2-saa.md`:**
- Tabla decisión: **Placement Groups** (Cluster vs Spread vs Partition)
- Comparativa: **Spot vs Reserved vs Savings Plans vs On-Demand vs Dedicated** (cuándo cada uno)
- Patrón: cuándo usar Spot Fleet vs ASG con Spot
- Tips para `tips/tips-examen.md`: trampas comunes con Spot interruptions

**Preguntas Dojo topic-based (15 preguntas - EC2):**
- [ ] Hacer 15 preguntas de EC2 nivel SAA
- [ ] Anotar errores en `errors/doc-maestro.md`

---

### 🟦 Martes 6 de mayo - Almacenamiento EC2 completo (4-5h)

**Contenido:**
- [ ] Resto de Sección 7: Almacenamiento de instancias EC2 (~45 min restantes)

**Hands-on (2h) - APROVECHA EL TIEMPO LIBERADO:**
- [ ] Crear volumen EBS gp3 y adjuntarlo a instancia
- [ ] Cambiar el tipo de volumen en caliente (gp3 → io1)
- [ ] Hacer snapshot de EBS y restaurar en otra AZ
- [ ] Comparar EBS (gp3) vs Instance Store (probar persistencia con stop/start)
- [ ] Crear EFS y montarlo en 2 instancias EC2 simultáneamente (multi-AZ)
- [ ] (Opcional) crear FSx for Windows o FSx for Lustre para entender diferencias

**Apuntes a construir en `notes/02-storage-ec2.md`:**
- Comparativa CRÍTICA: **EBS vs EFS vs Instance Store vs FSx**
  - Casos de uso, performance, multi-AZ, multi-attach
- Tabla: **tipos de volúmenes EBS** (gp3, gp2, io1/io2, st1, sc1) - cuándo cada uno
- Tabla: **tipos de FSx** (Windows, Lustre, NetApp ONTAP, OpenZFS)
- Patrón: cuándo replicar EBS a otra AZ (snapshot) vs usar EFS multi-AZ
- Tips para `tips/tips-examen.md`: keywords que disparan cada tipo de storage

**Preguntas Dojo topic-based (20 preguntas - Storage EC2):**
- [ ] Hacer 20 preguntas de EBS/EFS/Instance Store/FSx
- [ ] Revisar errores y profundizar lo dudoso

---

### 🟦 Miércoles 7 de mayo - ELB y Auto Scaling (4-5h)

**Contenido:**
- [ ] Sección 8: Alta disponibilidad y escalabilidad: ELB y ASG (1h 44min)

**Hands-on (2h):**
- [ ] Crear ALB con 2 target groups (mínimo 2 AZ)
- [ ] Lanzar 2 EC2 detrás del ALB con páginas web distintas
- [ ] Configurar Health Checks personalizados
- [ ] Configurar Sticky Sessions y probar comportamiento
- [ ] Crear NLB y comparar con ALB en consola
- [ ] Crear Launch Template (no Launch Configuration legacy)
- [ ] Crear Auto Scaling Group con mín=2, max=4, desired=2
- [ ] Configurar política de scaling: Target Tracking (CPU 50%)
- [ ] Probar scaling: simular CPU alta con stress y verificar que ASG escala
- [ ] Configurar lifecycle hooks (opcional)

**Apuntes a construir en `notes/03-elb-asg.md`:**
- Comparativa CRÍTICA: **CLB vs ALB vs NLB vs GLB**
  - Capa OSI, casos de uso, sticky sessions, target types, latency
- Tabla: **políticas de scaling** (target tracking, step, simple, scheduled, predictive)
- Tabla: **target types** (instance, IP, Lambda, ALB)
- Patrón: arquitectura web HA con ALB + ASG multi-AZ
- Tips para `tips/tips-examen.md`:
  - "millions of requests per second" → NLB
  - "HTTP routing por path/host" → ALB
  - "encryption at TCP layer" → NLB

**Preguntas Dojo topic-based (20 preguntas - ELB/ASG):**
- [ ] Hacer 20 preguntas de balanceadores y autoscaling
- [ ] Anotar errores

---

### 🟦 Jueves 8 de mayo - RDS, Aurora, ElastiCache (4-5h)

**Contenido:**
- [ ] Sección 9: Fundamentos de AWS - RDS + Aurora + ElastiCache (1h 31min)

**Hands-on (2h):**
- [ ] Crear instancia RDS MySQL (t3.micro, free tier)
- [ ] Habilitar Multi-AZ deployment
- [ ] Crear Read Replica (en misma región y otra región)
- [ ] Conectarse desde EC2 a RDS (security groups + endpoint)
- [ ] Hacer snapshot manual y restaurar en otra región
- [ ] Habilitar encryption at rest con KMS
- [ ] Crear cluster Aurora con 1 writer + 1 reader
- [ ] Probar failover de Aurora (forzar)
- [ ] (Opcional) Crear cluster ElastiCache Redis y conectar desde EC2

**Apuntes a construir en `notes/04-rds-aurora.md`:**
- Comparativa CRÍTICA: **RDS vs Aurora vs DynamoDB vs ElastiCache**
- Tabla: **motores soportados por RDS** (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server)
- Comparativa: **Multi-AZ vs Read Replicas** (HA vs performance, sync vs async)
- Comparativa CRÍTICA: **Aurora vs RDS** (cuándo migrar)
- Comparativa: **Redis vs Memcached** (cuándo cada uno)
- Tabla: **Aurora features** (Aurora Serverless, Global Database, Multi-Master)
- Patrón: arquitectura web con RDS Multi-AZ + Read Replicas + ElastiCache
- Tips para `tips/tips-examen.md`:
  - "read scaling" → Read Replicas
  - "disaster recovery cross-region" → Read Replica cross-region o Aurora Global DB
  - "decouple sessions" → ElastiCache (Redis)
  - "leaderboard / real-time analytics" → ElastiCache Redis
  - "infrequent traffic, scale to zero" → Aurora Serverless v2

**Preguntas Dojo topic-based (20 preguntas - BD):**
- [ ] Hacer 20 preguntas de RDS/Aurora/ElastiCache
- [ ] Anotar errores

---

### 🟦 Viernes 9 de mayo - Route 53 (4-5h)

**Contenido:**
- [ ] Sección 10: Route 53 (1h 42min)

**Hands-on (1.5h):**
- [ ] (Si tienes dominio) Registrar/usar hosted zone en Route 53
- [ ] Crear records A simples
- [ ] Configurar health checks
- [ ] Probar diferentes routing policies (al menos 3):
  - Simple
  - Weighted (90/10 entre dos servidores)
  - Failover (con health check)
  - Latency-based (si tienes recursos en 2 regiones)
- [ ] Comparar Alias vs CNAME (cuándo cada uno)

**Apuntes a construir en `notes/05-route53.md`:**
- Tabla CRÍTICA: **routing policies de Route 53** (simple, weighted, latency, failover, geolocation, geoproximity, multi-value)
  - Caso de uso de cada uno
- Comparativa CRÍTICA: **Alias vs CNAME**
  - Alias: gratis, root domain, AWS resources
  - CNAME: paga query, no root domain, cualquier destino
- Tabla: **tipos de health checks** (endpoint, calculated, CloudWatch alarm)
- Patrón: failover entre regiones con Route 53
- Tips para `tips/tips-examen.md`:
  - "lowest latency global" → CloudFront (NO Route 53 latency)
  - "different responses by location" → Geolocation
  - "shift traffic gradually" → Weighted
  - "blue/green deployment" → Weighted

**Repaso semanal (1h):**
- [ ] Lectura horizontal de las notas de toda la semana
- [ ] Identificar qué temas siguen confusos
- [ ] Marcar 2-3 temas para reforzar el sábado

---

### 🟦 Sábado 10 de mayo - Discusiones de arquitectura + integración (6-8h)

**Contenido:**
- [ ] Sección 11: Discusiones sobre soluciones clásicas de arquitectura (49 min)

**Hands-on integral (3h) - PROYECTO DE LA SEMANA:**
> Desplegar una arquitectura web HA completa que integre todo lo visto

- [ ] Crear VPC con 2 subnets públicas y 2 privadas (2 AZ)
- [ ] Configurar Internet Gateway y NAT Gateway
- [ ] Lanzar ALB en subnets públicas
- [ ] Crear ASG con EC2 en subnets privadas (mínimo 2)
- [ ] Configurar User Data: instalar nginx con página simple que muestre el AZ de la instancia
- [ ] Crear RDS Multi-AZ en subnets privadas
- [ ] Crear ElastiCache Redis en subnets privadas (opcional)
- [ ] (Opcional) registrar dominio en Route 53 o usar uno existente
- [ ] Crear hosted zone y record Alias apuntando al ALB
- [ ] Probar en navegador, verificar que rota entre instancias
- [ ] Simular fallo de una EC2 y verificar que ALB redirige
- [ ] **Dibujar el diagrama a mano** (importante para SAA)
- [ ] Tomar foto del diagrama y guardar en `diagrams/`

**Apuntes a construir en `notes/05-route53.md` (continuación):**
- Patrón completo: arquitectura web HA con todos los componentes
- Considerar: ¿qué cambia si necesito multi-región?
- Considerar: ¿cómo escalar a millones de usuarios?

**Preguntas Dojo topic-based (15 preguntas - mixtas):**
- [ ] Hacer 15 preguntas mezcladas de toda la semana
- [ ] Revisar errores en profundidad
- [ ] Actualizar `errors/doc-maestro.md` con patrones detectados

**Cleanup IMPORTANTE (30 min):**
- [ ] Eliminar RDS Multi-AZ (genera costo)
- [ ] Eliminar NAT Gateway (genera costo)
- [ ] Eliminar ElastiCache si lo creaste
- [ ] Eliminar ALB (genera costo)
- [ ] Apagar EC2 o eliminarlas
- [ ] Verificar Cost Explorer al día siguiente

---

### 🟦 Domingo 11 de mayo - Descanso

**Plan recomendado:**
- ❌ NO abrir AWS, Udemy, ni Dojo
- ✅ Actividad no técnica que disfrutes
- ✅ Dormir bien

**Opcional (máximo 30 min):**
- Lectura ligera de las notas de comparativas (sin agregar contenido)
- Revisar `tips/tips-examen.md` acumulado

---

## 📊 Métricas de control de la semana

Al cerrar el sábado, deberías tener:

| Métrica | Meta |
|---|---|
| Secciones del curso completadas | 6, 7, 8, 9, 10, 11 (de 34 totales) |
| Horas netas dedicadas | ~25-30h |
| Notas comparativas creadas (`notes/`) | Mínimo 8 tablas |
| Tips de examen acumulados | Mínimo 15 |
| Preguntas Dojo topic-based hechas | 90+ |
| Hands-on completados | 5 (uno por día L-V + integración sáb) |
| Arquitectura HA desplegada | ✅ 1 completa con diagrama |
| Recursos AWS eliminados | ✅ Todos los pagos cleanup |

## 🚨 Señales de alarma

Si al **viernes 9** no has completado al menos hasta sección 9 (RDS):
- Mover Route 53 al lunes 12
- Aceptar atraso de medio día sin entrar en pánico

Si al **sábado 10** sientes que EC2-SAA, EBS o ELB siguen confusos:
- Dedicar 1-2h del domingo a repaso (excepción al descanso)
- Volver a revisar las comparativas, no los videos
- Hacer 20 preguntas Dojo topic-based extra del tema débil

## 💡 Tips específicos para esta semana

1. **No transcribas a Stephane.** Cuando él compare 2 servicios, PAUSA el video y escribe TÚ la comparativa antes de seguir.

2. **Hands-on con timer.** Si llevas más de 1.5h en un hands-on, párate y sigue al video. La perfección es enemigo del avance.

3. **Free tier alert:** apaga/elimina recursos después de cada hands-on para no generar costos. Especialmente RDS Multi-AZ, NAT Gateway, ALB, ElastiCache.

4. **Dibuja a mano.** Para la arquitectura HA del sábado, hazla en papel o tablet. Los diagramas hechos a mano se aprenden mejor.

5. **El primer simulacro Dojo SAA es el sábado 17.** Esta semana NO hay simulacro completo, solo topic-based.

6. **Aprovecha las 6h liberadas** por saltar secciones 3, 4, 5: úsalas en hands-on adicional, no en más videos.

7. **Apuntes regla 70/30:** 70% comparativas y patrones, 30% lineal. Si te encuentras transcribiendo, párate.

## 🤖 Apoyo con Claude después de cada día

Al cerrar cada día, abrir Claude y pedirle:

```
Acabo de ver la sección X del curso SAA. Aquí están mis apuntes:
[pegar el .md]

1. ¿Qué te falta importante para el SAA?
2. Genera 5 preguntas tipo examen sobre estos conceptos.
3. ¿Hay algún tip de examen que debería agregar a tips/?
```

## 📝 Checklist de cierre semanal (sábado 10 noche)

- [ ] Secciones 6, 7, 8, 9, 10, 11 completadas
- [ ] Doc maestro tiene mínimo 8 comparativas estructuradas
- [ ] Diagrama de arquitectura HA dibujado a mano y fotografiado
- [ ] Listas de vocabulario inglés actualizadas con términos nuevos
- [ ] `tips/tips-examen.md` con mínimo 15 tips
- [ ] Identificados los 2 temas más débiles para reforzar la próxima semana
- [ ] Recursos AWS apagados/eliminados (sin costos extras)
- [ ] Cost Explorer revisado (sin sorpresas)

---

*Próxima semana: S3 avanzado + CDN + Decoupling/Serverless + primer Dojo SAA*