# Frontend, TypeScript y Node.js

Inventario breve de herramientas y criterios comentados para Delivery Loja y otros proyectos.

| Capa | Tecnología / tema | Para recordar |
|---|---|---|
| Frontend web | React | Construir interfaces por componentes; mantener componentes enfocados y separar estado de servidor, estado de interfaz y lógica de dominio. |
| Frontend web | Angular | Alternativa completa con estructura y herramientas integradas; elegir por experiencia del equipo y necesidades del producto, no por moda. |
| App móvil | Capacitor / Ionic | Permite empaquetar una app web para plataformas móviles y acceder a capacidades nativas mediante plugins; validar rendimiento y experiencia nativa requerida. |
| App móvil | React Native + Expo / Flutter / Kotlin y Swift | Alternativas para app móvil; evaluar experiencia del equipo, acceso a APIs nativas, rendimiento, mantenimiento y necesidad de dos aplicaciones o una multiplataforma. |
| Lenguaje | TypeScript | Usar tipos para hacer contratos y refactors más seguros; recordar que los tipos se eliminan en runtime y no sustituyen validación de entradas externas. |
| Backend Node | Hono / Express / NestJS | Hono es liviano y se adapta a runtimes como Lambda; Express es minimalista y conocido; NestJS ofrece una estructura más opinada. Decidir según complejidad, runtime y convenciones del equipo. |
| Node.js | Clases o funciones | Elegir una convención consistente. Clases pueden organizar servicios con estado/dependencias; funciones suelen ser simples para lógica pura y handlers. No convertir el uso de clases en regla universal. |
| API / validación | DTOs y esquemas runtime | Validar payloads en runtime (por ejemplo, con una librería de esquemas) y separar contratos HTTP del modelo interno. TypeScript por sí solo no valida JSON externo. |
| Persistencia | Drizzle ORM | ORM/consulta tipada para SQL; mantener migraciones explícitas y revisar consultas, transacciones, índices y límites de paginación. |
| Estado frontend | TanStack Query / RTK Query | Administrar datos remotos, caché, sincronización y estados de carga/error; evitar duplicar innecesariamente el estado de servidor en el store de interfaz. |
| Estado interfaz | Zustand / Redux | Mantener estado local/global de UI cuando se justifique. Redux aporta estructura y herramientas; Zustand ofrece una API ligera. |
| Formularios | React Hook Form | Gestionar estado y validación de formularios; definir mensajes útiles y separar reglas de entrada de reglas de negocio del backend. |
| Mapeo HTTP | Axios o fetch | Centralizar base URL, errores, autenticación y cancelación cuando sea útil; evitar capas redundantes que oculten el contrato HTTP. |
| UI | Tailwind CSS / shadcn/ui | Tailwind ofrece utilidades de estilo; shadcn/ui aporta componentes cuyo código se integra al proyecto. Mantener tokens y accesibilidad del sistema de diseño. |
| Autenticación | OAuth 2.0 / OIDC / JWT | Usar proveedor administrado cuando reduce riesgo operativo. No implementar gestión propia de contraseñas para el MVP sin una necesidad clara. Spring Security valida tokens en el backend Java. |
| Seguridad | Secretos y permisos | Variables/configuración segura para secretos; validar autorización en el backend en cada operación. Nunca confiar en que ocultar botones en el frontend protege datos. |
| Rendimiento | Caché y llamadas | Medir antes de optimizar; paginar listas, evitar consultas repetidas, establecer caché coherente e invalidación correcta. |
| Pruebas / diseño | Storybook y pruebas | Storybook es opcional para desarrollar/visualizar componentes aislados; priorizar pruebas del flujo crítico, accesibilidad y comportamiento real del producto. |

## Stack que dejamos como candidato

| Área | Candidato discutido |
|---|---|
| Frontend | React + TypeScript + Tailwind/shadcn; evaluar Capacitor para una primera app móvil. |
| Backend | Node.js + TypeScript + Hono; Drizzle para PostgreSQL si se elige persistencia relacional. |
| Estado y formularios | TanStack Query o RTK Query para estado remoto; Zustand si hace falta estado global de UI; React Hook Form para formularios. |

Son candidatos para una solución liviana, no una decisión irrevocable; comparar con el backend Java/Spring Boot cuando se defina el MVP.
