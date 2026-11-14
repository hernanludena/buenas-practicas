# AWS: recordatorio de servicios

| Nombre | Descripción breve |
|---|---|
| Lambda | Compute serverless por invocación; AWS administra la infraestructura subyacente y se aplican cuotas/límites. |
| API Gateway | Publica APIs HTTP y WebSocket y conecta rutas con backends. |
| ALB / ELB | ALB puede balancear HTTP y usar Lambda targets; ELB es la familia de balanceadores. |
| EC2 | Máquina virtual; no es una VPN. Para VPN usar Client VPN o Site-to-Site VPN. |
| ECS / EKS / Fargate | Orquestar contenedores: ECS o EKS; Fargate ofrece compute administrado sin gestionar hosts. |
| ECR | Registro de imágenes Docker. |
| App Runner | Despliegue administrado de aplicaciones web/APIs desde código o contenedor; contrastar costo y requisitos con ECS. |
| S3 / CloudFront | S3 almacena objetos; CloudFront distribuye contenido como CDN. Juntos sirven frontend estático con permisos y HTTPS bien configurados. |
| Amplify Hosting | Hosting y despliegue conectado al repositorio; puede usarse sin backend Amplify. |
| Amplify Gen 2 | Backend full stack code-first con TypeScript, que aprovisiona recursos AWS mediante código. |
| AppSync GraphQL / Events | GraphQL ofrece API GraphQL; Events ofrece pub/sub en tiempo real. Distinguirlos al diseñar el frontend. |
| Cognito | User Pools autentican usuarios y federan proveedores; Identity Pools entregan credenciales AWS federadas. |
| IAM / Secrets Manager | Permisos de mínimo privilegio y almacenamiento/rotación de secretos. |
| RDS / Aurora | Bases relacionales administradas; comparar motores, disponibilidad, escalado y costo. |
| DynamoDB | Base NoSQL; diseñar por patrones de acceso, claves e índices. |
| DynamoDB Streams | CDC casi en tiempo real de modificaciones de ítems; puede apoyar Outbox en DynamoDB, no sustituye todos los patrones Outbox. |
| ElastiCache | Caché administrada compatible con motores como Redis OSS/Valkey según región/oferta. |
| SQS / SNS / EventBridge | Cola de trabajo, pub/sub y bus/ruteo de eventos más scheduler, respectivamente. |
| Step Functions | Orquesta workflows; Request Response, .sync y callback task token dependen del servicio y tipo de workflow. |
| MSK | Kafka administrado; justificar complejidad y costo frente a SQS/EventBridge/RabbitMQ. |
| DocumentDB | Servicio compatible con MongoDB hasta cierto nivel; verificar compatibilidad antes de adoptarlo. |
| Route 53 | DNS administrado. |
| AWS Budgets | Presupuestos y alertas de gasto; revisar también costos reales y recursos activos. |
| Amazon Location Service | APIs de mapas/localización; comparar cobertura, proveedor, precios y términos en el checkout. |
| Pruebas de carga | Ejecutar antes de producción en entornos autorizados con límites de gasto y métricas. |

| Alternativa frontend | Recordatorio |
|---|---|
| S3 + CloudFront | Más configuración y control; automatizar con IaC/CI e incluir HTTPS, DNS, permisos y caché. |
| Amplify Hosting | Menos configuración de despliegue; verificar framework, SSR y costos de build/hosting. |

Referencias: [EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html), [Client VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html), [DynamoDB Streams](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html), [Outbox](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html), [Step Functions](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html), [Amplify Gen 2](https://docs.aws.amazon.com/amplify/latest/userguide/deploy-backend.html).


## Arquitecturas resilientes — guía de estudio (14 noviembre 2026)

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
