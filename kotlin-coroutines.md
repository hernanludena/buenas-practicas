# Kotlin: corrutinas

| Nombre | Descripción breve |
|---|---|
| Coroutine | Cómputo suspendible que permite concurrencia con código secuencial; no equivale a un thread dedicado. |
| suspend | Permite suspender y reanudar una función; no vuelve no bloqueantes automáticamente llamadas JDBC, I/O bloqueante ni CPU intensiva. |
| CoroutineScope | Define ciclo de vida y relación padre-hijo; preferir scopes estructurados sobre GlobalScope. |
| launch | Inicia trabajo concurrente sin resultado; controlar excepciones y cancelación del hijo. |
| async / await | Inicia trabajo que entrega resultado; usarlo cuando exista concurrencia útil y esperar el resultado explícitamente. |
| withContext | Cambia contexto/dispatcher y devuelve resultado; usar Dispatchers.IO para I/O bloqueante y Default para CPU, según la librería. |
| Cancelación | Propagar cancelación y respetar CancellationException; no ocultarla en un catch genérico. |
| runBlocking | Bloquea el thread llamador; reservar para bordes de aplicación o pruebas, no como puente habitual en un servidor. |
| Spring y JDBC | Añadir corrutinas no convierte Spring MVC/JDBC en I/O no bloqueante; verificar soporte del stack de persistencia y runtime. |
| Estado del Playground | El repo revisado usa Kotlin con Spring/Temporal, pero la búsqueda no encontró uso de kotlinx.coroutines; tratarlo como tema para estudiar, no como parte ya implementada. |

Referencia: [Kotlin Coroutines Basics](https://kotlinlang.org/docs/coroutines-basics.html) y [Structured Concurrency](https://kotlinlang.org/docs/coroutines-and-channels.html).
