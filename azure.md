# Azure: mapa breve de servicios y conceptos

Referencia inicial para comparar opciones de Azure con las alternativas AWS del proyecto. Confirmar región, soporte, cuotas y precios antes de decidir.

| Servicio / concepto | Para recordar |
|---|---|
| Azure Functions | Compute serverless por eventos. Durable Functions agrega estado, checkpoints, timers, reintentos y coordinación de workflows. |
| Durable Functions | Orquesta procesos duraderos mediante funciones de orquestador, actividad y entidades definidas en código. Hay soporte oficial para Java; no es obligatorio describir toda la máquina de estados en JSON. Respetar las reglas de determinismo del orquestador y diseñar actividades idempotentes. |
| Azure Container Apps | Plataforma administrada para contenedores, APIs Java/Spring Boot, workers y trabajos programados o activados por eventos; opción a evaluar frente a App Service/AKS según control requerido. |
| AKS | Kubernetes administrado; útil si se necesitan sus capacidades y el equipo puede operar su complejidad. No es requisito por usar microservicios. |
| Azure Service Bus | Mensajería empresarial con colas y topics/subscriptions; evaluar para comandos/eventos con entrega confiable y desacoplamiento. |
| Event Grid | Enrutamiento de eventos para integración reactiva; diferente de una cola de trabajo persistente. |
| Azure Database for PostgreSQL | Servicio administrado de PostgreSQL; evaluar nivel, disponibilidad, respaldo, red y costos. |
| Azure Blob Storage | Almacenamiento de objetos/archivos; análogo conceptual a S3, con diferencias de servicio y configuración. |
| Microsoft Entra ID | Proveedor de identidad y acceso; soporta escenarios OIDC/OAuth 2.0. El backend valida tokens según audiencia, emisor, firma y permisos. |
| Azure Monitor / Application Insights | Métricas, logs y trazas para operación y diagnóstico; definir correlación y alertas. |
| Terraform | Infraestructura como código multi-cloud; versionar módulos y estados con control de acceso, revisión y secretos fuera del código. |

## Orquestación: comparación recordatoria

| Opción | Cuándo considerarla |
|---|---|
| Azure Durable Functions | Workflow administrado en Azure, escrito como funciones en código, especialmente serverless y procesos duraderos. Java está soportado oficialmente. |
| Temporal con Java | Orquestador/workflow durable orientado a código, portable entre entornos; evaluar despliegue, operación y costo del servicio Temporal. |
| AWS Step Functions | Workflow administrado de AWS; expresa transiciones en Amazon States Language y se integra con servicios AWS y algunas APIs externas. |

## Referencias oficiales

- [Durable Functions overview y lenguajes](https://learn.microsoft.com/azure/azure-functions/durable/durable-functions-overview?tabs=java)
- [Quickstart de Durable Functions con Java](https://learn.microsoft.com/azure/azure-functions/durable-functions/quickstart-java)
- [Java en Azure Container Apps](https://learn.microsoft.com/azure/container-apps/java-overview)
- [Azure Container Apps](https://learn.microsoft.com/azure/container-apps/overview)
