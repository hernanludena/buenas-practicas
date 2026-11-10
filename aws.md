# AWS: mapa breve de servicios

Recordatorio de responsabilidades; escoger cada servicio según el caso, costo, operación y requisitos del sistema.

| Servicio | Para recordar |
|---|---|
| Lambda | Ejecuta funciones bajo demanda en infraestructura administrada por AWS. Es compute serverless; no significa que no existan servidores. API Gateway suele exponer APIs HTTP/WebSocket. |
| API Gateway | Entrada administrada para APIs HTTP y WebSocket; aplica rutas, autenticación, cuotas e integración con backends. |
| Application Load Balancer (ALB) / Elastic Load Balancing | Balancea tráfico HTTP/HTTPS entre targets; ALB puede integrar targets Lambda. No es necesario para “unificar” Lambdas si API Gateway ya resuelve la entrada. ELB es la familia; ALB, NLB y GWLB son tipos distintos. |
| EC2 | Máquinas virtuales configurables. EC2 no es una VPN; AWS Client VPN y Site-to-Site VPN son servicios de VPN distintos. |
| ECS / EKS / Fargate | ECS orquesta contenedores en AWS; EKS administra Kubernetes; Fargate es compute serverless para tareas/Pods de ECS/EKS sin administrar servidores EC2. |
| ECR | Registro administrado para imágenes de contenedor. |
| App Runner | Servicio administrado para compilar/desplegar aplicaciones web y APIs desde código o imagen de contenedor; comparar encaje y costos con ECS/Fargate y otras opciones. |
| S3 / CloudFront | S3 almacena objetos y puede alojar assets estáticos; CloudFront distribuye contenido como CDN. Para frontend React estático, configurar HTTPS, permisos, DNS/certificados y despliegue. |
| Amplify Hosting / Amplify Gen 2 | Hosting facilita conexión a Git y despliegues. Gen 2 define backend full stack con TypeScript y puede integrar autenticación, datos/API, funciones y recursos AWS. Hosting puede usarse sin adoptar el backend Amplify. No es simplemente “Vercel”: comparar flujo, SSR, costos y control requerido. |
| AppSync GraphQL / AppSync Events | GraphQL proporciona una API GraphQL administrada; Events ofrece publicación/suscripción en tiempo real. Son modalidades distintas de AppSync. |
| Cognito | User Pools gestionan registro y autenticación; puede federarse con proveedores sociales como Google y Facebook. Identity Pools otorgan credenciales AWS federadas. |
| IAM / Secrets Manager | IAM controla identidades, roles y permisos con mínimo privilegio; Secrets Manager almacena y rota secretos. Nunca guardar contraseñas o llaves en el repo. |
| RDS / DocumentDB | RDS administra bases relacionales compatibles con motores soportados; elegir motor/tamaño/HA según requisitos. DocumentDB es compatible con APIs/uso de MongoDB en cierto grado, no debe describirse como MongoDB idéntico: validar compatibilidad. |
| DynamoDB / DynamoDB Streams | DynamoDB es NoSQL administrada. Streams captura cambios de ítems para consumo casi en tiempo real y puede apoyar CDC/outbox en diseños DynamoDB; no es sinónimo universal de Outbox. La retención del stream es limitada, considerar reintentos y consumidores. |
| ElastiCache | Caché administrado compatible con motores como Redis OSS/Valkey según oferta/región; útil para datos calientes, no como fuente de verdad por defecto. |
| SQS / SNS / EventBridge | SQS desacopla consumidores con colas; SNS distribuye notificaciones/pub-sub; EventBridge enruta eventos y tiene Scheduler para tareas temporizadas. No son intercambiables. |
| Step Functions | Orquestación administrada con máquina de estados. Patrones: Request Response, Run a Job (.sync) y Callback con task token; las integraciones y patrones disponibles dependen del servicio/workflow. Callback espera hasta que llegue respuesta o venza el timeout/cuota aplicable, no es espera ilimitada ni siempre gratuita. |
| MSK | Kafka administrado por AWS; evaluar cuando se requieren capacidades/ecosistema Kafka y el costo operativo se justifica. |
| Amazon Location Service | Servicios de mapas/localización; evaluar proveedor, cobertura, precisión, precio y términos cuando se implemente checkout con ubicación. |
| Route 53 / AWS Budgets | Route 53 provee DNS; Budgets permite definir presupuestos y alertas de gasto, pero no sustituye revisar facturación y recursos activos. |

## Hosting estático frente a plataforma integrada

| Opción | Resumen |
|---|---|
| S3 + CloudFront | Más control sobre infraestructura y despliegue; requiere configurar permisos, certificados, DNS, invalidación/caché e IaC/CI. |
| Amplify Hosting | Despliegue Git y HTTPS simplificados; puede usarse solo como hosting o junto con backend Amplify. |

## Recordatorios de operación

| Tema | Recordatorio |
|---|---|
| Pruebas de carga | Hacerlas antes de producción, con escenarios realistas, métricas, límites de gasto y autorización del proveedor; no dirigir tráfico de prueba a terceros ni a sistemas productivos sin permiso. |
| Capa gratuita | Verificar términos vigentes de Free Tier, región, fechas y uso real en la cuenta; configurar Budgets y alertas. No registrar en documentación correos de cuenta, tarjetas ni credenciales. |

## Referencias oficiales

- [Amazon EC2](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/concepts.html)
- [AWS Client VPN](https://docs.aws.amazon.com/vpn/latest/clientvpn-admin/what-is.html)
- [DynamoDB Streams](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html)
- [Transactional Outbox en AWS Prescriptive Guidance](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html)
- [ALB target groups](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/load-balancer-target-groups.html)
- [Step Functions service integration patterns](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html)
- [Amplify Gen 2](https://docs.aws.amazon.com/amplify/latest/userguide/deploy-backend.html)
