# Arquitecturas revisadas

Siete configuraciones recogidas de nuestras conversaciones. Son alternativas históricas/de diseño; no significa que todas estén aprobadas ni que deban desplegarse simultáneamente.

| # | Configuración | Componentes | Recordatorio / estado |
|---|---|---|---|
| 1 | AWS HTTP + WebSocket | API Gateway HTTP/WS, Lambda REST, Lambda WS, DynamoDB conexiones | Separar API y conexiones en tiempo real; validar autenticación, escala y reconexión. |
| 2 | AWS Lambda modular + worker | Node/TypeScript, Hono, Lambda API/worker, Drizzle, SQL Outbox, EventBridge Scheduler | API atiende requests; worker procesa pendientes. Outbox y consumidor requieren reintentos, idempotencia, alertas y recuperación. |
| 3 | Arquitectura A: Aurora | Aurora Serverless v2, Outbox, EventBridge, worker | SQL con flujo asíncrono; revisar costo mínimo, carga y estrategia de publicación. |
| 4 | Arquitectura B: referencia relacional | Backend relacional atribuido a Kevin/Meniuz; detalles sin verificar | Referencia pendiente de confirmar con su fuente; no se documentó suficiente para copiar el diseño. |
| 5 | Arquitectura C: DynamoDB real time | API Gateway HTTP → Lambda API → DynamoDB (orden/eventos/idempotencia) → Streams → worker Lambda → AppSync Events | CDC de ítems puede activar publicación; Streams no es una cola durable ilimitada ni reemplazo automático de Outbox SQL. |
| 6 | Arquitectura D: RDS económico | PostgreSQL RDS pequeño, API/monolito, EventBridge Scheduler, worker | Tamaño pequeño fue referencia, no garantía de Free Tier ni de capacidad; medir costo y rendimiento. |
| 7 | Arquitectura E: Azure Java modular | Identity/Auth, Users, Catalog, Orders, Deliveries; PostgreSQL; Durable Functions o Temporal | Modularizar primero; Durable Functions soporta Java y workflow en código; Temporal es alternativa. Definir hosting y mensajería al concretar requisitos. |

| Variante de despliegue | Recordatorio |
|---|---|
| Java Spring Boot en AWS | Docker y PostgreSQL; ECS/Fargate, ECS/EC2, EKS o EC2 según costo y operación. ECS no exige Fargate. |
| Java Spring Boot en Azure | Azure Container Apps para contenedores y jobs; AKS si se necesita Kubernetes y se puede operar. |
| Frontend AWS | S3 + CloudFront para control; Amplify Hosting para reducir configuración. Gen 2 backend TypeScript es opcional. |
| Orquestación | Step Functions, Durable Functions o Temporal mantienen estado del workflow; Kafka/EventBridge son mensajería/eventos, no motores de Saga. |
| Coreografía | Servicios reaccionan a eventos; usar contratos versionados, outbox/CDC cuando aplique, deduplicación, DLQ y trazabilidad. |
| Scheduler del Outbox | El EventBridge Scheduler anotado hoy dispara el barrido de Outbox; cancelaciones y pagos pendientes necesitan reglas/handlers adicionales. |
| Inicio de Delivery Loja | Happy path de restaurantes, menú, carrito y orden; conservar transacción local mientras un backend modular lo resuelva. |
| Evolución | Separar servicios cuando lo justifiquen escala, equipos o despliegues independientes; evitar complejidad antes de validarla. |

## Fuentes oficiales y primarias

- [AWS Step Functions integration patterns](https://docs.aws.amazon.com/step-functions/latest/dg/connect-to-resource.html)
- [DynamoDB Streams](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/Streams.html)
- [Azure Durable Functions](https://learn.microsoft.com/azure/azure-functions/durable/durable-functions-overview?tabs=java)
