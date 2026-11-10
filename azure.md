# Azure: recordatorio de servicios

| Nombre | Descripción breve |
|---|---|
| Azure Functions | Funciones serverless activadas por eventos; revisar runtime, límites, plan y lenguaje soportado. |
| Durable Functions | Orquestación duradera en código con estado, timers, retries y recuperación; Java está soportado oficialmente. |
| Azure Container Apps | Plataforma administrada para APIs/containers Java, workers y jobs; opción a evaluar para Spring Boot. |
| AKS | Kubernetes administrado; adoptarlo si Kubernetes y su operación resuelven necesidades concretas. |
| Azure Service Bus | Colas y topics/subscriptions para mensajería empresarial desacoplada. |
| Event Grid | Enrutamiento de eventos; no es una cola de trabajo equivalente a Service Bus. |
| Azure Database for PostgreSQL | PostgreSQL administrado; evaluar tamaño, backups, red, disponibilidad y costo. |
| Blob Storage | Almacenamiento de objetos; equivalente conceptual a S3, con configuración y capacidades propias. |
| Microsoft Entra ID | Identidad y acceso; integra OAuth 2.0/OIDC para autenticación/autorización. |
| Azure Monitor / Application Insights | Logs, métricas, trazas y alertas de aplicaciones e infraestructura. |
| Terraform | IaC multi-cloud; mantener state protegido y revisar cambios antes de aplicar. |
| Durable Functions vs Step Functions | Durable Functions escribe el orquestador en código; Step Functions configura un workflow de estados administrado en AWS. |
| Temporal con Java | Alternativa de workflows duraderos en código, portable según dónde se despliegue y opere Temporal. |

Referencias: [Durable Functions y Java](https://learn.microsoft.com/azure/azure-functions/durable/durable-functions-overview?tabs=java), [Java Durable Functions quickstart](https://learn.microsoft.com/azure/azure-functions/durable-functions/quickstart-java), [Java en Container Apps](https://learn.microsoft.com/azure/container-apps/java-overview).
