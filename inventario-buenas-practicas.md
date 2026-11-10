# Inventario general de buenas prácticas

Lista condensada para mantener presentes los temas que hemos revisado. Las guías por tecnología contienen el mapa de servicios y arquitecturas.

| Bloque | Tema | Recordatorio |
|---|---|---|
| Java / Spring Boot | Lombok y records | Lombok reduce boilerplate en clases que lo necesitan. Para DTOs simples e inmutables, considerar records por su contrato explícito y menor código generado; elegir según mutabilidad, herencia y necesidades del framework. |
| Java / Spring Boot | Jakarta Validation | Validar la entrada en el borde HTTP con restricciones estándar y activar con @Valid o @Validated. Usar grupos solo cuando las reglas cambien según la operación. |
| Java / Spring Boot | MapStruct | Generar mapeos explícitos entre contratos API, aplicación, dominio y persistencia; responder solo los campos requeridos y no exponer entidades ni datos internos. |
| Java / Spring Boot | Inyección por constructor | Declarar dependencias obligatorias en el constructor; facilita componentes válidos, referencias finales y pruebas. |
| Arquitectura | Hexagonal por dominios | Separar por dominios de negocio; Application aloja casos de uso, Domain reglas y puertos, adapters traducen entradas/salidas, Infrastructure configura tecnologías concretas. Controllers son adaptadores de entrada; JPA y clientes externos, de salida. |
| APIs / seguridad | OAuth 2.0, OpenID Connect y JWT | OAuth 2.0 es un marco de autorización; OIDC añade autenticación e identidad; JWT es un formato de token. Un proveedor de identidad emite tokens y el backend valida firma, emisor, audiencia y vigencia. |
| Sistemas distribuidos | Idempotencia (término por confirmar) | Reintentar una solicitud o evento no debe duplicar el efecto; usar identificadores idempotentes y estado persistente. “Ir en potencia” podría haber sido idempotencia. |
| Sistemas distribuidos | Outbox / registro de eventos (“logbook” por confirmar) | Outbox persiste el evento pendiente junto con el cambio local y lo publica después. No equivale a auditoría ni a event sourcing; confirmar cuál era el concepto llamado “logbook”. |
| Sistemas distribuidos | Saga | Coordinar transacciones locales con orquestación o coreografía y definir compensaciones. Aplicar cuando una operación cruza servicios con persistencia independiente. |
| Sistemas distribuidos | Mensajería y reintentos | SQS/Service Bus son colas; SNS/EventBridge/Event Grid cubren publicación y enrutamiento con distintos modelos. Diseñar consumidores idempotentes, DLQ, backoff, alertas y recuperación. |
| Operación | Observabilidad y costos | Medir logs, métricas, trazas, errores, latencia y gasto; configurar presupuestos y alertas. Probar carga antes de producción en un ambiente autorizado y con límites definidos. |
| Delivery Loja | Aprender por incrementos sostenibles | Construir entregas pequeñas y funcionales; priorizar un MVP simple y sostenible, aprender el ciclo de vida completo y reservar tiempo de descanso y familia. |

Más detalle: [AWS](aws.md), [Azure](azure.md), [Frontend/TypeScript/Node](frontend-typescript-node.md) y [Arquitecturas](arquitecturas.md).
