# Inventario de buenas prácticas

Inventario condensado de conceptos de Java, Spring Boot y patrones de arquitectura para tenerlos presentes y profundizarlos al implementarlos.

| Bloque | Práctica o concepto | Descripción breve |
|---|---|---|
| Java y Spring Boot | Lombok y records para DTOs | Lombok reduce código repetitivo en clases que lo necesitan. Para DTOs simples e inmutables, considerar Java `record`, que hace explícitos sus componentes y evita agregar anotaciones solo para generar accesores y métodos comunes. Elegir según requisitos de mutabilidad, herencia y serialización. |
| Java y Spring Boot | Jakarta Validation en DTOs | Declarar restricciones de entrada con anotaciones como `@NotBlank`, `@Email` y `@Size`; activar la validación en Spring con `@Valid` o `@Validated`. Usar grupos si las reglas varían por operación. |
| Java y Spring Boot | MapStruct para mapeos | Generar mappers en compilación para convertir entre modelos de API, aplicación, dominio y persistencia. Definir contratos de entrada y salida que expongan solo los datos necesarios y eviten devolver entidades o detalles internos al frontend. |
| Java y Spring Boot | Inyección por constructor | Inyectar las dependencias obligatorias mediante el constructor para hacerlas explícitas y permitir componentes con referencias finales. Spring Boot admite la inyección sin `@Autowired` cuando hay un solo constructor. |
| Java y Spring Boot | Arquitectura hexagonal por dominios | Organizar el microservicio modular por dominios de negocio. Dominio contiene reglas y puertos; Application contiene casos de uso; adaptadores conectan entradas y salidas. Controllers HTTP son adaptadores de entrada; persistencia y clientes externos son adaptadores de salida, normalmente ubicados en infraestructura. Mantener los detalles de frameworks fuera del dominio. |
| Patrones distribuidos | Idempotencia (término por confirmar) | Permitir que una solicitud o evento se procese más de una vez sin duplicar el efecto de negocio, usando claves de operación/evento y registros persistentes. “Ir en potencia” podría referirse a idempotencia; confirmar el término antes de profundizar. |
| Patrones distribuidos | Registro de eventos / Outbox (“logbook” por confirmar) | Registrar eventos relacionados con cambios de negocio. Si se busca guardar el cambio y el evento pendiente en una sola transacción, revisar Transactional Outbox. “Logbook” también podría significar auditoría o event log; confirmar el concepto porque son mecanismos distintos. |
| Patrones distribuidos | Saga: orquestación y coreografía | Coordinar transacciones locales entre servicios y definir compensaciones ante fallos. Orquestación usa un workflow coordinador (por ejemplo, Temporal con Java o AWS Step Functions); coreografía distribuye el flujo entre servicios que reaccionan y publican eventos. |
| Patrones distribuidos | Transactional Outbox | Persistir el evento pendiente junto con el cambio de negocio en la misma transacción local; un publicador lo envía después al broker con reintentos para reducir el riesgo de perder eventos. |
| Patrones distribuidos | Compensación en procesos distribuidos | Definir acciones de negocio que contrarresten pasos ya completados cuando una Saga falla; no equivale a un rollback global y también requiere idempotencia y manejo de errores. |

## Material relacionado

- [Jakarta Bean Validation: restricciones y grupos](jakarta-validation-grupos.md) — guía existente con ejemplos de grupos de validación.
