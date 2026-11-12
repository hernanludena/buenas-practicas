# Flyway y PostgreSQL

| Tema | Descripción |
|---|---|
| Flyway | Crea y actualiza estructuras con migraciones SQL versionadas. Requiere dependencia Maven y `spring.flyway.enabled=true` en `application.properties`; al iniciar la aplicación ejecuta las pendientes. |
| Esquemas y tablas | Un esquema agrupa tablas; `esquema.tabla` identifica una tabla. Ejemplo: `CREATE SCHEMA merchants; CREATE TABLE merchants.merchants (id uuid PRIMARY KEY);` |
| Bloqueo de filas | `SELECT` normal no bloquea filas para escritura. Añade `FOR UPDATE` al final para bloquear las seleccionadas hasta terminar la transacción: `SELECT * FROM orders.orders WHERE id = :id FOR UPDATE;`. `SKIP LOCKED` omite filas bloqueadas por otros workers. |

Fuentes: [Flyway en Spring Boot](https://docs.spring.io/spring-boot/how-to/data-initialization.html#howto.data-initialization.migration-tool.flyway) · [Bloqueos en PostgreSQL](https://www.postgresql.org/docs/current/explicit-locking.html#LOCKING-ROWS).
