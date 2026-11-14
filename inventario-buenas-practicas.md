# Inventario técnico para recordar

Recordatorio corto de los temas que hemos revisado. Cada fila resume qué hace o qué conviene recordar; profundizamos cuando toque implementarlo.

| Bloque | Nombre | Descripción breve |
|---|---|---|
| Java / Spring | Jersey vs Spring Boot | Jersey implementa JAX-RS; Spring Boot ofrece autoconfiguración y un ecosistema amplio para APIs y aplicaciones Java. |
| Java / Spring | Inyección por constructor | Declarar dependencias obligatorias en el constructor; Spring lo recomienda y un constructor único no necesita @Autowired. |
| Java / Spring | Varios beans para una interfaz | Spring inyecta el bean compatible; con varios candidatos, resolver con @Qualifier o marcar el predeterminado con @Primary. |
| Java / Spring | Repositorios Spring Data | Una interfaz que extiende `JpaRepository` (u otra interfaz Spring Data) recibe una implementación proxy creada por Spring Data e inyectable como bean. |
| Java / Spring | Lombok y records | Lombok reduce boilerplate en clases; records simplifican DTOs simples e inmutables con contrato visible. |
| Java / Spring | DTOs y MapStruct | Mapear explícitamente modelos API, aplicación, dominio y persistencia; exponer al frontend solo los campos requeridos. |
| Java / Spring | Jakarta Validation | Validar entradas con restricciones y @Valid/@Validated; reservar validadores de negocio para reglas de negocio. |
| Java / Spring | JPA Entity vs DTO | Entity representa persistencia; DTO representa contrato de entrada/salida. No devolver entidades JPA desde la API. |
| Java / Spring | Spring Security | Filtros procesan solicitudes y aplican autenticación/autorización; validar tokens y permisos del lado servidor. |
| Java / Spring | Spring Modulith | Ayuda a organizar y verificar límites de módulos dentro de una aplicación Spring modular. |
| Arquitectura | Hexagonal | Dominio contiene reglas y puertos; Application contiene casos de uso; adaptadores conectan entradas/salidas; infraestructura configura tecnología. |
| Arquitectura | Monolito modular | Empezar con módulos de negocio bien separados en una aplicación cuando no se justifica operar microservicios independientes. |
| Arquitectura | Microservicios | Separar cuando haya motivos de escala, despliegue, autonomía o aislamiento; cada servicio dueño de sus datos. |
| APIs | REST / OpenAPI | Diseñar contratos claros, errores consistentes y paginación; documentar endpoints con OpenAPI para humanos y herramientas. |
| APIs | Webhooks | Recibir avisos asíncronos de proveedores; validar firma, idempotencia, reintentos y eventos duplicados. |
| Seguridad | OAuth 2.0 / OIDC / JWT | OAuth 2.0 es autorización, OIDC añade autenticación, JWT es un formato; no son sinónimos. |
| Seguridad | Proveedor de identidad | Cognito, Auth0, Keycloak, Okta, Entra ID o Google Identity gestionan identidad; evitar custodiar contraseñas sin necesidad. |
| Seguridad | IAM y secretos | Aplicar mínimo privilegio; guardar claves/tokens en secret manager y nunca en el repositorio o logs. |
| Mensajería | Kafka | Plataforma de streaming/eventos durables; orden por partición y capacidad de reproducir eventos; no es requisito para cualquier Saga. |
| Mensajería | RabbitMQ | Broker con exchanges, colas, routing y acknowledgements; útil para tareas y distribución flexible de mensajes. |
| Mensajería | Kafka vs RabbitMQ | Kafka favorece streams y replay; RabbitMQ suele encajar en colas/routing de trabajo. Elegir por patrón y operación. |
| Mensajería | SQS, SNS, EventBridge | SQS es cola; SNS distribuye pub/sub; EventBridge enruta eventos y Scheduler programa ejecuciones. |
| Mensajería | Azure Service Bus / Event Grid | Service Bus maneja colas y topics; Event Grid enruta eventos. No tratarlos como equivalentes. |
| Mensajería | DLQ, ACK y reintentos | Definir confirmación de consumo, backoff, límite de reintentos, DLQ, alertas y procedimiento de recuperación. |
| Distribuidos | Idempotencia (“potencia”, término por confirmar) | Repetir un comando/evento no debe repetir su efecto; usar clave y registro persistente de procesamiento. |
| Distribuidos | Outbox | Guardar cambio de negocio y evento pendiente en una transacción local; publicar luego con reintentos. |
| Distribuidos | CDC | Capturar cambios de datos para alimentar procesos; DynamoDB Streams provee CDC de ítems, no equivale a todo Outbox. |
| Distribuidos | Event log / audit log (“logbook”, por confirmar) | Historial de hechos o auditoría; confirmar si “logbook” era audit log, event sourcing o Outbox: son conceptos distintos. |
| Distribuidos | Saga | Coordinar transacciones locales con compensaciones; orquestación centraliza el flujo, coreografía lo distribuye mediante eventos. |
| Distribuidos | Temporal / Step Functions / Durable Functions | Motores de workflow duradero; Temporal y Durable Functions permiten workflows en código, Step Functions modela estados en AWS. |
| Distribuidos | Timeout y circuit breaker | Limitar esperas y evitar llamadas repetidas a dependencias caídas; combinar con reintentos acotados e idempotencia. |
| Datos | PostgreSQL / RDS / Aurora | SQL relacional para relaciones y transacciones; RDS/Aurora administran operación con diferencias de capacidad y costo. |
| Datos | DynamoDB | NoSQL orientada a patrones de acceso definidos; diseñar claves e índices antes de modelar consultas. |
| Datos | DocumentDB | Servicio compatible con MongoDB en cierta medida; verificar compatibilidad de comandos y drivers antes de migrar. |
| Datos | PostGIS | Extensión geoespacial de PostgreSQL para consultas por ubicación, por ejemplo repartidores cercanos. |
| Datos | Redis / ElastiCache | Caché para lecturas frecuentes y datos temporales; definir expiración, invalidación y fuente de verdad. |
| Infraestructura | Nginx | Web server y reverse proxy; puede enrutar/balancear tráfico, servir estáticos y manejar caché/TLS según configuración. |
| Infraestructura | ALB vs Nginx | ALB es balanceador administrado de AWS; Nginx es software que se configura y opera como proxy/balanceador. |
| Infraestructura | Docker / ECR / ECS / EKS / Fargate | Docker empaqueta; ECR almacena imágenes; ECS/EKS orquestan; Fargate ejecuta contenedores sin administrar hosts. |
| Infraestructura | API Gateway / Lambda | API Gateway publica rutas; Lambda ejecuta código por invocación. Lambda no requiere mantener una VM, pero sí tiene límites. |
| Infraestructura | Terraform / IaC | Declarar infraestructura en código; revisar cambios, versionar módulos y proteger el state y secretos. |
| Entrega | CI/CD y liberaciones pequeñas | Automatizar build/despliegue y publicar cambios pequeños para obtener feedback funcional frecuente. |
| Frontend | React / Angular | Frameworks/plataformas distintos; escoger por equipo, estructura deseada, ecosistema y requisitos de la app. |
| Frontend | React Native / Expo / Flutter / Capacitor / nativo | Evaluar reutilización, experiencia móvil, plugins y acceso nativo antes de escoger el enfoque multiplataforma. |
| Frontend | TanStack Query / RTK Query | Administrar datos del servidor, caché y estados de carga/error; evitar duplicar ese estado en stores locales. |
| Frontend | Zustand / Redux | Estado compartido de interfaz; agregarlo cuando haga falta y mantener una fuente clara de verdad. |
| Frontend | React Hook Form / Jakarta Validation | Validar experiencia de formulario en frontend y volver a validar datos confiables en backend. |
| Frontend | Tailwind / shadcn/ui / Storybook | Estilos por utilidades, componentes personalizables y catálogo de componentes; Storybook es opcional. |
| Frontend | Accesibilidad y diseño adaptable | Usar etiquetas, teclado, contraste y diseños móviles; validar los flujos principales en dispositivos reales o emulados. |
| Node / TypeScript | Hono / Express / NestJS | Hono es liviano; Express minimalista; NestJS más estructurado. Elegir según runtime, tamaño y convenciones del equipo. |
| Node / TypeScript | TypeScript | Tipos ayudan en desarrollo, pero desaparecen en runtime; validar JSON y datos externos al recibirlos. |
| Node / TypeScript | Clases vs funciones | Mantener convención consistente; clases sirven para objetos con dependencias/estado y funciones para lógica simple/pura. |
| Node / TypeScript | Drizzle ORM | ORM tipado para SQL; mantener migraciones, transacciones e índices explícitos. |
| Node / TypeScript | Postman | Definir colecciones y ejemplos para explorar, documentar y validar contratos de APIs. |
| Operación | CloudWatch / Azure Monitor / Sentry / Datadog | Centralizar logs, métricas, trazas, errores y alertas; incluir IDs de correlación sin registrar secretos. |
| Operación | PostHog / analítica de producto | Medir uso de flujos con eventos mínimos, consentimiento y protección de datos personales. |
| Operación | Costos y presupuestos | Definir presupuestos/alertas, revisar recursos activos y validar costos por región; Free Tier tiene límites y condiciones. |
| Operación | Pruebas de carga | Hacerlas antes de producción, en ambiente autorizado, con escenarios, límites y métricas; no probar terceros sin permiso. |
| Operación | BrowserStack | Probar compatibilidad en navegadores/dispositivos cuando los entornos locales no cubran la matriz requerida. |
| Proyecto | MVP y entregas pequeñas | Aprender el ciclo de vida completo con incrementos funcionales; priorizar una solución mínima y sostenible. |
| Proyecto | Meta del piloto | Referencia anotada: piloto de 2–3 meses con 10–15 restaurantes y 8–10 repartidores; validar antes de escalar. |
| Proyecto | Aplicaciones | Alcance previsto: cliente, repartidor, comercio/restaurante y administración. |
| Proyecto | Modelo de negocio | Delivery y mandados con logística sostenible; buscar comisiones/costos competitivos sin depender de cientos de pedidos diarios. |
| Proyecto | Taxis | Mantener como etapa futura; validar interés, gremios, convenios, normativa y rentabilidad antes de desarrollar. |
| Proyecto | Mapas y pagos | Comparar cobertura, costo y soporte local; confirmar proveedor y modelo de cobro antes del checkout. |
| Proyecto | MapLibre/OSM, Mapbox y Google Maps | Comparar mapas, geocoding, rutas, precisión, cobertura de Loja, términos y costo por uso. |
| Proyecto | Stripe, PayPhone y Kushki | Confirmar disponibilidad comercial en Ecuador, requisitos, comisiones, liquidación, reembolsos y webhooks. |
| Proyecto | Correo transaccional / Resend | Evaluar entrega, reputación, límites, dominios y manejo de rebotes; no usar para spam. |
| Hosting | Vercel, Amplify, S3/CloudFront y Cloudflare Pages | Comparar builds, SSR, HTTPS, CDN, límites, costos y control del despliegue. |
| Hosting / datos | DigitalOcean, Fly.io, Railway, Render, Heroku, Neon, Supabase y Firebase | Opciones investigadas; comparar regiones, escalado, persistencia, backups, límites, costo y dependencia antes de elegir. |
| Proyecto | Ritmo de trabajo | Avanzar con features pequeños y reservar tiempo fuera del trabajo para familia y descanso. |

### Inyección de dependencias en Spring

Spring resuelve una dependencia por tipo entre los beans registrados en el contenedor. Si solo existe una implementación de una interfaz, la inyecta. Si hay varias candidatas para el mismo tipo, la inyección queda ambigua y normalmente la aplicación no inicia; Spring no busca dinámicamente una implementación en cada llamada.

Se puede seleccionar una implementación con `@Qualifier`:

```java
@Service("listMerchantsService")
class ListMerchantsService implements ListMerchantsUseCase {
    // ...
}

@RestController
class MerchantController {
    private final ListMerchantsUseCase listMerchantsUseCase;

    MerchantController(
            @Qualifier("listMerchantsService") ListMerchantsUseCase listMerchantsUseCase) {
        this.listMerchantsUseCase = listMerchantsUseCase;
    }
}
```

`@Primary` marca una implementación preferida cuando se inyecta ese tipo sin un calificador. Conviene que cada caso de uso tenga una interfaz específica (por ejemplo, `ListMerchantsUseCase`); `@Qualifier` sirve cuando varias implementaciones del mismo contrato son intencionales. La llamada del controlador se hace a la interfaz, pero el objeto concreto ya fue elegido e inyectado por Spring.

Referencia: [Spring Framework — Fine-tuning annotation-based autowiring with @Primary or @Fallback](https://docs.spring.io/spring-framework/reference/core/beans/annotation-config/autowired-primary.html).

| Bloque | Nombre | Descripción breve |
|---|---|---|
| QA / plataforma | Pruebas, cobertura y telemetría | Tests por riesgo, gates en CI y observabilidad como criterio de aceptación. |
| Kubernetes | HPA, Service, Gateway API e Istio | HPA escala Pods; Service distribuye tráfico; Gateway/mesh enrutan en bordes distintos. |
| Entrega | GitLab CI / Argo CD / Rollouts | CI valida/crea artefactos; Argo CD reconcilia Git; Rollouts ofrece canary/blue-green con métricas. |
| Kafka | Avro, Schema Registry, Connect y Debezium | Versionar contratos y capturar cambios; definir key, compatibilidad, lag, idempotencia y DLT. |
| Kotlin | Corrutinas | Suspender no equivale a bloquear menos por arte de magia; aplicar scope, cancelación y dispatcher correcto. |
| Datos/pagos | Ledger, Flyway y jOOQ | Mantener historia financiera auditable, migraciones versionadas y clases generadas desde el esquema actualizado. |
| APIs bancarias | BIAN / OpenAPI / Apigee | BIAN organiza capacidades; OpenAPI define contratos; Apigee administra políticas y publicación de APIs. |
| Desarrollo con IA | Backlog, agent rules y gates | Trabajar una HU por vez y verificar especificación/arquitectura antes de pasar de fase. |

Más detalle: [QA/escalabilidad/Kubernetes](qa-escalabilidad-kubernetes.md), [Kafka/CDC](kafka-cdc-eventos.md), [Kotlin coroutines](kotlin-coroutines.md), [Pagos/datos/APIs](pagos-datos-y-api.md), [desarrollo incremental con agentes](desarrollo-incremental-con-agentes.md), [AWS](aws.md), [Azure](azure.md), [Frontend/TypeScript/Node](frontend-typescript-node.md) y [Arquitecturas](arquitecturas.md).
