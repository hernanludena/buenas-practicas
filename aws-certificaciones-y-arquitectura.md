# AWS: certificaciones y arquitectura aplicada

**Ruta de estudio Solutions Architect Associate:** [Módulo 1 — Seguridad](#aws-solutions-architect--associate--módulo-1-seguridad) · [Módulo 2 — Arquitecturas resilientes](#aws-solutions-architect--associate--módulo-2-arquitecturas-resilientes-14-noviembre-2026). Se conservan también los apuntes anteriores de otras certificaciones y Delivery Loja.

Apuntes de estudio de Cloud Practitioner y Developer Associate y decisiones de arquitectura para Delivery Loja Enterprise (Java 21, Spring Boot, ECS/EC2). Fecha: noviembre de 2026. Verificar siempre la guía vigente de cada examen.

## Índice de estudio

- [Módulo 1 — Seguridad](#aws-solutions-architect--associate--módulo-1-seguridad)
  - Responsabilidad compartida e IAM
  - Criptografía, HTTPS y TLS
  - Modelo OSI y balanceadores
  - Route 53, DNS y failover
  - Seguridad en red y aplicación
  - Ejemplo Delivery Loja y preguntas de repaso
- [Módulo 2 — Arquitecturas resilientes](#aws-solutions-architect--associate--módulo-2-arquitecturas-resilientes-14-noviembre-2026)
  - Resiliencia, redundancia, replicación, HA, tolerancia a fallos
  - RTO, RPO, recuperación y failover
  - SQS, DLQ, S3, EBS, EFS, RDS, ElastiCache
  - Ejemplo Delivery Loja y preguntas de repaso
- [Preguntas recuperadas — Practitioner y Developer](#preguntas-recuperadas-de-conversaciones-anteriores--practitioner-y-developer)
- [Cloud Practitioner — fundamentos y dudas](#cloud-practitioner--fundamentos-y-dudas-explicadas)
- [Developer Associate — desarrollo y dudas](#developer-associate--desarrollo-y-dudas-explicadas)
- [Rutas de certificación](#rutas-de-certificación)
- [Arquitectura aplicada a Delivery Loja](#delivery-loja-enterprise-propuesta-incremental)
- [Referencias oficiales](#referencias-oficiales)

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

## Guía de repaso — Cloud Practitioner y Developer Associate

> Consolidación de conceptos discutidos y aplicados en Delivery Loja. Estas son preguntas de repaso redactadas para estudiar, **no** transcripciones literales de conversaciones anteriores. El temario y los códigos de examen deben contrastarse con las guías oficiales vigentes.

### Cloud Practitioner — fundamentos y dudas explicadas
| Pregunta | Respuesta y explicación |
|---|---|
| ¿Qué es AWS y qué es cloud computing? | AWS ofrece servicios de cómputo, almacenamiento, redes y datos bajo demanda. La nube permite aprovisionar recursos sin comprar y administrar todo el hardware físico. |
| ¿IaaS, PaaS y serverless son iguales? | No. IaaS ofrece infraestructura virtual (EC2); servicios administrados abstraen más operación (RDS); Lambda ejecuta funciones sin administrar servidores, pero conserva responsabilidades de configuración y seguridad. |
| ¿Región y Availability Zone son lo mismo? | No. Una región contiene varias AZ aisladas; desplegar en dos AZ protege frente a la caída de una zona, no necesariamente de toda la región. |
| ¿Alta disponibilidad y tolerancia a fallos son iguales? | No. HA minimiza interrupciones; tolerancia a fallos busca continuidad ante fallas definidas sin interrupción perceptible. |
| ¿Elasticidad y escalabilidad? | Escalabilidad es capacidad de crecer; elasticidad es ajustar capacidad dinámicamente según demanda. |
| ¿Quién protege los datos? | Responsabilidad compartida: AWS protege infraestructura de nube; el cliente administra permisos, clasificación, configuración y uso de datos según servicio. |
| ¿EC2, Lambda y ECS? | EC2 es servidor virtual; Lambda ejecuta funciones por eventos; ECS orquesta contenedores y puede ejecutarlos sobre EC2 o Fargate. |
| ¿S3, EBS y EFS? | S3 objetos; EBS bloques/disco para EC2; EFS sistema de archivos compartido NFS. |
| ¿CloudWatch y CloudTrail? | CloudWatch observa métricas/logs/alarmas; CloudTrail registra actividad y llamadas API para auditoría. |
| ¿Cómo se controla el gasto? | Budgets para alertas, Cost Explorer para analizar costos; revisar recursos activos, tarifas y cuotas del Free Tier. |
| ¿Qué significa RTO y RPO? | RTO es objetivo de tiempo de recuperación; RPO es máximo período de datos que se tolera perder. |
| ¿Qué hace Route 53? | Resuelve DNS; con failover puede cambiar el endpoint anunciado, pero no balancea cada petición HTTP como ALB. |

### Developer Associate — desarrollo y dudas explicadas
| Pregunta | Respuesta y explicación |
|---|---|
| ¿API Gateway y ALB son iguales? | No. API Gateway gestiona publicación/controles de APIs; ALB enruta y balancea tráfico HTTP. Pueden usarse por separado o combinados según requisitos. |
| ¿Cuándo elegir Lambda? | Para tareas event-driven y APIs con cargas compatibles con límites y costos; no por obligación de usar serverless. |
| ¿SQS, SNS y EventBridge? | SQS desacopla trabajo en cola; SNS publica a múltiples suscriptores; EventBridge enruta eventos por reglas. |
| ¿Quién procesa un mensaje SQS? | El consumidor/worker, no la cola. El worker confirma éxito eliminando el mensaje; reintentos pueden duplicar entregas. |
| ¿Standard o FIFO? | Standard prioriza escala sin orden garantizado y entrega al menos una vez; FIFO mantiene orden por grupo y deduplicación dentro de sus garantías. Diseñar consumidores idempotentes. |
| ¿Para qué sirve una DLQ? | Retiene mensajes que fallaron repetidamente; no los corrige ni los reprocesa sola. |
| ¿Qué es idempotencia? | Repetir la misma operación no debe causar efectos adicionales, fundamental en reintentos de pagos/pedidos. |
| ¿Qué hace Cognito y qué hace Spring Security? | Cognito puede autenticar y emitir tokens; Spring Security valida tokens y aplica autorización en el backend. |
| ¿KMS, Secrets Manager y ACM? | KMS administra claves; Secrets Manager secretos; ACM certificados TLS. |
| ¿Qué es Outbox? | Persistir cambio de negocio y evento en una misma transacción de base de datos y publicarlo después mediante worker/CDC para evitar inconsistencias. |
| ¿Qué es DynamoDB Streams? | Flujo de cambios de ítems de DynamoDB; permite reaccionar a modificaciones sin hacer polling completo. |
| ¿Qué hace Step Functions? | Orquesta workflows con pasos, reintentos y decisiones; distinto de una cola SQS. |
| ¿Cómo desplegar contenedores? | GitHub Actions o CI construye imagen → ECR almacena imagen → ECS despliega servicio en EC2/Fargate. |
| ¿Cómo depurar errores? | Logs/métricas/alarmas con CloudWatch, trazas cuando corresponda, DLQ y correlación por request/order ID. |

### Ejemplo integrado de estudio: Delivery Loja
App móvil → Route 53 (DNS) → ALB HTTPS → ECS/EC2 Spring Boot → RDS PostgreSQL. Cognito autentica; Spring Security autoriza. Para procesos asíncronos, API → SQS → worker idempotente → DLQ para fallos persistentes. S3 almacena imágenes, CloudWatch observa el sistema, y Secrets Manager/KMS ayudan a proteger secretos y datos. Esta arquitectura combina fundamentos de Cloud Practitioner, desarrollo de Developer Associate y resiliencia de Solutions Architect.

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


## Preguntas recuperadas de conversaciones anteriores — Practitioner y Developer

> Estas preguntas corresponden a dudas efectivamente identificadas en conversaciones anteriores. Se normaliza su redacción para facilitar el estudio; no se presentan como citas textuales. Los ejemplos amplían la explicación.

### Cloud Practitioner: dudas planteadas

**1. ¿Cloud Practitioner y Developer Associate son la misma certificación?** No. Cloud Practitioner es de nivel Foundational y evalúa fundamentos de AWS, nube, seguridad, servicios y facturación. Developer Associate es de nivel Associate y se centra en desarrollar, desplegar, proteger y solucionar problemas de aplicaciones en AWS. **Ejemplo:** identificar qué es Lambda corresponde al nivel fundamental; implementar una función que consume SQS con reintentos e idempotencia es un caso de desarrollo.

**2. ¿Qué módulos, servicios y tecnologías evalúa Cloud Practitioner?** Los dominios de CLF-C02 son conceptos de nube (24%), seguridad y cumplimiento (30%), tecnología y servicios (34%) y facturación, precios y soporte (12%). Servicios representativos: IAM, EC2, Lambda, ECS, S3, EBS, EFS, RDS, DynamoDB, VPC, Route 53, ELB, CloudFront, SQS, SNS, CloudWatch, CloudTrail, KMS y Budgets. No exige implementar cada servicio en código.

**3. ¿ALB también entra en Cloud Practitioner?** Sí, dentro de los conceptos de balanceo y Elastic Load Balancing. Hay que reconocer su propósito y cuándo usarlo.

**4. ¿Qué son ELB, ALB y NLB y dónde se usan?** ELB es la familia de servicios. ALB enruta HTTP/HTTPS a nivel de aplicación (capa 7), incluso por ruta como `/orders`. NLB trabaja con conexiones de transporte TCP/UDP/TLS (capa 4). **Ejemplo Delivery Loja:** ALB delante de la API REST Spring Boot; NLB sería una alternativa para un protocolo de tracking propio basado en UDP. Usar GPS no obliga por sí solo a utilizar NLB.

**5. ¿Qué certificación sigue a Cloud Practitioner? ¿Existe Cloud Professional?** No hay una certificación AWS cuyo nombre sea simplemente «Cloud Professional». Existen certificaciones Professional específicas, como Solutions Architect – Professional y DevOps Engineer – Professional. Tras Practitioner puedes estudiar directamente Solutions Architect – Associate o Developer – Associate; no hay prerrequisito obligatorio.

**6. ¿Para estudiar arquitectura tengo que obtener primero Developer Associate o puedo ir directamente a Solutions Architect – Associate? ¿Cuál es más compleja?** Puedes ir directamente a Solutions Architect – Associate. Esta evalúa decisiones de diseño, seguridad, resiliencia, rendimiento y costo; Developer Associate enfatiza la implementación y el ciclo de vida de aplicaciones. La dificultad relativa depende de tu experiencia; para un desarrollador Java, Developer puede resultar más familiar, pero no es un paso obligatorio.

**7. ¿Cuál es el temario de Solutions Architect – Associate frente a Developer Associate?** Solutions Architect se enfoca en diseñar arquitecturas seguras, resilientes, de alto rendimiento y optimizadas en costos. Developer se enfoca en desarrollo con servicios AWS, seguridad, despliegue y resolución de problemas. Un mismo servicio, como SQS, se estudia desde la selección arquitectónica en el primero y desde el consumo, errores e idempotencia en el segundo.

### Developer Associate: dudas planteadas

**8. ¿Qué módulos hay en Developer Associate?** En el temario DVA-C02: desarrollo con servicios AWS (32%), seguridad (26%), despliegue (24%) y solución de problemas/optimización (18%). Verificar el código y la guía vigentes antes de programar el examen. Servicios frecuentes: Lambda, API Gateway, DynamoDB, S3, SQS, SNS, EventBridge, Step Functions, IAM, Cognito, KMS, CloudWatch y herramientas de CI/CD.

**9. ¿Qué habíamos dicho sobre API Gateway?** Es una puerta de entrada administrada para APIs: define rutas, integraciones, autenticación/autorización y controles como throttling; algunas capacidades dependen del tipo de API. No es equivalente a ALB y no se necesita automáticamente por tener muchos microservicios. **Ejemplo:** socios externos de Delivery Loja consumen `POST /partner/orders` a través de API Gateway con controles de acceso y límites, mientras ALB distribuye HTTP hacia servicios ECS cuando esa combinación se justifica.

**10. ¿Cuándo conviene API Gateway en vez de ALB?** API Gateway cuando necesitas características de administración y exposición de APIs, como authorizers, cuotas o planes de uso en REST APIs. ALB cuando necesitas distribuir solicitudes HTTP/HTTPS a múltiples servicios/instancias y enrutar por host o path. Ambos pueden coexistir; evaluar costos y complejidad.

### Mapa de lo documentado y lo pendiente

- **Confirmado como pregunta recuperada:** los diez temas anteriores (algunos agrupan varias preguntas relacionadas).
- **Ya explicado en otras secciones:** IAM, KMS, Cognito, ACM, TLS, cifrado, Route 53, sticky sessions, SQS, DLQ, Multi-AZ, RTO/RPO, backups, redundancia y replicación.
- **Límite de recuperación:** no se dispone de una transcripción íntegra de todas las sesiones anteriores. No atribuir al usuario como pregunta literal ninguna pregunta didáctica creada para repaso.

Referencias: [Cloud Practitioner](https://aws.amazon.com/certification/certified-cloud-practitioner/), [Developer Associate](https://aws.amazon.com/certification/certified-developer-associate/), [Solutions Architect Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/), [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html), [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html).


### Continuación de dudas reales — Auto Scaling, ALB, SPOF, Health Checks y RDS Multi-AZ (14 noviembre 2026)

**¿Auto Scaling se aplica a cualquier servicio o a puertos?** No. Los puertos (80, 443, 8080) transportan tráfico; no son recursos escalables. EC2 Auto Scaling ajusta instancias EC2; ECS Service Auto Scaling ajusta tareas; Application Auto Scaling soporta capacidades de servicios compatibles, como DynamoDB. Lambda ajusta concurrencia mediante su propio modelo y cuotas; Aurora Serverless tiene escalado propio. Cada servicio tiene reglas y límites diferentes.

**¿Dónde se configura? ¿Hay políticas?** Sí: consola AWS, Terraform, CloudFormation, CLI o SDK. Para EC2: crear Launch Template; crear Auto Scaling Group con subredes/AZ, mínimo, deseado y máximo; asociar Target Group del ALB; definir políticas como target tracking de CPU promedio al 60 %. CloudWatch proporciona métricas. Ejemplo: mínimo 2, deseado 2, máximo 5; con CPU promedio elevada el grupo puede aumentar instancias y, al bajar la carga, reducirlas. No se garantiza que el CPU baje inmediatamente a 60 %: depende de tráfico, tiempos de arranque y configuración.

**¿Qué hace ALB y qué hace ASG?** ALB distribuye nuevas solicitudes HTTP/HTTPS entre targets saludables según health checks y reglas; ASG administra cantidad/capacidad de EC2 y reemplaza instancias declaradas no saludables. ALB no crea EC2 y ASG no distribuye peticiones. Juntos favorecen disponibilidad.

**¿Qué es SPOF?** Un punto único cuya caída afecta al servicio. Tres EC2 que dependen de una única base de datos sin respaldo pueden seguir teniendo SPOF en la BD. Reducir con despliegue multi-AZ, redundancia, failover, respaldos y revisión de dependencias.

**¿Dónde se configuran y quién ejecuta los Health Checks?** En EC2 → Target Groups → Health checks se define protocolo, puerto, ruta, intervalos, timeout y umbrales. El ALB realiza las comprobaciones a sus targets. En EC2 → Auto Scaling Groups → Health checks se puede habilitar el uso del estado de Elastic Load Balancing para decidir reemplazos, además de las verificaciones de EC2. No basta con que ALB marque unhealthy para garantizar reemplazo por ASG si esa integración no está habilitada.

**Ejemplo Spring Boot:** exponer `GET /actuator/health` mediante Spring Boot Actuator, en el puerto 8080 si ese es el puerto real de la app; configurar en Target Group HTTP, puerto de tráfico, path `/actuator/health`, intervalo 30 segundos y umbral unhealthy de 2 o 3 verificaciones. Proteger el acceso con Security Groups y asegurar respuesta HTTP 200 saludable. Si falla repetidamente, ALB evita enviar tráfico a ese target (con matices como fail-open cuando todos están unhealthy); ASG puede reemplazarlo si usa health checks del balanceador. La ruta debe existir y estar accesible desde el ALB.

**¿Qué es RDS Multi-AZ?** Una opción de alta disponibilidad para bases de datos RDS. En la modalidad tradicional de instancia Multi-AZ, RDS mantiene un standby síncrono en otra AZ y realiza failover automático ante fallas compatibles. Puede haber una interrupción breve; no es una garantía de cero downtime ni un backup para borrados lógicos. Existen también implementaciones Multi-AZ DB cluster con características distintas. Read Replicas se orientan principalmente a escalar lecturas y usan replicación que puede tener retraso.

**¿Cómo se relaciona con RTO/RPO?** RTO = tiempo objetivo de recuperación; RPO = pérdida de datos tolerable expresada como tiempo; SLA = compromiso formal que puede contener esos objetivos. RDS Multi-AZ reduce el tiempo de recuperación ante ciertos fallos, pero no promete un RTO universal. Backups y pruebas de restauración siguen siendo necesarios.

**Resumen de aprendizaje:** ALB = enruta a destinos sanos; ASG = escala y reemplaza EC2; health check = detecta problemas; SPOF = dependencia única crítica; RDS Multi-AZ = redundancia de base de datos con failover. Diseñar y probar estos mecanismos para alcanzar RTO/RPO, no asumir que los garantizan.
