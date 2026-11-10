# Jakarta Validation: recordatorio

| Nombre | Descripción breve |
|---|---|
| Jakarta Validation | API estándar para declarar restricciones como @NotBlank, @Email y @Size en objetos de entrada. |
| @Valid | Activa validación estándar del objeto recibido; en Spring MVC suele usarse en el parámetro del controller. |
| @Validated | Integración de Spring que permite seleccionar grupos de validación en el punto de entrada. |
| Grupo Default | Las restricciones sin grupos explícitos pertenecen al grupo Default. |
| Grupos por operación | Usar grupos simples como OnCreate/OnUpdate cuando cambien las reglas entre operaciones. |
| Mensajes de error | Responder errores claros por campo sin filtrar datos sensibles ni detalles internos. |
| Fechas y formatos | Usar tipos adecuados como LocalDate y validar formato/rango; @NotBlank solo comprueba texto no vacío. |
| Límite de responsabilidad | Validar forma y restricciones de entrada en DTOs; reglas de negocio permanecen en dominio/casos de uso. |
| Cuándo separar DTOs | Preferir DTOs distintos si los contratos de crear/actualizar difieren mucho; evitar demasiados grupos/excepciones. |

Más detalle se agrega cuando esta práctica se implemente en un proyecto.

Referencias: [Jakarta Validation](https://jakarta.ee/specifications/bean-validation/), [Spring validation](https://docs.spring.io/spring-framework/reference/core/validation/beanvalidation.html).
