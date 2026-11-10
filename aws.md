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
