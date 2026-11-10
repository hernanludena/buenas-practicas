# Jakarta Bean Validation: restricciones y grupos

## Idea principal

Jakarta Bean Validation (antes Java Bean Validation) define una API estándar para declarar restricciones sobre objetos Java y ejecutarlas en puntos concretos de una aplicación. Anotaciones como `@NotBlank`, `@Email` y `@Size` son restricciones; el proveedor de validación las evalúa cuando se solicita la validación. Hibernate Validator es un proveedor habitual, mientras que Spring puede integrar la validación en controladores y otros componentes.

## ¿Qué es un grupo de validación?

Un grupo permite seleccionar qué restricciones se evalúan en una operación o contexto. Cada restricción pertenece por defecto al grupo `jakarta.validation.groups.Default`, salvo que se le asigne otro mediante `groups`.

Jakarta Validation establece que los grupos se identifican mediante tipos Java (`Class<?>`). La forma convencional de declarar un grupo propio es una interfaz vacía:

```java
public interface CreatePatientValidationGroup {
}
```

La interfaz no contiene lógica ni implementa un validador. Su clase (`CreatePatientValidationGroup.class`) funciona como identificador del grupo. El nombre, propósito y cantidad de estos grupos son decisiones del proyecto; el mecanismo de grupos tipados y su uso en las restricciones pertenecen a Jakarta Validation.

## Declarar restricciones por grupo

```java
public class PatientRequestDTO {
    @NotBlank
    private String name;

    @NotBlank(groups = CreatePatientValidationGroup.class,
              message = "Registered date is required")
    private String registeredDate;
}
```

- `name` no especifica `groups`; por eso pertenece a `Default`.
- `registeredDate` solo pertenece a `CreatePatientValidationGroup`.
- Si se omite `groups`, no se agrega automáticamente la restricción a todos los grupos: queda en `Default`.

## Elegir los grupos al validar

Con Spring MVC se puede indicar qué grupos ejecutar mediante `@Validated` en el parámetro del cuerpo:

```java
@PostMapping("/patients")
public PatientResponseDTO create(
        @Validated({Default.class, CreatePatientValidationGroup.class})
        @RequestBody PatientRequestDTO request) {
    // ...
}

@PutMapping("/patients/{id}")
public PatientResponseDTO update(
        @Validated(Default.class)
        @RequestBody PatientRequestDTO request) {
    // ...
}
```

En el `POST`, se evalúan las restricciones de ambos grupos: las comunes y las específicas de creación. En el `PUT`, solo se evalúa `Default`; la restricción de `registeredDate` no se ejecuta. La misma selección puede hacerse directamente con Jakarta Validation usando `Validator.validate(objeto, grupos...)`.

## Aplicación al proyecto de pacientes

En `PatientRequestDTO`:

- `name`: `@NotBlank` y `@Size(max = 100)`, grupo `Default`.
- `email`: `@NotBlank` y `@Email`, grupo `Default`.
- `address` y `dateOfBirth`: `@NotBlank`, grupo `Default`.
- `registeredDate`: `@NotBlank` en `CreatePatientValidationGroup`.

Por eso el controlador combina `Default` con `CreatePatientValidationGroup` para `POST /patients`, y usa solo `Default` para `PUT /patients/{id}`. Esta selección de grupos no modifica los campos recibidos ni hace que el DTO sea parcial: en el ejemplo, los campos comunes siguen siendo obligatorios también al actualizar.

## Buenas prácticas

1. **Usar grupos cuando las reglas del mismo objeto realmente cambian por operación.** Por ejemplo, requerir un campo al crear y dejarlo opcional al actualizar.
2. **Nombrar los grupos por contexto de uso**, como `OnCreate` y `OnUpdate`, y mantenerlos simples. Evitar crear un grupo por cada campo o combinaciones difíciles de entender.
3. **Hacer explícita la selección de grupos** en cada punto de validación. Revisar qué ocurre con `Default`: puede incluirse explícitamente junto a otros grupos cuando se quieren ejecutar ambos.
4. **No confundir grupos con validadores personalizados.** Un grupo clasifica restricciones existentes; una restricción personalizada requiere su propia anotación y una implementación `ConstraintValidator`.
5. **Elegir tipos que permitan validar el formato.** `@NotBlank` aplicado a un `String` solo exige texto no vacío. No valida que una fecha sea correcta. Para fechas, preferir `LocalDate` y restricciones compatibles, o validar el formato de forma explícita.
6. **Considerar DTO separados si los contratos son sustancialmente distintos.** Grupos son convenientes para variaciones acotadas; varios grupos y muchas excepciones pueden volver el DTO confuso.
7. **Recordar la integración de Spring.** `@Validated` es la anotación de Spring que permite indicar grupos en este punto de entrada; `@Valid` también dispara validación, pero no permite especificar grupos en el parámetro de la misma manera.

## Ejemplo mínimo independiente

```java
public interface OnCreate {}

public class UserRequest {
    @NotBlank
    private String name; // Default

    @NotBlank(groups = OnCreate.class)
    private String externalId; // solo OnCreate
}
```

Validar `new UserRequest()` con `Default.class` exige `name`, pero no `externalId`. Validarlo con `Default.class` y `OnCreate.class` exige ambos.

## Referencias oficiales

- [Jakarta Bean Validation 3.0, especificación (secciones de grupos y restricciones)](https://jakarta.ee/specifications/bean-validation/3.0/jakarta-bean-validation-spec-3.0.html)
- [Jakarta Validation, página de especificaciones](https://jakarta.ee/specifications/bean-validation/)
- [Spring Framework: validación de argumentos de métodos](https://docs.spring.io/spring-framework/reference/core/validation/beanvalidation.html)

