# Arquitecturas revisadas

Registro breve de siete configuraciones discutidas. Son alternativas y etapas de diseño; no representan siete decisiones aprobadas para producción. Las opciones llamadas A-D conservan las etiquetas usadas al compararlas; para las demás se resume la conversación disponible.

| # | Nombre de referencia | Componentes principales | Idea / estado |
|---|---|---|---|
| 1 | AWS HTTP + WebSocket separado | API Gateway HTTP y WebSocket; Lambda para REST y otra Lambda para WebSocket; DynamoDB para conexiones | Separar requests y conexiones en tiempo real. Boceto inicial; revisar autenticación, entrega y ciclo de vida de conexiones. |
| 2 | AWS Lambda modular con worker y SQL Outbox | API Lambda Node/TypeScript/Hono; worker Lambda; Drizzle; base SQL; EventBridge Scheduler; outbox | Mantener API y procesamiento asíncrono desacoplados; scheduler despierta worker para procesar pendientes. Es una alternativa de bajo costo que requiere revisar persistencia, polling, duplicados y métricas. |
| 3 | Arquitectura A: Aurora | Aurora Serverless v2 relacional + Outbox + EventBridge + worker | Prioriza transacciones y relaciones SQL con publicación asíncrona. Comparar costo mínimo real, pausado/escalado disponible y carga del MVP. |
| 4 | Arquitectura B: referencia relacional de Kevin/Meniuz | Backend y persistencia relacional como referencia; detalles de componentes por confirmar | Se mencionó como diseño relacional de referencia, pero no quedó documentado con suficiente detalle para tratarlo como una arquitectura especificada. Validar tecnologías con la fuente antes de replicarla. |
| 5 | Arquitectura C: DynamoDB y eventos | API Gateway HTTP → Lambda API → DynamoDB (orden, eventos e idempotencia) → DynamoDB Streams → Lambda worker → AppSync Events | Actualizar cliente en tiempo real. Streams captura cambios y puede activar procesamiento; no equivale por sí solo a Outbox relacional. Definir orden, deduplicación, DLQ y reintentos. |
| 6 | Arquitectura D: PostgreSQL económico | API Java/Spring Boot o backend modular; RDS PostgreSQL pequeño; EventBridge Scheduler; worker | Alternativa relacional de costo mínimo a validar. El tamaño t3.micro fue una referencia de análisis, no garantía de capa gratuita o capacidad suficiente. |
| 7 | Arquitectura E: Azure modular Java | Aplicación Java modular por dominios (Identity/Auth, Users, Orders, Deliveries y otros); PostgreSQL; orquestación Durable Functions o Temporal | Mantener dominios y límites claros. Durable Functions permite orquestación en código y soporta Java; Temporal es alternativa. Hosting Java en contenedores puede evaluarse con Azure Container Apps; definir mensajería y topología al concretar el flujo. |

## Variantes y decisiones de despliegue relacionadas

| Variante | Componentes / criterio |
|---|---|
| Java modular en AWS | Spring Boot + PostgreSQL + Docker; evaluar ECS con Fargate, ECS sobre EC2, EKS o EC2 según costo, control operativo y escala. ECS no obliga a usar Fargate: también puede usar capacidad EC2. |
| Hosting de frontend | S3 + CloudFront da control; Amplify Hosting simplifica integración con Git. Amplify Gen 2 puede sumar backend TypeScript, pero no es requisito para usar Amplify Hosting. |
| Orquestación o coreografía | Orquestar con Step Functions, Durable Functions o Temporal cuando se requiere estado y visibilidad central del flujo; coreografiar con eventos cuando los servicios reaccionan a hechos de negocio. Evitar una equivalencia simplista: Kafka/EventBridge no son orquestadores. |
| Serverless vs contenedores | Lambda y contenedores resuelven modelos distintos; comparar duración, uso constante, cold starts, recursos, escalado, costos y carga operativa. |
| Monolito modular primero | Mantener módulos y límites de dominio dentro de una sola aplicación cuando todavía no hacen falta despliegues y bases independientes; extraer servicios cuando existan necesidades concretas. |

## Regla de selección para Delivery Loja

| Etapa | Recordatorio |
|---|---|
| MVP | Priorizar el flujo feliz de restaurantes, carrito y orden con la menor cantidad de servicios operativos posible. Usar transacción local cuando una sola aplicación/base resuelve el caso. |
| Crecimiento | Separar worker, eventos, tiempo real o servicios cuando aparezcan requisitos reales; instrumentar costos y disponibilidad. |
| Producción | Antes de carga real, revisar seguridad, respaldos, recuperación, límites, alertas, pagos, mapas, pruebas de carga y costo total. No desplegar toda alternativa a la vez. |
