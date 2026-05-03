# Semana 1 (5-10 mayo) - Fundamentos + RDS + Route 53

> **Foco:** Bloques A (Fundamentos) + B (BD básicas) + C (Route 53/Arquitecturas)
> **Hito al cierre:** dominio sólido de IAM, EC2, ELB/ASG, RDS y Route 53

## 🎯 Objetivos de la semana

- ✅ Completar secciones 3 a 11 del curso
- ✅ Construir primeras notas comparativas (3 tipos)
- ✅ Hands-on real con IAM, EC2, EBS, ELB/ASG y RDS
- ✅ Hacer al menos 60 preguntas Dojo topic-based (no simulacro completo)
- ✅ Cerrar la semana con una arquitectura web HA desplegada manualmente

## 📅 Plan día por día

### 🟦 Lunes 5 de mayo - IAM y arranque (4-5h)

**Contenido:**
- [ ] Sección 3: Empezando con AWS (20 min)
- [ ] Sección 4: IAM y CLI de AWS (1h 10min)

**Hands-on (1h):**
- [ ] Crear usuario IAM con MFA habilitado
- [ ] Crear grupo "Developers" con política AWS managed
- [ ] Crear política custom (read-only S3 con condición de IP)
- [ ] Asumir rol con AWS CLI desde tu terminal
- [ ] Probar permisos con el simulador de políticas IAM

**Apuntes a construir:**
- Comparativa: **IAM Users vs Groups vs Roles**
- Tabla: tipos de políticas (AWS managed, customer managed, inline, resource-based)
- Patrón: cuándo usar Roles para EC2 / Lambda / cross-account

**Preguntas Dojo topic-based (20 preguntas - IAM):**
- [ ] Hacer 20 preguntas de IAM en modo topic
- [ ] Anotar errores en doc maestro

---

### 🟦 Martes 6 de mayo - EC2 fundamentos (4-5h)

**Contenido:**
- [ ] Sección 5: Fundamentos de EC2 (2h 12min)

**Hands-on (1h):**
- [ ] Lanzar instancia EC2 t2.micro (free tier)
- [ ] Configurar Security Groups (entrada SSH solo desde tu IP)
- [ ] Conectar via SSH (key pair)
- [ ] Probar User Data: instalar Apache automáticamente al lanzar
- [ ] Comparar tipos de instancias: General Purpose vs Compute Optimized vs Memory Optimized

**Apuntes a construir:**
- Tabla decisión: **tipos de instancias EC2** (cuándo cada familia)
- Comparativa: **modelos de pricing** (On-Demand / Reserved / Savings Plans / Spot / Dedicated)
- Patrón: cuándo usar Spot vs Reserved vs On-Demand

**Preguntas Dojo topic-based (20 preguntas - EC2):**
- [ ] Hacer 20 preguntas de EC2 fundamentos
- [ ] Anotar errores

---

### 🟦 Miércoles 7 de mayo - EC2 SAA + Storage EC2 (4-5h)

**Contenido:**
- [ ] Sección 6: EC2 - Nivel Solutions Architect Associate (51 min)
- [ ] Sección 7: Almacenamiento de instancias EC2 (1h 21min)

**Hands-on (1h):**
- [ ] Crear volumen EBS y adjuntarlo a instancia
- [ ] Hacer snapshot de EBS
- [ ] Crear AMI custom desde tu instancia
- [ ] Lanzar nueva instancia desde tu AMI
- [ ] Comparar EBS vs Instance Store (probar persistencia con stop/start)
- [ ] Crear EFS y montarlo en 2 instancias EC2 simultáneamente

**Apuntes a construir:**
- Comparativa CRÍTICA: **EBS vs EFS vs Instance Store vs FSx**
- Tabla: **tipos de volúmenes EBS** (gp3, gp2, io1/io2, st1, sc1) - cuándo cada uno
- Patrón: cuándo replicar EBS a otra AZ (snapshot) vs usar EFS multi-AZ

**Preguntas Dojo topic-based (20 preguntas - Storage EC2):**
- [ ] Hacer 20 preguntas de EBS/EFS/Instance Store
- [ ] Anotar errores

---

### 🟦 Jueves 8 de mayo - ELB y Auto Scaling (4-5h)

**Contenido:**
- [ ] Sección 8: Alta disponibilidad y escalabilidad: ELB y ASG (1h 44min)

**Hands-on (1.5h):**
- [ ] Crear ALB con 2 target groups (mínimo 2 AZ)
- [ ] Lanzar 2 EC2 detrás del ALB con páginas web distintas
- [ ] Configurar Health Checks
- [ ] Crear Launch Template
- [ ] Crear Auto Scaling Group con mín=2, max=4, desired=2
- [ ] Probar scaling: simular CPU alta y verificar que ASG escala
- [ ] Comparar ALB vs NLB en consola (qué configuración cambia)

**Apuntes a construir:**
- Comparativa CRÍTICA: **CLB vs ALB vs NLB vs GLB**
  - Capa OSI, casos de uso, sticky sessions, target types
- Tabla: **políticas de scaling** (target tracking, step, simple, scheduled)
- Patrón: arquitectura web HA con ALB + ASG multi-AZ

**Preguntas Dojo topic-based (20 preguntas - ELB/ASG):**
- [ ] Hacer 20 preguntas de balanceadores y autoscaling
- [ ] Anotar errores

---

### 🟦 Viernes 9 de mayo - RDS, Aurora, ElastiCache (4-5h)

**Contenido:**
- [ ] Sección 9: Fundamentos de AWS - RDS + Aurora + ElastiCache (1h 31min)

**Hands-on (1h):**
- [ ] Crear instancia RDS MySQL (t3.micro, free tier)
- [ ] Habilitar Multi-AZ deployment
- [ ] Crear Read Replica
- [ ] Conectarse desde EC2 a RDS (security groups)
- [ ] Hacer snapshot manual y restaurar
- [ ] (Opcional) crear cluster Aurora con 1 writer + 1 reader

**Apuntes a construir:**
- Comparativa CRÍTICA: **RDS vs Aurora vs DynamoDB vs ElastiCache**
- Tabla: **motores soportados por RDS** (MySQL, PostgreSQL, MariaDB, Oracle, SQL Server)
- Comparativa: **Multi-AZ vs Read Replicas** (HA vs performance)
- Comparativa: **Redis vs Memcached** (cuándo cada uno)
- Patrón: arquitectura web con RDS Multi-AZ + Read Replicas + ElastiCache

**Repaso semanal (1h):**
- [ ] Lectura horizontal de las notas de toda la semana
- [ ] Identificar qué temas siguen confusos
- [ ] Marcar 2-3 temas para reforzar el sábado

---

### 🟦 Sábado 10 de mayo - Route 53 + Arquitecturas + integración (6-8h)

**Contenido:**
- [ ] Sección 10: Route 53 (1h 42min)
- [ ] Sección 11: Discusiones sobre soluciones clásicas de arquitectura (49 min)

**Hands-on integral (2-3h) - PROYECTO DE LA SEMANA:**
> Desplegar una arquitectura web HA completa que integre todo lo visto

- [ ] Crear VPC con 2 subnets públicas y 2 privadas (2 AZ)
- [ ] Lanzar ALB en subnets públicas
- [ ] Crear ASG con EC2 en subnets privadas (mínimo 2)
- [ ] Configurar User Data: instalar nginx con página simple
- [ ] Crear RDS Multi-AZ en subnets privadas
- [ ] (Opcional) registrar dominio en Route 53 o usar uno existente
- [ ] Crear hosted zone y record A apuntando al ALB
- [ ] Probar en navegador
- [ ] **Dibujar el diagrama a mano** (importante para SAA)

**Apuntes a construir:**
- Tabla: **tipos de routing policies de Route 53** (simple, weighted, latency, failover, geolocation, geoproximity, multi-value)
- Comparativa: **Alias vs CNAME** (cuándo cada uno)
- Patrón: arquitectura web HA completa (el diagrama que acabas de dibujar)

**Preguntas Dojo topic-based (30 preguntas mixtas):**
- [ ] Hacer 30 preguntas mezcladas de toda la semana
- [ ] Revisar errores en profundidad
- [ ] Actualizar doc maestro con patrones detectados

---

### 🟦 Domingo 11 de mayo - Descanso

**Plan recomendado:**
- ❌ NO abrir AWS, Udemy, ni Dojo
- ✅ Actividad no técnica que disfrutes
- ✅ Dormir bien

**Opcional (máximo 30 min):**
- Lectura ligera de tu doc maestro de comparativas (sin agregar contenido)

---

## 📊 Métricas de control de la semana

Al cerrar el sábado, deberías tener:

| Métrica | Meta |
|---|---|
| Secciones del curso completadas | 9 de 34 (sec 3-11) |
| Horas netas dedicadas | ~25-30h |
| Notas comparativas creadas | Mínimo 8 tablas |
| Preguntas Dojo topic-based hechas | 110+ |
| Hands-on completados | 5 (uno por día L-V + integración sáb) |
| Arquitectura HA desplegada | ✅ 1 completa |

## 🚨 Señales de alarma

Si al **viernes 9** no has completado al menos hasta sección 9 (RDS):
- Mover Route 53 al lunes 12
- No incluir Sec 11 esta semana
- Aceptar atraso de medio día sin entrar en pánico

Si al **sábado 10** sientes que IAM, EC2 o EBS siguen confusos:
- Dedicar 1-2h del domingo a repaso (excepción al descanso)
- Volver a revisar las comparativas, no los videos
- Hacer 20 preguntas Dojo topic-based extra del tema débil

## 💡 Tips específicos para esta semana

1. **No transcribas a Stephane.** Cuando él compare 2 servicios, PAUSA el video y escribe TÚ la comparativa antes de seguir.

2. **Hands-on con timer.** Si llevas más de 1.5h en un hands-on, párate y sigue al video. La perfección es enemigo del avance.

3. **Free tier alert:** apaga/elimina recursos después de cada hands-on para no generar costos. Especialmente RDS y NAT Gateway.

4. **Dibuja a mano.** Para la arquitectura HA del sábado, hazla en papel o tablet. Los diagramas hechos a mano se aprenden mejor.

5. **El primer simulacro Dojo SAA es el sábado 17.** Esta semana NO hay simulacro completo, solo topic-based.

## 📝 Checklist de cierre semanal (sábado 10 noche)

- [ ] Todas las secciones 3-11 completadas
- [ ] Doc maestro tiene mínimo 8 comparativas estructuradas
- [ ] Diagrama de arquitectura HA dibujado a mano
- [ ] Listas de vocabulario inglés actualizadas con términos nuevos
- [ ] Identificados los 2 temas más débiles para reforzar la próxima semana
- [ ] Recursos AWS apagados/eliminados (sin costos extras)

---

*Próxima semana: S3 completo + CDN + Decoupling/Serverless + primer Dojo SAA*