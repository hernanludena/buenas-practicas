# Pagos, datos y contratos de servicio

| Nombre | Descripción breve |
|---|---|
| Ledger | Registro financiero auditable; preferir entradas inmutables y correcciones compensatorias en vez de editar el historial. |
| Confirmación de fondos | Modelarla como estado/evento explícito; no asumir que una solicitud aceptada significa fondos liquidados. |
| PUSH / AUTO_PULL | Separar quién inicia el movimiento, los estados, intentos, retornos, reintentos y confirmación de fondos. |
| Desembolso / cancelación / devolución | Tratar cada responsabilidad como flujo de negocio explícito con estados, idempotencia y compensaciones definidas. |
| PostgreSQL | Diseñar tablas, claves, constraints, transacciones e índices desde las consultas y reglas del dominio. |
| Flyway | Versionar migraciones SQL inmutables; ejecutarlas por orden contra la conexión configurada y probarlas con una base compatible. |
| jOOQ | Generar clases tipadas desde el esquema ya migrado; actualizar codegen después de cambiar el esquema. |
| Gradle | Definir tareas reproducibles para compilar, probar, migrar/generar código y empaquetar; fijar versiones y dependencias. |
| BIAN | Referencia para dominios y capacidades de servicios bancarios; no es un framework que implemente APIs por sí solo. |
| OpenAPI / Swagger UI | OpenAPI define contratos REST; Swagger UI los presenta para exploración y pruebas manuales. |
| OpenAPI Generator | Generar clientes o stubs desde un contrato; revisar el código generado y versionarlo/regenerarlo de forma reproducible. |
| OkHttp / Feign / WebClient | Clientes HTTP con modelos distintos; configurar timeouts, errores, TLS y reintentos con cuidado. No depender de un cliente obsoleto. |
| Apigee / API Gateway | Gestión de APIs, políticas, seguridad, cuotas y publicación; distinto de la lógica interna del servicio. |
| REST / GraphQL / gRPC | Elegir REST por recursos/contratos HTTP, GraphQL por consultas flexibles de clientes o gRPC por RPC tipado entre servicios. |
| BFF | Backend for Frontend adapta y agrega APIs para una experiencia cliente específica; no duplicar dominio de negocio. |
| Webhook / WebSocket | Webhook entrega eventos a un receptor HTTP; WebSocket mantiene canal bidireccional; ambos requieren auth, correlación y manejo de reconexión/reintentos. |

## Referencias

- [Flyway migrations](https://documentation.red-gate.com/flyway/flyway-concepts/migrations)
- [jOOQ code generation](https://www.jooq.org/doc/latest/manual/code-generation/)
- [OpenAPI Specification](https://spec.openapis.org/oas/latest.html)
