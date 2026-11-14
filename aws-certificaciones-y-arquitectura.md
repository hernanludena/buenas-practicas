# AWS: certificaciones y arquitectura aplicada

**Ruta de estudio Solutions Architect Associate:** [Módulo 1 — Seguridad](#aws-solutions-architect--associate--módulo-1-seguridad) · [Módulo 2 — Arquitecturas resilientes](#aws-solutions-architect--associate--módulo-2-arquitecturas-resilientes-14-noviembre-2026). Se conservan también los apuntes anteriores de otras certificaciones y Delivery Loja.

Apuntes de estudio de Cloud Practitioner y Developer Associate y decisiones de arquitectura para Delivery Loja Enterprise (Java 21, Spring Boot, ECS/EC2). Fecha: noviembre de 2026. Verificar siempre la guía vigente de cada examen.

## Rutas de certificación
- Foundational: Cloud Practitioner, AI Practitioner.
- Associate: Solutions Architect, Developer, CloudOps Engineer, Data Engineer, Machine Learning Engineer.
- Professional: Solutions Architect, DevOps Engineer.
- Specialty: consultar el catálogo oficial actualizado.
- Ruta arquitectura sugerida: Cloud Practitioner → Solutions Architect Associate → Solutions Architect Professional.
- Ruta desarrollo sugerida: Cloud Practitioner → Developer Associate → DevOps Engineer Professional.
- No existen prerrequisitos obligatorios entre estos exámenes.

## Cloud Practitioner (CLF-C02)
| Dominio | Peso | Temas |
|---|---:|---|
| Conceptos de nube | 24% | IaaS/PaaS/SaaS, regiones y AZ, elasticidad, alta disponibilidad, Well-Architected |
| Seguridad y cumplimiento | 30% | Responsabilidad compartida, IAM, MFA, KMS, WAF, Shield, CloudTrail |
| Tecnología y servicios | 34% | EC2, Lambda, ECS, S3, RDS, DynamoDB, VPC, Route 53, ELB, CloudFront, SQS/SNS |
| Facturación y soporte | 12% | Free Tier, On-Demand, Reserved, Spot, Budgets, Cost Explorer, planes de soporte |

Orientación: reconocer el propósito de los servicios y escenarios de uso, no programarlos.

## Developer Associate (DVA-C02)
| Dominio | Peso | Tecnologías representativas |
|---|---:|---|
| Desarrollo con servicios AWS | 32% | Lambda, API Gateway, DynamoDB, S3, SQS, SNS, EventBridge, Step Functions |
| Seguridad | 26% | IAM, Cognito, KMS, Secrets Manager, OAuth2/OIDC/JWT |
| Despliegue | 24% | CodeBuild, CodeDeploy, CodePipeline, CloudFormation, SAM, Beanstalk |
| Troubleshooting y optimización | 18% | CloudWatch, X-Ray, logs, reintentos, idempotencia, rendimiento |

**Versiones:** porcentajes anteriores son de DVA-C02; revisar la guía de DVA-C03 si corresponde al examen elegido.

## Route 53, ELB, ALB y NLB
- Route 53 resuelve DNS hacia el endpoint (ALB o API Gateway); no es un salto HTTP en cada solicitud. DNS failover puede cambiar respuestas DNS según health checks y políticas, sujeto a cachés/TTL.
- ELB es la familia de balanceadores. No es un balanceador adicional delante de ALB.
- ALB: capa 7, HTTP/HTTPS, reglas por host/path, WebSocket; apropiado para APIs REST y Spring Boot en ECS.
- NLB: capa 4, TCP/UDP/TLS; útil para protocolos de transporte, alto rendimiento, baja latencia y requisitos específicos de red.
- GWLB: appliances virtuales de seguridad; CLB: legado.
- GPS no exige NLB: si el tracking usa HTTPS/WebSocket, ALB es compatible. Si usa protocolo TCP/UDP propio, considerar NLB.
- Riesgo SPOF: diseñar alta disponibilidad multi-AZ, health checks y escalado; no asumir que una sola instancia backend es HA.

## API Gateway frente a ALB
- API Gateway tiene HTTP API, REST API y WebSocket API. REST API ofrece, entre otras capacidades, usage plans y API keys; HTTP API suele ser más sencillo/económico para casos compatibles.
- ALB balancea y enruta tráfico HTTP; API Gateway administra exposición, autorización, throttling, cuotas y consumidores de APIs.
- Tener 3, 20 o 50 microservicios **no obliga** a usar API Gateway. Alta carga tampoco lo obliga.
- Ejemplo bancario B2B: socios consumen `POST /transfers` con autorización, cuotas por consumidor, monitoreo y versionado. Las API keys y cuotas no reemplazan autenticación/autorización robusta, controles antifraude ni límites de negocio.
- Para partners de delivery: exponer contratos específicos como `POST /partner/orders` en lugar de reutilizar indiscriminadamente endpoints internos.
- Si se justifica usar ambos: cliente → DNS Route 53 → API Gateway → VPC Link → ALB interno → servicios ECS (según tipo de API/integración admitida).

## Cognito y Spring Security
1. Login: app web/móvil → Cognito User Pool (opcional federación Google/Facebook) → tokens OAuth2/OIDC.
2. Solicitud API: app con access token Bearer → ALB → Spring Boot.
3. Spring Security OAuth2 Resource Server valida JWT (firma, issuer, expiración y audience/client según configuración) y autoriza por scopes/roles.
4. Reglas de negocio permanecen en backend: un cliente solo puede leer sus pedidos.
5. API Gateway puede añadir un JWT authorizer (según tipo de API); **no es obligatorio** para integrar Cognito.
6. ALB dispone de funciones de autenticación OIDC/Cognito en ciertos escenarios, pero no debe confundirse con un autorizador JWT genérico de APIs.

## Delivery Loja Enterprise: propuesta incremental
**Base:** app móvil/web → Route 53 (resolución DNS) → ALB público HTTPS → servicios Spring Boot en ECS sobre EC2 → PostgreSQL. Cognito autentica usuarios; Spring Security protege cada servicio. Merchants y Dispatch pueden tener despliegue/BD separados según las decisiones del proyecto. Considerar Redis, Kafka/outbox, observabilidad, autoscaling y multi-AZ según carga real y presupuesto.

**Evolución opcional:** API Gateway frente a servicios privados cuando se requieran políticas centralizadas, API products, cuotas por partners o integraciones B2B. Evaluar costo, latencia, seguridad y complejidad adicional. No añadir API Gateway solo por tener múltiples canales web/móvil.

## Preguntas rápidas de examen
- `/orders` y `/users` hacia backends distintos según ruta HTTP → ALB.
- Conexiones UDP de rastreo con protocolo propio → considerar NLB.
- Ejecutar código sin administrar servidores → Lambda.
- Resolver `api.midominio.com` → Route 53.
- Autenticar usuarios y emitir tokens → Cognito User Pools.
- Administrar APIs externas con cuotas y planes de uso → API Gateway REST API.
- Enviar tareas desacopladas → SQS; publicar a múltiples suscriptores → SNS; rutear eventos por reglas → EventBridge.

## Referencias oficiales
- [AWS Certification](https://aws.amazon.com/certification/)
- [Cloud Practitioner exam](https://aws.amazon.com/certification/certified-cloud-practitioner/)
- [Developer Associate exam](https://aws.amazon.com/certification/certified-developer-associate/)
- [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)
- [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [API Gateway private integrations](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vpc-links.html)
- [Amazon Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [Spring Security OAuth2 Resource Server](https://docs.spring.io/spring-security/reference/servlet/oauth2/resource-server/jwt.html)

## AWS Solutions Architect – Associate | Módulo 1: Seguridad

> Apuntes de preguntas y dudas recuperables de nuestras conversaciones. Se explican los conceptos; no se presentan como transcripción literal de preguntas que no están disponibles.

### 1. Responsabilidad compartida e IAM
- **Responsabilidad compartida:** AWS protege **la infraestructura de la nube** (centros de datos, hardware y servicios administrados); el cliente protege **lo que configura y ejecuta en la nube** (identidades, datos, permisos, aplicaciones, configuraciones). El reparto concreto cambia por servicio: en EC2 el cliente administra SO/parches; en Lambda AWS administra el SO subyacente.
- **IAM:** usuarios, grupos, roles y políticas. Aplicar **mínimo privilegio**, credenciales temporales mediante roles y MFA. Una **policy** define permisos; un **role** es una identidad asumible por servicios o usuarios.
- **Autenticación** = comprobar quién eres; **autorización** = decidir qué puedes hacer.
- **Cognito User Pools** autentica usuarios de aplicaciones y emite tokens; **Identity Pools** permite obtener credenciales AWS temporales. No confundir con IAM para administración de recursos.

### 2. Criptografía, HTTPS y TLS
- **Cifrado en tránsito:** TLS protege la comunicación entre cliente y servidor (HTTPS). **Cifrado en reposo:** protege datos almacenados (p. ej., S3, EBS, RDS) con claves administradas según configuración.
- **Simétrico:** una misma clave cifra y descifra; eficiente para datos. **Asimétrico:** clave pública/privada; útil para firmas e intercambio/autenticación de claves. **Hash:** función unidireccional para integridad; no es cifrado reversible.
- **AWS KMS:** administra claves criptográficas y permisos de uso; **Secrets Manager:** almacena y puede rotar secretos; **ACM:** aprovisiona/administra certificados TLS para servicios compatibles. No son intercambiables.
- **SSL vs TLS:** TLS es el protocolo vigente, sucesor de SSL; decir «certificado SSL» es uso coloquial, pero la conexión moderna emplea TLS.
- **TLS termination en ALB:** cliente establece HTTPS con ALB; ALB descifra, inspecciona HTTP y puede abrir otra conexión TLS hacia backend si se configura HTTPS. Si ALB→backend va por HTTP, ese tramo no está cifrado.
- **TLS pass-through:** el balanceador no descifra el tráfico; lo reenvía hasta backend, que termina TLS. Un NLB con listener TCP puede permitirlo; un listener TLS de NLB termina TLS. ALB, al operar a nivel HTTP, no ofrece pass-through TLS transparente.
- **Certificado digital:** permite autenticar al servidor y respaldar el establecimiento seguro de TLS; no confundir certificado con clave simétrica de sesión.

### 3. Modelo OSI y balanceadores
| Capa OSI | Función / ejemplo |
|---|---|
| 7 Aplicación | HTTP, DNS; reglas de ALB basadas en host/ruta HTTP |
| 6 Presentación | Formato/codificación; el modelo conceptual suele asociar cifrado aquí |
| 5 Sesión | Gestión de sesiones |
| 4 Transporte | TCP/UDP; NLB opera principalmente aquí |
| 3 Red | IP y enrutamiento |
| 2 Enlace de datos | Tramas, MAC |
| 1 Física | Señales y medio físico |

- **ELB** es la familia de balanceadores; **ALB** capa 7 (HTTP/HTTPS), **NLB** capa 4 (TCP/UDP/TLS). No son tres balanceadores colocados uno detrás de otro.
- **Sticky sessions (afinidad):** dirigir solicitudes sucesivas de un usuario al mismo target, normalmente mediante cookie en ALB. Útil para estado local heredado, pero crea dependencia de instancia; preferir aplicaciones stateless y sesiones externas cuando sea posible.
- **Health checks:** el balanceador detecta destinos no saludables y deja de elegirlos para solicitudes nuevas, sujeto a umbrales y tiempos de detección.
- **SPOF (single point of failure):** si un componente único falla, tumba el servicio. Dos instancias en AZ distintas y un ALB multi-AZ reducen SPOF; no garantizan ausencia total de errores.

### 4. Route 53, DNS y failover
- **Orden lógico:** el cliente consulta **Route 53 como DNS** para resolver el dominio; después se conecta al endpoint devuelto, por ejemplo **ALB**. **DNS failover no es un servidor adicional entre Route 53 y ALB:** es una política de respuesta DNS de Route 53.
- Route 53 puede devolver endpoint principal o secundario según políticas y comprobaciones de salud. El cambio puede retrasarse por **TTL y cachés DNS**.
- **Route 53 DNS failover** decide qué endpoint anunciar; **ALB** distribuye solicitudes HTTP entre targets de su target group.

### 5. Seguridad en red y aplicación
- **Security Groups:** firewall stateful asociado a recursos; reglas allow. **Network ACLs:** reglas stateless de permitir/denegar a nivel de subred.
- **VPC:** red virtual aislada; subred pública tiene ruta a Internet Gateway, una privada normalmente no tiene ruta directa hacia él. **NAT Gateway** permite conexiones salientes desde subred privada cuando está correctamente configurado.
- **AWS WAF:** filtra solicitudes web HTTP(S) con reglas; **AWS Shield:** protección DDoS; **CloudTrail:** auditoría de llamadas y actividad API; **CloudWatch:** métricas, logs y alarmas.
- **Defensa en profundidad:** HTTPS + WAF + políticas IAM mínimas + SG restrictivos + cifrado en reposo + observabilidad.

### 6. Ejemplo aplicado: Delivery Loja
Cliente móvil → consulta DNS Route 53 → HTTPS/TLS al ALB (certificado ACM, TLS termination) → ECS/EC2 Spring Boot en subredes privadas. ALB permite solo tráfico HTTPS entrante; SG de Spring Boot admite tráfico únicamente desde SG del ALB; RDS solo acepta conexiones desde SG de la aplicación. Cognito autentica usuarios y Spring Security valida JWT y autoriza acciones por rol y propiedad de pedidos. Secretos en Secrets Manager; cifrado con KMS según servicio.

### Preguntas rápidas del módulo 1
- ¿Sticky session equivale a guardar sesión en Redis? **No:** sticky dirige al mismo backend; Redis externaliza el estado.
- ¿ALB descifra HTTPS cuando termina TLS? **Sí.** Puede volver a cifrar hacia el backend.
- ¿TLS pass-through permite inspección HTTP en el balanceador? **No**, porque no descifra.
- ¿Route 53 es un salto de tráfico HTTP? **No:** responde DNS.
- ¿ALB vs NLB? **HTTP/rutas capa 7** vs **transporte capa 4**.
- ¿Un solo balanceador autogestionado puede ser SPOF? **Sí**; usar infraestructura de balanceo redundante/administrada.
- ¿KMS guarda contraseñas de bases de datos? **No es su función principal**; usar Secrets Manager.
- ¿Hash equivale a cifrado? **No:** el hash no está diseñado para descifrarse.

Referencias oficiales: [Responsabilidad compartida](https://aws.amazon.com/compliance/shared-responsibility-model/), [IAM](https://docs.aws.amazon.com/IAM/latest/UserGuide/introduction.html), [ACM](https://docs.aws.amazon.com/acm/latest/userguide/acm-overview.html), [ALB HTTPS](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/create-https-listener.html), [NLB listeners](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/load-balancer-listeners.html), [Route 53 failover](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html).

## AWS Solutions Architect – Associate | Módulo 2: Arquitecturas resilientes (14 noviembre 2026)

### Conceptos y diferencias
| Concepto | Qué significa | Ejemplo AWS / matiz |
|---|---|---|
| Resiliencia | Resistir, adaptarse y recuperarse de fallas | Multi-AZ, reintentos, backups y pruebas de recuperación |
| Redundancia | Recursos adicionales que evitan depender de uno solo | Dos tareas ECS/instancias EC2 en AZ diferentes |
| Replicación | Copiar y mantener datos en otros destinos, síncrona o asíncronamente | RDS Multi-AZ o S3 Replication |
| Alta disponibilidad (HA) | Minimizar indisponibilidad | ALB y backends Multi-AZ; puede haber errores breves |
| Tolerancia a fallos | Seguir operando ante fallas definidas sin interrupción perceptible | Redundancia activa y aislamiento de fallas; no basta con poner dos EC2 |
| Failover | Cambiar al recurso secundario ante falla | RDS Multi-AZ, Route 53 DNS failover |
| Failback | Regresar al recurso preferido tras recuperarlo | Reversión planificada al sitio principal |
| Disaster Recovery | Recuperación ante desastre mayor | Backup/restore, pilot light, warm standby, active-active |
| Backup | Copia recuperable de un punto en el tiempo | AWS Backup / snapshots; protege contra borrados replicados |
| RTO | Tiempo objetivo máximo para restaurar servicio | RTO 15 min: recuperar antes de 15 min |
| RPO | Antigüedad máxima tolerable de datos perdidos | RPO 5 min: como máximo 5 min de cambios; no porcentaje |
| SPOF | Componente cuya falla tumba el servicio | Una única instancia sin respaldo |
| Health check | Comprobar salud del destino | ALB evita enviar nuevas solicitudes a targets no saludables |
| Graceful degradation | Mantener funciones esenciales con funciones secundarias degradadas | Pedidos disponibles aunque recomendaciones fallen |
| Circuit breaker | Cortar temporalmente llamadas repetidamente fallidas | Resilience4j en Spring Boot |
| Escalabilidad | Capacidad de aumentar capacidad | Auto Scaling |
| Elasticidad | Ajustar capacidad a demanda | Auto Scaling escala hacia arriba/abajo |
| Multi-AZ | Recursos en zonas de disponibilidad diferentes de una región | ALB + EC2 en dos AZ; RDS Multi-AZ |
| Multi-Region | Recursos en regiones distintas | Sitio alterno para DR |

**No confundir:** dos EC2 con la misma aplicación son redundancia de cómputo; RDS manteniendo una copia de datos es replicación. La replicación proporciona redundancia de datos, pero puede propagar borrados; no sustituye backups. HA minimiza cortes; tolerancia a fallos busca continuidad ante un conjunto definido de fallas. Ninguna configuración promete cero errores de forma absoluta.

### DNS, balanceadores y failover
- **DNS** traduce nombres como `api.deliveryloja.com` a destinos resolubles; **Route 53** responde consultas DNS, no transporta cada solicitud HTTP.
- Flujo: cliente consulta DNS Route 53 → recibe dirección del **ALB** → envía HTTPS al ALB → ALB dirige a un target EC2/ECS saludable.
- **ELB** es la familia; **ALB** capa 7 HTTP/HTTPS, **NLB** capa 4 TCP/UDP/TLS.
- Route 53 puede apuntar a un ALB o usar varios endpoints con políticas **Failover**, **Weighted** o **Latency**. Con failover principal/secundario, responde normalmente con el principal y cambia al secundario cuando las verificaciones de salud y configuración lo indican. Caché DNS/TTL pueden demorar el cambio.
- Un ALB multi-AZ con dos backends evita el SPOF de una única instancia, pero las conexiones en curso pueden fallar y requieren reintentos/idempotencia.

### Mensajería Amazon SQS y DLQ
- Patrón: **Producer (Spring Boot API) → SQS Queue → Consumer (worker Java)**. SQS almacena y entrega mensajes; **no ejecuta** el trabajo.
- El productor usa API HTTPS. El worker recibe mensajes mediante polling (preferiblemente long polling), procesa y elimina con DeleteMessage al tener éxito. Si falla, tras el visibility timeout puede reintentarse.
- Mensajes: texto, JSON o XML como contenido. Ejemplo: `{"event":"ORDER_CREATED","orderId":123}`.
- **Standard:** entrega al menos una vez, posibles duplicados, orden no garantizado, alto rendimiento. **FIFO:** orden por message group y deduplicación en la cola; el consumidor igualmente debe ser idempotente.
- **DLQ (Dead Letter Queue):** otra cola asociada mediante redrive policy y `maxReceiveCount`; recibe mensajes que excedieron el límite de recepciones. No corrige errores ni reprocesa automáticamente por sí sola; investigar y usar redrive cuando corresponda.
- **SQS** es cola de trabajo con consumidores competidores; **SNS** es pub/sub; **EventBridge** enruta eventos por reglas.

### Almacenamiento, copias y resiliencia
- **S3 Replication:** copia objetos entre buckets; **SRR** dentro de la misma región y **CRR** entre regiones. Se activa versionado en origen/destino y una regla en origen. Objetos nuevos elegibles se copian de forma asíncrona; objetos previos requieren Batch Replication. No mueve ni borra automáticamente el original. No reemplaza backup.
- **AWS Backup:** centraliza políticas, programación, retención y recuperación de respaldos de servicios compatibles como RDS, EBS y DynamoDB; no es replicación en vivo.
- **EFS Regional:** sistema de archivos elástico compartido (NFS) para múltiples servidores Linux; datos redundantes en varias AZ. Distinguir de EFS One Zone.
- **EBS:** volúmenes de bloques persistentes para EC2, asociados a una AZ; reiniciar EC2 no borra por sí solo el volumen. Snapshots permiten restaurar/crear volúmenes. Un volumen suele adjuntarse a una instancia, con excepciones Multi-Attach en configuraciones compatibles.
- **S3:** almacenamiento de objetos; **EFS:** archivos compartidos; **EBS:** discos de bloques.

### Base de datos y caché
- **RDS Multi-AZ:** alta disponibilidad mediante standby/failover; la transición puede causar una interrupción breve. En despliegue clásico, standby no sirve lecturas.
- **RDS Read Replicas:** escalar SELECT; replicación generalmente asíncrona y posible lag. Se puede promover una réplica, pero no equivale al failover automático de Multi-AZ.
- **ElastiCache:** caché administrada en memoria para bajar latencia/carga de PostgreSQL. Configuraciones compatibles admiten réplicas y failover; la caché no reemplaza la base transaccional.

### Ejemplo aplicado: Delivery Loja
1. Cliente resuelve `api.deliveryloja.com` por Route 53; conecta por HTTPS al ALB.
2. ALB distribuye a dos o más tareas ECS/EC2 con Spring Boot en AZ distintas; health checks y capacidad de reserva.
3. PostgreSQL RDS Multi-AZ para HA, con backups y restauraciones probadas. Un failover de BD puede requerir reconexión/reintentos.
4. API publica trabajo asíncrono en SQS; worker consume, procesa idempotentemente y elimina; DLQ retiene mensajes problemáticos.
5. S3 guarda imágenes; CRR opcional si se justifica recuperación interregional; AWS Backup/snapshots para restaurar datos.
6. Definir RTO y RPO por proceso: pedidos/pagos requieren objetivos estrictos; analítica reconstruible puede tolerar más pérdida. Medirlos en pruebas.

### Preguntas de repaso
- ¿Dos EC2 detrás de ALB son replicación? **No necesariamente:** son redundancia de cómputo.
- ¿Replicar S3 mueve archivos? **No:** copia objetos y mantiene el origen.
- ¿RPO se expresa en porcentaje? **No:** tiempo de datos que se tolera perder.
- ¿SQS procesa los mensajes? **No:** el consumer/worker los procesa.
- ¿DLQ arregla mensajes? **No:** los conserva para inspección y reprocesamiento.
- ¿Route 53 balancea peticiones HTTP? **No:** responde DNS; ALB balancea HTTP.
- ¿Multi-AZ RDS equivale a Read Replica? **No:** HA/failover versus escalado de lecturas.
- ¿Replicación reemplaza backup? **No:** un borrado erróneo puede propagarse.

Referencias: [AWS Well-Architected Reliability](https://docs.aws.amazon.com/wellarchitected/latest/reliability-pillar/welcome.html), [Route 53 DNS failover](https://docs.aws.amazon.com/Route53/latest/DeveloperGuide/dns-failover.html), [SQS DLQ](https://docs.aws.amazon.com/AWSSimpleQueueService/latest/SQSDeveloperGuide/sqs-dead-letter-queues.html), [S3 Replication](https://docs.aws.amazon.com/AmazonS3/latest/userguide/replication.html), [RDS Multi-AZ](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/Concepts.MultiAZ.html).
