# Frontend, TypeScript y Node.js: recordatorio breve

| Nombre | Descripción breve |
|---|---|
| React / Angular | Alternativas web; elegir por estructura, experiencia del equipo y ecosistema requerido. |
| Capacitor / Ionic | Empaquetan aplicaciones web para móvil; validar plugins, rendimiento y experiencia nativa requerida. |
| React Native + Expo / Flutter / Kotlin + Swift | Opciones móviles; comparar reutilización, acceso nativo, costo de mantenimiento y requisitos de plataforma. |
| TypeScript | Tipos estáticos ayudan al desarrollo, pero no validan en runtime datos recibidos por HTTP. |
| Hono / Express / NestJS | Hono es liviano para runtimes como Lambda; Express minimalista; NestJS más opinado y estructurado. |
| Clases / funciones | Convención de diseño; clases para objetos con dependencias/estado, funciones para lógica pura; evitar convertirlo en dogma. |
| Drizzle ORM | Acceso tipado a SQL; revisar migraciones, consultas e índices. |
| React Hook Form | Maneja formularios; validar en backend aunque también se valide en el frontend. |
| TanStack Query / RTK Query | Datos del servidor, caché y estados remotos; no duplicar el estado sin necesidad. |
| Zustand / Redux | Estado compartido de interfaz; agregar cuando el estado local ya no sea suficiente. |
| Tailwind CSS / shadcn/ui | Utilidades de estilos y componentes editables dentro del proyecto; mantener accesibilidad y diseño consistente. |
| Storybook | Catálogo/desarrollo aislado de componentes; herramienta útil, pero no obligatoria para el MVP. |
| Nginx | Web server, reverse proxy, caché y balanceador configurable; sirve de proxy frente a APIs/servicios. |
| ALB vs Nginx | ALB es balanceador administrado AWS; Nginx es software que requiere configuración y operación. |
| API REST / GraphQL | REST modela recursos y endpoints; GraphQL permite pedir campos de un esquema; elegir según clientes y consultas. |
| WebSocket / Socket.IO / AppSync Events | Canales en tiempo real; WebSocket es protocolo, Socket.IO librería con protocolo propio, AppSync Events servicio administrado pub/sub. |
| OAuth 2.0 / OIDC / JWT | Authorization framework / capa de identidad / formato de token; validar tokens y permisos en backend. |
| Better Auth / Cognito | Alternativas distintas de autenticación; comparar soporte, operación, seguridad, costo e integración con el stack. |
| Postman | Colecciones y ejemplos para explorar, documentar y validar APIs; usar variables por ambiente y nunca incluir secretos compartidos. |
| BrowserStack | Pruebas en navegadores/dispositivos diversos cuando el entorno local no cubre la matriz. |
| Axios / fetch | Clientes HTTP; centralizar base URL, manejo de errores y autenticación sin crear capas innecesarias. |
| Accesibilidad / adaptable | Soportar teclado, etiquetas, contraste, mensajes legibles y tamaños móviles en los flujos principales. |

| Candidato conversado | Stack |
|---|---|
| Frontend web/móvil | React + TypeScript + Tailwind/shadcn; evaluar Capacitor para distribución móvil. |
| Backend Node | Hono + TypeScript + Drizzle; PostgreSQL si el modelo relacional y consultas lo justifican. |
| Estado/UI | TanStack Query o RTK Query para servidor; Zustand si se necesita estado global de interfaz. |

Referencias: [Nginx reverse proxy](https://nginx.org/en/docs/http/ngx_http_proxy_module.html), [Nginx load balancing](https://nginx.org/en/docs/http/load_balancing.html).
