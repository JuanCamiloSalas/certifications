[![](https://img.shields.io/badge/<-FF4859?style=for-the-badge)](../18_Other_Services/README.md)
[![](https://img.shields.io/badge/CONTENT_TABLE-175074?style=for-the-badge)](../README.md)

# Arquitectura y ecosistema de AWS

[![aws-links](https://img.shields.io/badge/WELL_ARCHITECTED_FRAMEWORK-orange?style=for-the-badge)](https://aws.amazon.com/architecture/well-architected)

## Well Architected Framework - Principios generales de orientación
- Deja de adivinar tus necesidades de capacidad 
- Testea sistemas a escala de producción 
- Automatiza para facilitar la experimentación arquitectónica 
- Permite arquitecturas evolutivas 
    - Diseña en función de los requisitos cambiantes 
- Impulsa las arquitecturas utilizando datos 
- Mejorar mediante días de juego 
    - Simular aplicaciones para días de venta flash

## Mejores prácticas en el Cloud de AWS - Principios de diseño
- **Escalabilidad:** vertical y horizontal
- **Recursos desechables:** los servidores deben ser desechables y fácilmente configurables
- **Automatización:** Sin servidor, infraestructura como servicio, autoescalado...
- **Acoplamiento:**
    - Los monolitos son aplicaciones que hacen más y más con el tiempo, se hacen más grandes
    - Divídela en componentes más pequeños y débilmente acoplados
    - Un cambio o un fallo en un componente no debería afectar en cascada a otros componentes
- **Servicios, no servidores:**
    - No utilices sólo EC2
    - Utiliza servicios gestionados, bases de datos, serverless, etc.

## Well Architected Framework - 6 Pilares

1) **Excelencia operativa**
2) **Seguridad**
3) **Fiabilidad**
4) **Eficiencia del rendimiento**
5) **Optimización de costes**
6) **Sostenibilidad**

> *No son algo a equilibrar, ni a compensar, son una sinergia*

## 1) Excelencia operativa

- Incluye la capacidad de **ejecutar y supervisar los sistemas** para aportar valor al negocio y **mejorar continuamente los procesos y procedimientos de soporte**.

- **Principios de diseño:**
  - **Realiza operaciones como código** — Infraestructura como código.
  - **Anotar la documentación** — Automatizar la creación de documentación anotada después de cada construcción.
  - **Realiza cambios frecuentes, pequeños y reversibles** — Para que, en caso de cualquier fallo, puedas revertirlo.
  - **Perfecciona los procedimientos de las operaciones con frecuencia** — Asegúrate de que los miembros del equipo estén familiarizados con ellos.
  - **Anticipa los fallos**
  - **Aprende de todos los fallos operativos**

### Servicios AWS - Excelencia operativa
![](./assets/first-pilar-services.png)

## 2) Seguridad
- Incluye la capacidad de **proteger la información, los sistemas y los activos** a la vez que se proporciona valor empresarial mediante evaluaciones de riesgo y estrategias de mitigación.
- **Principios de diseño:**
  - **Implementar una base sólida de identidad** — Centralizar la gestión de privilegios y reducir (o incluso eliminar) la dependencia de las credenciales a largo plazo. Principio de mínimo privilegio. IAM.
  - **Habilitar la trazabilidad** — Integrar logs y métricas con los sistemas para responder y actuar automáticamente.
  - **Aplicar la seguridad en todas las capas** — Como red de borde, VPC, subred, equilibrador de carga, cada instancia, sistema operativo y aplicación.
  - **Automatizar las mejores prácticas de seguridad**
  - **Protege los datos en tránsito y en reposo** — Cifrado, tokenización y control de acceso.
  - **Mantén a las personas alejadas de los datos** — Reduce o elimina la necesidad de acceso directo o procesamiento manual de los datos.
  - **Prepárate para los eventos de seguridad** — Realiza simulaciones de respuesta a incidentes y utiliza herramientas con automatización para aumentar la velocidad de detección, investigación y recuperación.
  - **Modelo de responsabilidad compartida**

### Servicios AWS - Seguridad
![](./assets/second-pilar-services.png)

## 3) Fiabilidad
- Capacidad de un sistema para recuperarse de las interrupciones de la infraestructura o del servicio, adquirir dinámicamente recursos informáticos para satisfacer la demanda y mitigar las interrupciones, como las desconfiguraciones o los problemas transitorios de la red.
- **Principios de diseño:**
  - **Prueba los procedimientos de recuperación** — Utiliza la automatización para simular diferentes fallos o para recrear escenarios que hayan provocado fallos anteriormente.
  - **Recupérate automáticamente de los fallos** — Anticipa y remedia los fallos antes de que se produzcan.
  - **Escala horizontalmente para aumentar la disponibilidad agregada del sistema** — Distribuye las peticiones entre múltiples recursos más pequeños para asegurar que no comparten un punto de fallo común.
  - **Deja de adivinar la capacidad** — Mantén el nivel óptimo para satisfacer la demanda sin aprovisionamiento excesivo o insuficiente. Utiliza el escalado automático.
  - **Gestiona el cambio en la automatización** — Utiliza la automatización para realizar cambios en la infraestructura.

### Servicios AWS - Fiabilidad
![](./assets/third-pilar-services.png)

## 4) Eficiencia del rendimiento
- Incluye la capacidad de **utilizar los recursos informáticos de forma eficiente** para satisfacer los requisitos del sistema, y de mantener esa eficiencia a medida que cambia la demanda y evolucionan las tecnologías.
- **Principios de diseño:**
  - **Democratizar las tecnologías avanzadas** — Las tecnologías avanzadas se convierten en servicios y, por tanto, puedes centrarte más en el desarrollo de productos.
  - **Hazte global en minutos** — Despliegue fácil en múltiples regiones.
  - **Utiliza arquitecturas sin servidor** — Evita la carga de gestionar servidores.
  - **Experimenta más a menudo** — Es fácil realizar pruebas comparativas.
  - **Simpatía mecánica** — Conoce todos los servicios de AWS.

### Servicios AWS - Eficiencia del rendimiento
![](./assets/fourth-pilar-services.png)

## 5) Optimización de costes
- Incluye la capacidad de **ejecutar sistemas para ofrecer valor empresarial al precio más bajo**.
- **Principios de diseño:**
  - **Adopta un modo de consumo** — Paga sólo por lo que usas.
  - **Medir la eficiencia global** — Utilizar CloudWatch.
  - **Deja de gastar dinero en las operaciones del centro de datos** — AWS se encarga de la parte de la infraestructura y permite al cliente centrarse en los proyectos de la organización.
  - **Analiza y atribuye el gasto** — La identificación precisa del uso y los costes del sistema ayuda a medir el retorno de la inversión (ROI). Asegúrate de utilizar etiquetas.
  - **Utiliza servicios gestionados y a nivel de aplicación para reducir el coste de propiedad** — Como los servicios gestionados operan a escala del Cloud, pueden ofrecer un menor coste por transacción o servicio.

### Servicios AWS - Optimización de costes
![](./assets/fifth-pilar-services.png)

## 6) Sostenibilidad
- El pilar de la sostenibilidad se centra en minimizar el impacto medioambiental de la ejecución de cargas de trabajo en el Cloud.
- Principios de diseño
  - **Comprende tu impacto** - establece indicadores de rendimiento, evalúa las mejoras
  - **Establece objetivos de sostenibilidad** - Establece objetivos a largo plazo para cada carga de trabajo, modela el retorno de la inversión (ROI)
  - **Maximizar la utilización** - Dimensionar correctamente cada carga de trabajo para maximizar la eficiencia energética del hardware subyacente y minimizar los recursos ociosos.
  - **Anticipa y adopta nuevas ofertas de hardware y software más eficientes** - y diseña la flexibilidad para adoptar nuevas tecnologías con el tiempo.
  - **Utiliza servicios gestionados** - los servicios compartidos reducen la cantidad de infraestructura; los servicios gestionados ayudan a automatizar las mejores prácticas de sostenibilidad, como mover los datos a los que se accede con poca frecuencia al almacenamiento en frío y ajustar la capacidad de computación.
  - **Reduce el impacto descendente de tus cargas de trabajo en el Cloud** - Reduce la cantidad de energía o recursos necesarios para utilizar tus servicios y reduce la necesidad de que tus clientes actualicen sus dispositivos

### Servicios AWS - Sostenibilidad
![](./assets/sixth-pilar-services.png)
