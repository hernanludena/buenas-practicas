# Kafka, RabbitMQ y CDC

| Nombre | Descripción breve |
|---|---|
| Kafka | Event streaming distribuido con topics, particiones, offsets y retención; permite varios consumer groups y replay desde offsets. |
| Orden en Kafka | Kafka garantiza orden dentro de una partición; usar una key de negocio estable para mantener relacionados juntos. |
| Consumer group / lag | Cada grupo consume independientemente; medir lag para detectar retraso y capacidad insuficiente. |
| Kafka Connect | Framework para mover datos entre Kafka y sistemas externos mediante connectors configurables. |
| Debezium / CDC | Captura cambios de bases como PostgreSQL y los publica en Kafka; modelar qué cambios son eventos de negocio. |
| Transactional Outbox | Persistir cambio y evento en la misma transacción; publicar el outbox por relay o CDC para evitar el dual-write. |
| Avro | Formato de eventos compacto y con esquema; acordar evolución compatible antes de desplegar productores/consumidores. |
| Schema Registry | Guarda/versiona esquemas y aplica políticas de compatibilidad para evitar cambios incompatibles en eventos. |
| Idempotent Consumer | Deduplicar con eventId y clave de negocio (por ejemplo, invoiceId); Kafka puede reentregar tras fallos. |
| Retry / DLT | Reintentar con límites y enviar errores no recuperables a Dead Letter Topic/Queue con alerta y recuperación definida. |
| RabbitMQ | Broker orientado a exchanges, routing y queues; ACK, redelivery y competing consumers son parte de su operación. |
| Kafka vs RabbitMQ | Kafka encaja en streams durables/replay; RabbitMQ en colas y routing de mensajes de trabajo. Elegir por semántica y operación. |
| SQS / SNS / EventBridge | Servicios AWS administrados de cola, pub/sub y event bus; pueden evitar operar brokers cuando cumplen el caso. |
| Amazon MSK | Kafka administrado por AWS; aprender operación Kafka sin mantener todos los brokers. |
| Confluent Cloud | Kafka gestionado con ecosistema de Schema Registry/connectors; verificar precios y funcionalidades por plan. |
| WarpStream | Servicio compatible con protocolo Kafka que usa almacenamiento tipo S3; compatibilidad de protocolo no implica la misma arquitectura interna. |
| Redpanda / Aiven / Azure Event Hubs | Alternativas compatibles o gestionadas; confirmar diferencias de protocolo, límites, semántica y costos antes de migrar. |
| Laboratorio sugerido | Aprender Kafka local primero; luego probar MSK; explorar Confluent/Schema Registry y WarpStream como opciones separadas. |

## Referencias

- [Apache Kafka](https://kafka.apache.org/documentation/)
- [RabbitMQ queues](https://www.rabbitmq.com/docs/queues)
- [RabbitMQ acknowledgements](https://www.rabbitmq.com/docs/confirms)
- [AWS Transactional Outbox](https://docs.aws.amazon.com/prescriptive-guidance/latest/cloud-design-patterns/transactional-outbox.html)
