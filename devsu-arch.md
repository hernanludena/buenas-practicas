# Devsu — 88 preguntas técnicas con respuestas y explicaciones

Cuestionario en español para estudiar y preparar evaluaciones técnicas de Devsu.

Cada pregunta incluye el enunciado, todas las opciones, la respuesta correcta y una explicación técnica de por qué es correcta. Se conserva el contenido de las preguntas y opciones que compartiste, sin agregar alternativas.

## DevOps — Preguntas 1 a 9

### 01 / 88 · Balanceadores de carga

**Pregunta:** Al trabajar con balanceadores de carga, se pueden usar dos de las siete capas de aplicación para balancear. Estas capas son:

- **A.** L6, L4
- **B.** L6, L3
- **C.** L7, L3
- **D.** L7, L4
- **E.** L4, L3

**Respuesta correcta:** D. L7, L4

**Explicación:** Los balanceadores de carga funcionan principalmente en dos capas del modelo OSI. La capa 4 (transporte) distribuye tráfico utilizando TCP/UDP, direcciones IP y puertos. La capa 7 (aplicación) puede analizar solicitudes HTTP, URLs, headers y cookies para decidir a qué servidor enviarlas.

El modelo OSI divide la comunicación de redes en 7 capas:

7. Aplicación: HTTP, HTTPS, DNS, SMTP.
6. Presentación: Cifrado, compresión, formato de datos.
5. Sesión: Establece, mantiene y cierra sesiones.
4. Transporte: TCP, UDP, puertos.
3. Red: IP, routers, enrutamiento.
2. Enlace de datos: MAC, Ethernet, switches.
1. Física: Cables, fibra óptica, señales.



### 02 / 88 · Máquinas virtuales y contenedores

**Pregunta:** ¿En cuál de estos escenarios se prefiere una máquina virtual sobre los contenedores?

- **A.** Alojar microservicios
- **B.** Ejecutar aplicaciones compartimentadas
- **C.** Permitir un CI/CD más rápido de una aplicación modular
- **D.** Alojar aplicaciones monolíticas

**Respuesta correcta:** D. Alojar aplicaciones monolíticas

**Explicación:** Las máquinas virtuales pueden ser más convenientes para aplicaciones monolíticas tradicionales, especialmente cuando dependen de un sistema operativo completo o configuraciones heredadas. Los contenedores suelen ser más ligeros y prácticos para microservicios y despliegues frecuentes. Sin embargo, un monolito también puede ejecutarse en contenedores.

### 03 / 88 · Disponibilidad del servidor

**Pregunta:** El tiempo de actividad del servidor es una métrica esencial para los servicios de alojamiento. ¿Qué cifras son buenas y cuáles son preocupantes?

- **A.** 100 % de disponibilidad es un objetivo saludable; 98,9 % requiere ajustes
- **B.** 100 % de disponibilidad es un objetivo saludable; 99,9 % requiere ajustes
- **C.** 99,99999 % es un objetivo saludable; 99,8 % requiere ajustes
- **D.** 90,9 % es un objetivo saludable; 98,9 % requiere ajustes
- **E.** 99,9 % es un objetivo saludable; 98,9 % requiere ajustes

**Respuesta correcta:** E. 99,9 % es un objetivo saludable; 98,9 % requiere ajustes

**Explicación:** Una disponibilidad del 99,9 % equivale aproximadamente a 43 minutos de inactividad al mes. En cambio, 98,9 % representa casi ocho horas de inactividad. Una diferencia aparentemente pequeña puede causar impactos importantes en sistemas productivos. El objetivo específico debe establecerse según los SLA y SLO del negocio.

### 04 / 88 · Predicción de carga

**Pregunta:** ¿Cuál de los siguientes es un factor relevante para predecir la carga del servidor en producción?

- **A.** Hora del día
- **B.** Actualizaciones del proveedor de alojamiento
- **C.** Registros de fallos del servidor
- **D.** Tendencias de búsquedas en Google
- **E.** Registros de cambios de desarrollo

**Respuesta correcta:** A. Hora del día

**Explicación:** El tráfico de aplicaciones normalmente presenta patrones horarios. Por ejemplo, una plataforma bancaria puede recibir más solicitudes durante el horario laboral. Analizar estos patrones permite configurar el escalado automático y anticipar necesidades de infraestructura.

### 05 / 88 · Persistencia de sesión

**Pregunta:** Al balancear carga, ¿cómo se llama la conexión de un mismo usuario al mismo servidor durante toda su visita?

- **A.** Persistencia de sesión / sticky session
- **B.** Inicio de sesión
- **C.** Cookies
- **D.** Protocolo de enlace
- **E.** Latencia

**Respuesta correcta:** A. Persistencia de sesión

**Explicación:** La persistencia de sesión, también llamada sticky session o afinidad de sesión, permite mantener las solicitudes de un usuario dirigidas hacia el mismo servidor. Puede implementarse mediante cookies o configuraciones del balanceador. Resulta útil cuando la aplicación mantiene información de sesión localmente.
Generalmente, es preferible diseñar servicios stateless (sin estado de sesión local).
AWS Application Load Balancer admite Sticky Sessions mediante cookies y permite configurar su duración.

Una Sticky Session (sesión persistente o afinidad de sesión) es una técnica de balanceo de carga (Load Balancing) que permite que las solicitudes de un mismo usuario se dirijan siempre al mismo servidor durante un período determinado.

### 06 / 88 · SSL/TLS

**Pregunta:** La capa de sockets seguros (SSL) tiene dos modos principales:

- **A.** 1. conexión redundante; 2. marcación rápida
- **B.** 1. TLS Pass-through (sin descifrar); 2. TLS Termination (descifrado en el balanceador)
- **C.** 1. alto rendimiento; 2. alto procesamiento
- **D.** 1. callejón sin salida; 2. camino abierto

**Respuesta correcta:** B. 1. paso directo; 2. terminación

**Explicación:** En SSL/TLS pass-through, el balanceador reenvía la conexión cifrada hasta el servidor backend, donde se descifra. En SSL/TLS termination, el balanceador descifra el tráfico y puede inspeccionar las solicitudes HTTP. Actualmente se utiliza TLS, sucesor de SSL.

AWS confirma que un NLB con listener TCP en el puerto 443 permite TLS Pass-through, mientras que un ALB con listener HTTPS realiza TLS Termination

1. ALB — Application Load Balancer
Trabaja en la capa 7 (Aplicación) del modelo OSI.
- Maneja tráfico HTTP y HTTPS.
- Puede inspeccionar URLs, headers y cookies.
- Permite enrutar solicitudes según la ruta.
- Soporta Sticky Sessions.
- Puede realizar TLS Termination.
- Ideal para APIs REST y microservicios Spring Boot.

2. NLB — Network Load Balancer
Trabaja en la capa 4 (Transporte) del modelo OSI.
- Maneja conexiones TCP, UDP y otros protocolos compatibles.
- Ofrece alto rendimiento y baja latencia.
- Permite direcciones IP estáticas.
- Puede realizar TLS Pass-through o TLS Termination, según su listener.
- Ideal para sistemas que necesitan balancear conexiones a nivel de red.

### 07 / 88 · Git

**Pregunta:** Selecciona las ventajas y desventajas correctas de usar Git para el control de versiones:

- **A.** Ventajas: Git tiene una codificación robusta para impedir el espionaje del código; administra automáticamente commits y ramas; ofrece herramientas de asignación de tareas. Desventajas: puede ser lento con commits grandes y la consola no siempre es intuitiva.

- **B.** Ventajas: Git permite operaciones complejas de ramas, cambiar el historial más allá del último commit y administrar código fuente. [El final de la alternativa no es visible en la captura.]

- **C.** Ventajas: restringe a cada desarrollador a una rama, protege el historial anterior y busca commits sospechosos. Desventajas: requiere mucha intervención de DevOps y obliga a descartar todo el trabajo posterior al punto de restauración.

- **D.** Ventajas: es fácil de entender, el historial siempre avanza y evita múltiples cabezas al hacer push. Desventajas: requiere comandos como rebase y puede resultar insuficiente en proyectos grandes.

**Respuesta correcta:** B. Ventajas de Git: branching complejo, modificación del historial y control del código fuente

**Explicación:** Git permite gestionar ramas, fusionar cambios y modificar el historial mediante operaciones como `rebase`, `reset` y `cherry-pick`. Además, facilita el trabajo colaborativo y el control de versiones. Git no incorpora por sí mismo un sistema completo de gestión de tareas ni cifra automáticamente todo el código.

**Nota:** la opción B está incompleta en el material original.

### 08 / 88 · Punto único de fallo

**Pregunta:** Los balanceadores de carga permiten alojar la aplicación en varios servidores, aumentando la redundancia, pero...

- **A.** El tiempo y sobrecosto de procesamiento de implementarlos superan sus beneficios
- **B.** También se deben configurar versiones de respaldo de las aplicaciones
- **C.** Solo pueden dirigir tráfico dentro de un único clúster
- **D.** Un único balanceador puede convertirse en un punto único de fallo

**Respuesta correcta:** D. Un único balanceador puede convertirse en un punto único de fallo

**Explicación:** Aunque existan múltiples servidores backend, si todo el tráfico pasa por un único balanceador y este falla, la aplicación puede quedar inaccesible. Esto se conoce como Single Point of Failure (SPOF). Para evitarlo se utilizan balanceadores redundantes, alta disponibilidad y mecanismos de failover.

Usar Arquitectura con alta disponibilidad (HA)
Si falla el balanceador principal, un mecanismo de failover cambia el tráfico hacia otro balanceador saludable.
AWS ALB ya es un servicio administrado que incorpora redundancia.
    AWS distribuye los nodos del ALB en múltiples Availability Zones (AZ).
    Un ALB requiere al menos dos zonas de disponibilidad.
    Si una zona falla, puede continuar enviando tráfico a los backends saludables de otra zona.

Por eso no necesitas crear manualmente dos ALB para protegerte contra el fallo de un nodo del balanceador. Para protegerte de fallos regionales, podrías diseñar una arquitectura multirregión con Route 53 y DNS Failover.

Ojo: la alta disponibilidad del balanceador no elimina otros SPOF, como una única base de datos PostgreSQL sin réplica.

Si Nginx falla, los servidores siguen funcionando, pero la aplicación queda inaccesible.

Soluciones:
Redundancia: múltiples instancias.
HA (High Availability): alta disponibilidad.
Failover: cambio automático a un recurso saludable.
Health Checks: detección de fallos.
Multi-AZ: distribución entre zonas de disponibilidad.
Multi-Region: protección adicional ante fallos regionales.

AWS:
ALB incorpora redundancia mediante múltiples AZ.
Route 53 permite DNS Failover.
RDS Multi-AZ ayuda a proteger la base de datos.

**AWS – Orden de componentes**

Cliente → Route 53 (DNS + Failover) → ALB → Backend (Spring Boot)

- Route 53: resuelve el dominio y selecciona el destino.
- DNS Failover: funcionalidad de Route 53 para cambiar de destino ante fallos.
- ALB: distribuye las peticiones HTTP/HTTPS.
- Backend: procesa las solicitudes.

**Clave:** DNS Failover no es un servicio independiente, es una política de enrutamiento de Route 53.

### 09 / 88 · Logs en pipelines

**Pregunta:** El despliegue automatizado de un pipeline falla; a simple vista, los logs indican errores en el código, pero no está claro dónde ocurrió la falla. Estos registros pueden mejorarse mediante:

- **A.** El equipo DevOps
- **B.** Cambiar las herramientas de integración
- **C.** El departamento de QA automatizado
- **D.** No hay manera; leer logs en profundidad es una habilidad fundamental de DevOps
- **E.** El equipo de desarrollo

**Respuesta correcta:** E. El equipo de desarrollo

**Explicación:** El equipo de desarrollo conoce el comportamiento interno del código y puede incorporar logs estructurados, mensajes descriptivos, stack traces y trace IDs para identificar fallos. DevOps también participa configurando la recolección y visualización de logs, por lo que en la práctica es una responsabilidad compartida.

## Seguridad — Preguntas 10 a 15

### 10 / 88 · Gestión de riesgos

**Pregunta:** Por lo general, las respuestas a los riesgos incluyen:

- **A.** Prevención
- **B.** Todas las anteriores
- **C.** Aceptación
- **D.** Mitigación
- **E.** Ninguna de las anteriores

**Respuesta correcta:** B. Todas las anteriores

**Explicación:** Una organización puede prevenir o evitar un riesgo, aceptarlo cuando su impacto es tolerable, o mitigarlo mediante controles que reduzcan su probabilidad o consecuencias. En muchos marcos de gestión también se considera la transferencia del riesgo, por ejemplo, mediante seguros.

### 11 / 88 · Criptografía asimétrica

**Pregunta:** Los algoritmos de clave asimétrica Diffie-Hellman y RSA son de tipo:

- **A.** Cifrado asimétrico
- **B.** Cifrado de clave simétrica
- **C.** Cifrado de seguridad

**Respuesta correcta:** A. Cifrado asimétrico

**Explicación:** La criptografía asimétrica utiliza claves públicas y privadas. RSA puede utilizarse para cifrado y firmas digitales. Diffie-Hellman permite establecer un secreto compartido entre participantes y, aunque pertenece a la criptografía asimétrica, no cifra mensajes directamente.

### 12 / 88 · Autenticación y autorización

**Pregunta:** \_\_\_\_\_ es la forma de asegurar que solo los usuarios con permisos puedan acceder a una red. Mientras que \_\_\_\_\_ permite acceder a recursos necesarios, como bases de datos o archivos específicos.

- **A.** Autenticación y autorización
- **B.** Control del nivel de permisos de red y autorización
- **C.** Autorización y autenticación

**Respuesta correcta:** A. Autenticación y autorización

**Explicación:** La autenticación verifica la identidad del usuario: quién es. La autorización determina qué recursos y operaciones puede utilizar. Por ejemplo, Spring Security puede autenticar mediante JWT y después evaluar roles o permisos para acceder a un endpoint.

### 13 / 88 · MFA

**Pregunta:** ¿Cuál de las siguientes opciones recomendarías para añadir una capa adicional de seguridad al inicio de sesión de los usuarios de tu empresa?

- **A.** Usar contraseñas de al menos 16 caracteres
- **B.** Usar contraseñas distintas para cuentas distintas
- **C.** Eliminar contraseñas repetidas
- **D.** Autenticación multifactor (MFA)

**Respuesta correcta:** D. Autenticación multifactor (MFA)

**Explicación:** MFA añade un factor independiente al inicio de sesión, como una llave de seguridad o aplicación de autenticación. Así, aunque alguien robe una contraseña, necesitaría superar una verificación adicional. Las contraseñas fuertes siguen siendo importantes, pero no representan por sí solas un segundo factor.

### 14 / 88 · Sistema de gestión de seguridad

**Pregunta:** Trabajas en una empresa de tecnología financiera en el área de seguridad de la información, y te piden asesoramiento porque quieren implementar un marco de políticas y controles para gestionar la seguridad y el riesgo en toda la organización. ¿Qué les recomendarías?

- **A.** Realiza un estudio para identificar todos los riesgos y cómo los gestionarías.
- **B.** Implementación de un sistema de gestión de la seguridad de la información
- **C.** Usted indica que le llevará muchos años lograr lo que solicita y que sería mejor buscar la ayuda de un consultor especializado.

**Respuesta correcta:** B. Implementación de un sistema de gestión de la seguridad de la información

**Explicación:** Un SGSI permite establecer políticas, responsabilidades, controles, evaluaciones de riesgos y auditorías de seguridad de manera integral. Puede basarse en ISO 27001 y fomenta la mejora continua de la seguridad de la información en toda la organización.

### 15 / 88 · Ingeniería social

**Pregunta:** Supongamos lo siguiente:

Un estafador crea una cuenta de correo electrónico prácticamente idéntica a la del director del departamento de contabilidad de la startup donde trabajas y envía instrucciones a un empleado por correo electrónico para que realice una transferencia bancaria de 100 000 dólares a una cuenta en el extranjero con extrema urgencia.

¿Qué tipo de ataque crees que llevó a cabo el estafador?

- **A.** Ingeniería social
- **B.** Estafas por correo electrónico
- **C.** Violación de cuenta de correo electrónico

**Respuesta correcta:** A. Ingeniería social

**Explicación:** La ingeniería social manipula a las personas para conseguir información o acciones indebidas. En este escenario, el atacante utiliza suplantación de identidad, autoridad y urgencia para convencer al empleado de transferir dinero. Es una modalidad de fraude empresarial conocida como BEC (Business Email Compromise).

## Desarrollo web — Preguntas 16 a 26

### 16 / 88 · Método POST

**Pregunta:** En una API REST, ¿cuál de las siguientes afirmaciones se aplica al método POST?

- **A.** Envía una entidad al recurso especificado y provoca un cambio de estado o efectos secundarios en el servidor.
- **B.** Aplica modificaciones parciales a un recurso.
- **C.** Reemplaza la representación del recurso de destino con la carga útil de la solicitud especificada.

**Respuesta correcta:** A. Envía una entidad al recurso especificado y provoca un cambio de estado o efectos secundarios en el servidor.

**Explicación:** POST envía información al servidor para su procesamiento y puede utilizarse para crear recursos, como una nueva orden. PATCH se usa para actualizaciones parciales y PUT para reemplazar la representación de un recurso. POST no es idempotente por defecto.

### 17 / 88 · Seguridad de contraseñas

**Pregunta:** ¿Cuáles de estas cosas NO debes hacer al crear un sistema de autenticación?

- **A.** Permitir proveedores de identidad de terceros
- **B.** Limitar la frecuencia de los intentos de inicio de sesión
- **C.** Almacena las contraseñas como texto plano.
- **D.** Crear una estructura de roles

**Respuesta correcta:** C. Almacena las contraseñas como texto plano.

**Explicación:** Almacenar contraseñas sin protección permite que cualquier persona con acceso a la base de datos pueda leerlas. La práctica recomendada es almacenar hashes seguros con sal, utilizando algoritmos como Argon2id o bcrypt, en lugar de guardar contraseñas originales.

### 18 / 88 · Server-Side Rendering

**Pregunta:** ¿Necesitas implementar renderizado del lado del servidor (SSR) en React? ¿Cuál de las siguientes bibliotecas lo hace de forma predeterminada?

- **A.** Expresar
- **B.** ReactuarHidratar
- **C.** Próximo
- **D.** Redux

**Respuesta correcta:** C. Próximo

**Explicación:** La respuesta se refiere a Next.js, un framework de React que permite renderizar contenido en el servidor. Esto puede mejorar el tiempo de visualización inicial y facilitar el SEO. Next.js también admite generación estática y renderizado en el cliente; no todas las rutas utilizan SSR obligatoriamente.

### 19 / 88 · Caché

**Pregunta:** ¿Por qué es importante usar algún tipo de caché en tu sitio web?

- **A.** Mejorar la capacidad de respuesta de la página
- **B.** Mayor disponibilidad de datos
- **C.** Todos
- **D.** Mejorar el tiempo de carga de la página

**Respuesta correcta:** C. Todos

**Explicación:** La caché almacena temporalmente información para evitar procesar o consultar repetidamente los mismos datos. Esto mejora el tiempo de respuesta, reduce carga sobre los servidores y puede aumentar la disponibilidad del contenido cuando el origen no responde, dependiendo de la arquitectura.

### 20 / 88 · WebSockets

**Pregunta:** ¿Cuál de las siguientes es una URL de WebSockets con el formato correcto?

- **A.** ws\://devsu.com/v1/sockets
- **B.** websockets\://devsu.com/v1/sockets
- **C.** https\://devsu.com/sockets
- **D.** wk://devsu.com/sockets

**Respuesta correcta:** A. ws\://devsu.com/v1/sockets

**Explicación:** WebSocket utiliza los esquemas `ws://` y `wss://` para establecer conexiones bidireccionales persistentes. `ws://` no utiliza TLS, mientras que `wss://` permite comunicación cifrada, recomendable para producción. Los otros esquemas no representan URLs WebSocket estándar.

### 21 / 88 · APIs del navegador

**Pregunta:** ¿Qué tipo de tecnología debería utilizar una aplicación del lado del cliente?

- **A.** API web
- **B.** API del sistema operativo
- **C.** Base de datos integrada
- **D.** Acceso directo a archivos

**Respuesta correcta:** A. API web

**Explicación:** Una aplicación web del lado del cliente utiliza las Web APIs proporcionadas por el navegador, como Fetch API, DOM API, Web Storage y WebSocket API. Estas permiten comunicarse con servidores, manipular interfaces y almacenar información sin acceder directamente a recursos privilegiados del sistema operativo.

### 22 / 88 · Puertos HTTP y HTTPS

**Pregunta:** ¿Cuáles de los siguientes puertos son utilizados por defecto por HTTP y HTTPS respectivamente?

- **A.** 80.5000
- **B.** 3000, 80
- **C.** 80.442
- **D.** 80.443

**Respuesta correcta:** D. 80.443

**Explicación:** HTTP utiliza por defecto el puerto 80, mientras HTTPS utiliza el puerto 443 para conexiones cifradas mediante TLS. Los servidores pueden configurarse con otros puertos, pero esos son los valores predeterminados.

### 23 / 88 · Renderizado web

**Pregunta:** Una empresa está interesada en adquirir un panel de administración web para uso interno; ¿qué tipo de aplicación debería recibir?

- **A.** Una aplicación generada estáticamente
- **B.** Aplicación renderizada del lado del cliente
- **C.** Una aplicación entregada a través de CDN
- **D.** Aplicación renderizada en el servidor

Respuesta correcta propuesta: D. Aplicación renderizada en el servidor

**Explicación:** El renderizado del lado del servidor permite generar vistas dinámicas usando información de usuarios y del negocio. Sin embargo, esta pregunta es ambigua: los paneles administrativos internos también pueden implementarse perfectamente como SPA con React y renderizado del lado del cliente. No existe una regla técnica que obligue a utilizar SSR para este escenario.

### 24 / 88 · Code Splitting

**Pregunta:** Las aplicaciones web modernas suelen tener sus archivos Javascript y CSS necesarios en bloques separados que se pueden cargar en diferentes partes; ¿cómo se denomina esta estrategia?

- **A.** División de códigos
- **B.** Carga diferida
- **C.** Minificación
- **D.** Agrupación

**Respuesta correcta:** A. División de códigos

**Explicación:** Code Splitting divide el código JavaScript y otros recursos en archivos más pequeños llamados chunks. Así, una aplicación puede cargar únicamente el código necesario para una ruta o funcionalidad, reduciendo el tamaño de la descarga inicial. Lazy loading complementa esta técnica al cargar esos recursos cuando se necesitan.

### 25 / 88 · Patrón Observer

**Pregunta:** El patrón \_\_\_\_\_ se utiliza para que un objeto pueda notificar a un número ilimitado de otros objetos.

- **A.** Prototipo
- **B.** MVC
- **C.** Semifallo
- **D.** Observador

**Respuesta correcta:** D. Observador

**Explicación:** El patrón Observer permite que un objeto, llamado sujeto, mantenga múltiples observadores suscritos y les notifique cuando ocurra un cambio. Es útil para sistemas basados en eventos, interfaces reactivas y mecanismos de publicación y suscripción.

### 26 / 88 · HATEOAS

**Pregunta:** ¿Qué es cierto acerca del principio HATEOAS?

- **A.** Cuando se trata de hipermedia, esos recursos deben tener su propio punto final.
- **B.** Dado un punto final genérico de nuestra API REST, debería poder descubrir sus recursos basándose únicamente en la respuesta del servidor.
- **C.** Todo lo anterior.
- **D.** Los puntos finales de tu API deben ser lo suficientemente claros como para que un cliente pueda utilizarlos incluso sin leer la documentación.

**Respuesta correcta:** B. Dado un punto final genérico de nuestra API REST, debería poder descubrir sus recursos basándose únicamente en la respuesta del servidor.

**Explicación:** HATEOAS (Hypermedia as the Engine of Application State) establece que una API REST debe proporcionar enlaces y acciones en sus respuestas para que el cliente pueda descubrir cómo interactuar con los recursos. Por ejemplo, la respuesta de una orden podría incluir enlaces para consultar su estado o cancelarla. No basta con que las URLs sean intuitivas.

## Diseño de sistemas — Preguntas 27 a 39

### 27 / 88 · Patrones arquitectónicos

**Pregunta:** Los patrones de arquitectura son difíciles de cambiar o reestructurar una vez que la aplicación ya ha sido construida.

- **A.** Una vez implementadas, no se pueden cambiar.
- **B.** Sí, a menudo es difícil realizar cambios una vez que la aplicación está desarrollada.
- **C.** No, son mucho más fáciles de inyectar, modificar y añadir que la arquitectura general.

**Respuesta correcta:** B. Sí, a menudo es difícil realizar cambios una vez que la aplicación está desarrollada.

**Explicación:** Las decisiones arquitectónicas afectan la estructura del código, las dependencias, la persistencia y los mecanismos de comunicación. Cambiar de monolito a microservicios, por ejemplo, puede requerir modificar muchos componentes y migrar datos. No es imposible, pero puede resultar costoso.

### 28 / 88 · Acoplamiento

**Pregunta:** A continuación se muestra una lista de tipos de acoplamiento entre módulos. Seleccione el peor tipo de acoplamiento.

- **A.** Acoplamiento de control
- **B.** Acoplamiento de contenido
- **C.** Acoplamiento de datos

**Respuesta correcta:** B. Acoplamiento de contenido

**Explicación:** El acoplamiento de contenido ocurre cuando un módulo accede directamente a los detalles internos de otro módulo o modifica sus datos. Esto rompe el encapsulamiento y provoca que un cambio interno pueda afectar a otros componentes. Es uno de los tipos de acoplamiento más perjudiciales.

### 29 / 88 · SOLID y POO

**Pregunta:** ¿Es necesario conocer la programación orientada a objetos para poder implementar los principios SOLID en el desarrollo?

- **A.** Ambas cosas significan lo mismo.
- **B.** Sí, tienes que conocer conceptos como herencia, polimorfismo, abstracción y encapsulación.
- **C.** No. Solo necesitas conocer los principios SOLID.

**Respuesta correcta:** B. Sí, tienes que conocer conceptos como herencia, polimorfismo, abstracción y encapsulación.

**Explicación:** Los principios SOLID surgieron principalmente para mejorar el diseño orientado a objetos. Comprender abstracción, interfaces, encapsulación y polimorfismo permite aplicar correctamente principios como inversión de dependencias y sustitución de Liskov. Aunque algunas ideas de SOLID pueden aplicarse en otros paradigmas, conocer POO es fundamental para su uso tradicional.

### 30 / 88 · Virtualización

**Pregunta:** Trabajas en el área de sistemas de una empresa de desarrollo de software y te asignan una tarea en la que tendrás que ejecutar múltiples sistemas operativos y aplicaciones en un solo servidor. ¿Cómo lo lograrías?

- **A.** Recomiendas que es mejor comprar varios servidores.
- **B.** Es imposible hacer lo que se te pide.
- **C.** Mediante la virtualización

**Respuesta correcta:** C. Mediante la virtualización

**Explicación:** La virtualización permite ejecutar varias máquinas virtuales sobre un único servidor físico mediante un hipervisor. Cada máquina virtual puede disponer de su propio sistema operativo, memoria y recursos asignados, sin necesidad de comprar un servidor independiente.

### 31 / 88 · Domain-Driven Design

**Pregunta:** Es necesario implementar un enfoque de ingeniería de software donde la solución gire en torno al modelo de negocio, conectando la ejecución con los principios empresariales clave. De la siguiente lista, ¿cuál usarías para lograrlo?

- **A.** Arquitectura basada en eventos
- **B.** Diseño orientado al dominio
- **C.** Diseño basado en atributos

**Respuesta correcta:** B. Diseño orientado al dominio

**Explicación:** DDD (Domain-Driven Design) busca que el diseño del software refleje las reglas y conceptos del negocio. Utiliza herramientas como entidades, value objects, agregados, lenguaje ubicuo y bounded contexts. Esto ayuda a organizar la aplicación alrededor de sus dominios empresariales.

### 32 / 88 · AWS EventBridge

**Pregunta:** ¿Qué componente de AWS se puede utilizar para implementar una arquitectura basada en eventos?

- **A.** AWS Event Bridge
- **B.** Amazon Cognito
- **C.** Administrador de sistemas de Amazon
- **D.** Amazon CloudFormation

**Respuesta correcta:** A. AWS Event Bridge

**Explicación:** Amazon EventBridge es un servicio administrado que permite recibir, filtrar y distribuir eventos entre aplicaciones y servicios AWS. Por ejemplo, un evento de creación de una orden puede activar procesos de notificación o logística sin acoplar directamente al productor con los consumidores.

### 33 / 88 · Arquitectura basada en eventos

**Pregunta:** ¿Qué debemos tener en cuenta para implementar una arquitectura basada en eventos?

- **A.** Reducir costos
- **B.** Sus requisitos de control de rendimiento
- **C.** Servicios desacoplados

**Respuesta correcta:** C. Servicios desacoplados

**Explicación:** Una arquitectura basada en eventos busca que los componentes se comuniquen mediante eventos sin depender directamente unos de otros. Esto permite agregar nuevos consumidores sin modificar al productor. El desacoplamiento facilita la evolución y escalabilidad de los sistemas distribuidos.

### 34 / 88 · Multitenencia

**Pregunta:** Seleccione cuál no es una forma de implementar la arquitectura de multitenencia.

- **A.** Base de datos y esquemas de usuario compartidos: todos los usuarios acceden a la misma aplicación y a la misma base de datos.
- **B.** Base de datos independiente por usuario
- **C.** Se crea una instancia de la aplicación para cada usuario, lo que permite que la solución sea personalizada por cada usuario.
- **D.** Base de datos compartida pero con esquemas diferentes.

Respuesta correcta propuesta: C. Se crea una instancia de la aplicación para cada usuario, lo que permite que la solución sea personalizada por cada usuario.

**Explicación:** La multitenencia permite que diferentes clientes, llamados tenants, compartan una plataforma manteniendo aislamiento lógico de sus datos. Las implementaciones habituales incluyen una base compartida, esquemas separados o bases independientes. Una aplicación dedicada a cada cliente se aproxima a single-tenancy, aunque también puede existir dentro de una plataforma SaaS multitenant.

### 35 / 88 · Computación distribuida

**Pregunta:** Indica cuáles de los conceptos expresados a continuación pertenecen a la computación distribuida.

- **A.** Proporciona un conjunto de recursos compartidos y configurables bajo demanda, a los que se puede acceder mediante conceptos como el pago por uso.
- **B.** Ayuda a mejorar los tiempos de resolución de problemas.
- **C.** Es una técnica informática que ofrece servicios alojados a través de Internet.

Respuesta correcta propuesta: A. Proporciona un conjunto de recursos compartidos y configurables bajo demanda, a los que se puede acceder mediante conceptos como el pago por uso.

**Explicación:** La opción A describe principalmente la computación en la nube, que ofrece recursos compartidos y configurables bajo demanda. La nube generalmente utiliza infraestructura distribuida, por lo que ambos conceptos están relacionados. Sin embargo, computación distribuida y cloud computing no significan exactamente lo mismo.

### 36 / 88 · Arquitectura SOA

**Pregunta:** En una arquitectura orientada a servicios, existe un conjunto de principios que deben cumplirse. Seleccione cuáles de los siguientes principios pertenecen a este tipo de arquitectura.

- **A.** Los servicios no deben ser aislados; deben tener un enfoque general.
- **B.** Los servicios adquieren un acuerdo de comunicación, tal como se define en conjunto con uno o más documentos.
- **C.** Los servicios deben estar estrechamente vinculados.
- **D.** Los servicios deben limitarse a tres niveles, cuyos conceptos deben estar claramente definidos.

**Respuesta correcta:** B. Los servicios adquieren un acuerdo de comunicación, tal como se define en conjunto con uno o más documentos.

**Explicación:** La arquitectura orientada a servicios (SOA) utiliza contratos que definen cómo deben comunicarse e interactuar los servicios. Estos contratos pueden especificar operaciones, mensajes y protocolos. SOA favorece el bajo acoplamiento y no exige que los servicios estén estrechamente vinculados.

### 37 / 88 · Pruebas de microservicios

**Pregunta:** Completa seleccionando de la lista el orden correcto de las tres categorías de pruebas utilizadas en microservicios:

\_\_\_\_\_\_: se utilizan para realizar pruebas de aceptación. \_\_\_\_\_\_: se realizan pruebas generales como pruebas de rendimiento y pruebas unitarias. \_\_\_\_\_\_: se utilizan para pruebas exploratorias.

- **A.** Pruebas de nivel superior, pruebas de nivel inferior, pruebas de nivel medio
- **B.** Pruebas de nivel inferior, pruebas de nivel medio, pruebas de nivel superior
- **C.** Pruebas de nivel medio, pruebas de nivel inferior, pruebas de nivel superior

Respuesta correcta propuesta: C. Pruebas de nivel medio, pruebas de nivel inferior, pruebas de nivel superior

**Explicación:** Esta es la clasificación propuesta en el cuestionario, pero no corresponde exactamente a la pirámide de pruebas habitual. Normalmente, las pruebas unitarias se encuentran en la base, las pruebas de integración en el nivel medio y las pruebas end-to-end o de aceptación en los niveles superiores. Las pruebas exploratorias no tienen una posición universal fija.

### 38 / 88 · Comunicación entre microservicios

**Pregunta:** En arquitecturas basadas en microservicios, cuando cada componente quiere comunicarse con otro, la forma correcta de llevar a cabo esta comunicación es:

- **A.** Consumir un punto final del microservicio de destino
- **B.** Escribir directamente en la fuente de datos asociada con el microservicio de destino.
- **C.** Escribir en una cola que es escuchada por el microservicio de destino.

Respuestas técnicamente correctas: A y C.

**Explicación:** La opción A representa comunicación síncrona mediante HTTP o gRPC, donde un servicio consume el endpoint de otro. La opción C representa comunicación asíncrona mediante mensajería, como RabbitMQ o Amazon SQS. Ambas son válidas según las necesidades de la arquitectura. La opción B es incorrecta porque un microservicio no debería modificar directamente los datos privados de otro.

### 39 / 88 · Fork-Join

**Pregunta:** Existe un conjunto de patrones para ejecutar algoritmos paralelos. De las siguientes características, indique cuál pertenece al conocido patrón Fork-Join.

- **A.** Genera dos ejecuciones concurrentes que comienzan después de que se llama al proceso principal. Luego se utiliza una instrucción para unirse a la instrucción de la que se separó.
- **B.** Combina cada elemento de una colección en un solo elemento utilizando una función combinatoria.
- **C.** Replica una función sobre todos los elementos de un conjunto de entrada.

**Respuesta correcta:** A. Genera dos ejecuciones concurrentes que comienzan después de que se llama al proceso principal. Luego se utiliza una instrucción para unirse a la instrucción de la que se separó.

**Explicación:** Fork-Join divide un trabajo en varias tareas que pueden ejecutarse en paralelo (fork) y posteriormente sincroniza sus resultados (join). En Java existe el framework `ForkJoinPool`, útil para algoritmos recursivos que pueden dividirse en subtareas independientes.

## Infraestructura en la nube — Preguntas 40 a 51

### 40 / 88 · Procesamiento distribuido

**Pregunta:** ¿Qué es un sistema de procesamiento distribuido?

- **A.** Es un sistema que utiliza una sola unidad de procesamiento para funcionar.
- **B.** Es un sistema que utiliza más de una unidad de procesamiento para funcionar.
- **C.** Es un sistema que distribuye unidades de procesamiento a otros sistemas diferentes.
- **D.** Es un sistema que distribuye todo el trabajo en una sola unidad de procesamiento.

**Respuesta correcta:** B. Es un sistema que utiliza más de una unidad de procesamiento para funcionar.

**Explicación:** Un sistema de procesamiento distribuido utiliza múltiples nodos o computadoras que colaboran para ejecutar tareas. Cada nodo puede procesar parte del trabajo y comunicarse con los demás por una red. Esto permite distribuir cargas y mejorar la capacidad de procesamiento.

### 41 / 88 · Nube pública

**Pregunta:** ¿Qué es una nube pública?

- **A.** Se trata de una nube comunitaria compartida por organizaciones similares.
- **B.** Se trata de una nube que hace referencia a múltiples nubes híbridas.
- **C.** Se trata de una nube que permite a un cliente específico acceder a servicios y sistemas.
- **D.** Se trata de una nube que permite a cualquier persona acceder a servicios y sistemas.

**Respuesta correcta:** D. Se trata de una nube que permite a cualquier persona acceder a servicios y sistemas.

**Explicación:** La nube pública ofrece infraestructura y servicios de proveedores como AWS, Azure o Google Cloud a clientes que pueden contratar sus recursos. Los servicios están disponibles comercialmente para diferentes organizaciones, aunque cada cliente conserva mecanismos de aislamiento, permisos y seguridad sobre sus datos.

### 42 / 88 · Serverless

**Pregunta:** Este tipo de modelo permite trabajar mediante abstracciones de servidores físicos, siendo el proveedor de la nube el responsable de su gestión.

- **A.** Monolítico
- **B.** n-niveles
- **C.** Servidor cliente
- **D.** Sin servidor

**Respuesta correcta:** D. Sin servidor

**Explicación:** Serverless permite ejecutar aplicaciones sin administrar directamente los servidores subyacentes. El proveedor se encarga de la infraestructura y del aprovisionamiento de capacidad. Por ejemplo, AWS Lambda ejecuta funciones cuando se invocan, mientras el desarrollador administra el código, la configuración y la seguridad de la aplicación.

### 43 / 88 · Elasticidad

**Pregunta:** Este concepto se refiere a la capacidad de un sistema para adaptarse automáticamente a los cambios en la carga de trabajo.

- **A.** Escalabilidad
- **B.** Seguridad
- **C.** Elasticidad
- **D.** Fiabilidad

**Respuesta correcta:** C. Elasticidad

**Explicación:** La elasticidad permite aumentar o reducir automáticamente los recursos según la demanda. Por ejemplo, si las solicitudes aumentan, AWS Auto Scaling puede agregar instancias; cuando disminuyen, puede retirarlas. La diferencia con escalabilidad es que esta última no necesariamente implica automatización.

### 44 / 88 · SaaS, PaaS e IaaS

**Pregunta:** ¿Cuál es el orden de abstracción de los modelos de computación en la nube (de mayor a menor)?

- **A.** PaaS - SaaS - IaaS
- **B.** SaaS - IaaS - PaaS
- **C.** IaaS - PaaS - SaaS
- **D.** SaaS - PaaS - IaaS

**Respuesta correcta:** D. SaaS - PaaS - IaaS

**Explicación:** SaaS ofrece aplicaciones listas para utilizar y abstrae casi toda la infraestructura. PaaS proporciona una plataforma administrada para desarrollar aplicaciones. IaaS entrega recursos como máquinas virtuales, redes y almacenamiento, pero deja más responsabilidades técnicas al cliente.

### 45 / 88 · Fiabilidad

**Pregunta:** ¿Qué definición describe mejor el concepto de fiabilidad en los sistemas en la nube?

- **A.** Un sistema en la nube fiable es aquel que tiene una alta probabilidad de ejecutar los servicios para los que se requiere.
- **B.** Un sistema en la nube fiable es aquel que incorpora servicios de autenticación de usuarios multifactor, así como alertas para los administradores.
- **C.** Un sistema en la nube fiable es aquel que incluye un servicio de registro para todos sus servicios, incluido el inicio de sesión.
- **D.** Un sistema en la nube fiable es aquel que proporciona soporte al cliente de diferentes maneras, como correo electrónico, asistencia técnica, llamadas, etc.

**Respuesta correcta:** A. Un sistema en la nube fiable es aquel que tiene una alta probabilidad de ejecutar los servicios para los que se requiere.

**Explicación:** La fiabilidad es la capacidad de un sistema para cumplir correctamente sus funciones durante un periodo determinado y bajo condiciones definidas. Incluye aspectos como tolerancia a fallos, funcionamiento estable y recuperación. Las demás opciones describen características de seguridad, monitoreo o soporte.

### 46 / 88 · Hipervisor

**Pregunta:** ¿Qué es un hipervisor?

- **A.** Es un usuario que supervisa el sistema operativo que los empleados desean virtualizar.
- **B.** Se trata de un software que contiene todos los recursos de hardware que un host puede virtualizar.
- **C.** Es un software que permite descargar sistemas operativos para virtualizarlos.
- **D.** Es una capa de software entre el hardware y las máquinas virtuales que crea y ejecuta máquinas virtuales.

**Respuesta correcta:** D. Es una capa de software entre el hardware y las máquinas virtuales que crea y ejecuta máquinas virtuales.

**Explicación:** Un hipervisor permite crear y administrar máquinas virtuales, distribuyendo recursos físicos como CPU, memoria y almacenamiento. También proporciona aislamiento entre ellas. Existen hipervisores de tipo 1, que funcionan directamente sobre el hardware, y de tipo 2, que funcionan sobre un sistema operativo anfitrión.

### 47 / 88 · PaaS

**Pregunta:** ¿Qué definición es válida para el término Plataforma como Servicio?

- **A.** En este modelo, el cliente se encarga de desarrollar una plataforma personalizada, mientras que el proveedor ofrece el hardware.
- **B.** El cliente puede suscribirse a una plataforma web que gestiona sus procesos de negocio según este modelo.
- **C.** En este modelo, el cliente puede desarrollar y gestionar sus soluciones en una plataforma administrada por un tercero.
- **D.** En este modelo, el proveedor de servicios web ofrece procesamiento y almacenamiento a través de un protocolo seguro.

**Respuesta correcta:** C. En este modelo, el cliente puede desarrollar y gestionar sus soluciones en una plataforma administrada por un tercero.

**Explicación:** PaaS permite desarrollar, desplegar y administrar aplicaciones utilizando una plataforma que el proveedor mantiene. El desarrollador se concentra en su aplicación sin administrar directamente servidores, sistema operativo o runtime subyacente. Ejemplos incluyen Azure App Service y Google App Engine.

### 48 / 88 · Resiliencia

**Pregunta:** ¿Qué definición describe mejor el concepto de resiliencia en los sistemas en la nube?

- **A.** Un sistema en la nube resiliente incorpora al menos cinco capas de seguridad, desde usuarios, redes y registros.
- **B.** Un sistema en la nube resiliente es aquel que mantiene una disponibilidad constante superior al 98%.
- **C.** Un sistema en la nube resiliente es aquel que se prepara para posibles fallos e interrupciones, haciendo uso de sistemas redundantes y otras técnicas.
- **D.** Un sistema en la nube resiliente es aquel que puede recuperarse económicamente de ataques o pérdida de clientes mediante planes de contingencia.

**Respuesta correcta:** C. Un sistema en la nube resiliente es aquel que se prepara para posibles fallos e interrupciones, haciendo uso de sistemas redundantes y otras técnicas.

**Explicación:** La resiliencia permite que una aplicación soporte fallos y continúe funcionando o se recupere correctamente. Se implementa con mecanismos como redundancia, reintentos controlados, circuit breakers, failover y recuperación ante desastres.

### 49 / 88 · Elasticidad en la nube

**Pregunta:** Los sistemas en la nube requieren distintos servicios o herramientas para considerarse elásticos. ¿Cuáles son esos servicios?

- **A.** Monitoreo, balanceo de carga, escalado automático
- **B.** Registros, escalado automático, monitoreo
- **C.** Instancias virtuales, balanceo de red, monitoreo
- **D.** Bases de datos SQL, balanceo de carga, serverless

**Respuesta correcta:** A. Monitoreo, balanceo de carga, escalado automático

**Explicación:** El monitoreo permite detectar cambios en la demanda. El escalado automático agrega o retira recursos y el balanceador distribuye las solicitudes entre las instancias disponibles. Estas tecnologías, trabajando juntas, permiten responder dinámicamente a variaciones en la carga.

### 50 / 88 · Almacenamiento AWS

**Pregunta:** ¿Cuáles son los servicios de almacenamiento de AWS?

- **A.** Objetos: Elastic Object Store; archivos: Elastic File Service; bloques: Elastic Block Store
- **B.** Objetos: S3; archivos: Elastic File Service; bloques: Elastic Block System
- **C.** Objetos: Elastic Object Store; archivos: Elastic File System; bloques: Elastic Block Store
- **D.** Objetos: S3; archivos: Elastic File System; bloques: Elastic Block Store

**Respuesta correcta:** D. Objetos: S3; archivos: Elastic File System; bloques: Elastic Block Store

**Explicación:** Amazon S3 almacena objetos, como imágenes y documentos. Amazon EFS proporciona un sistema de archivos compartido para múltiples instancias. Amazon EBS ofrece almacenamiento por bloques utilizado normalmente como volúmenes de discos para EC2.

### 51 / 88 · Sincronización de tiempo

**Pregunta:** Un problema importante de la computación distribuida es sincronizar la hora entre subsistemas. ¿Qué opción ofrece una solución tangible?

- **A.** Algoritmo de Kruskal para encontrar la ruta más rápida entre puntos interconectados
- **B.** Algoritmo de Martin para buscar la ruta más corta entre subsistemas y calcular retrasos
- **C.** Protocolo Internacional de Tiempo para definir retrasos según distancia y red
- **D.** Protocolo de Tiempo de Red (NTP) para sincronizar subsistemas con UTC mediante algoritmos

**Respuesta correcta:** D. Protocolo de Tiempo de Red (NTP) para sincronizar subsistemas con UTC mediante algoritmos

**Explicación:** NTP (Network Time Protocol) sincroniza los relojes de dispositivos conectados a una red utilizando referencias horarias y estimaciones del retardo. Esto permite mantener horas consistentes entre servidores, algo importante para correlacionar logs, analizar eventos y diagnosticar problemas distribuidos.

## Arquitecto de Soluciones — Preguntas 52 a 64

### 52 / 88 · CQRS

**Pregunta:** En una arquitectura CQRS, ¿cuál es una de las principales desventajas que debe considerarse?

- **A.** No permite escalar horizontalmente la base de datos
- **B.** Aumenta el acoplamiento entre los microservicios
- **C.** Puede generar inconsistencia eventual entre las bases de datos de lectura y escritura
- **D.** Requiere una implementación obligatoria de orquestación centralizada

**Respuesta correcta:** C. Puede generar inconsistencia eventual entre las bases de datos de lectura y escritura

**Explicación:** CQRS separa las operaciones de escritura (Commands) de las operaciones de lectura (Queries). Cuando los modelos de lectura se actualizan mediante eventos asíncronos, puede existir un intervalo en el que los datos de lectura todavía no reflejen la última escritura. Esto se conoce como consistencia eventual. CQRS no obliga a utilizar bases de datos separadas.

### 53 / 88 · Circuit Breaker

**Pregunta:** ¿Cuál de los siguientes patrones permite la resiliencia en un sistema distribuido cuando un servicio dependiente falla?

- **A.** Circuit Breaker
- **B.** API Gateway
- **C.** Event Sourcing
- **D.** CQRS

**Respuesta correcta:** A. Circuit Breaker

**Explicación:** Circuit Breaker protege una aplicación cuando un servicio dependiente empieza a fallar. Después de detectar varios errores, interrumpe temporalmente las llamadas para evitar saturar el servicio afectado y generar fallos en cascada. Sus estados habituales son Closed, Open y Half-Open. En Java puede implementarse con Resilience4j.

### 54 / 88 · Publisher-Subscriber

**Pregunta:** ¿En qué escenario es recomendable aplicar el patrón Publisher-Subscriber en una arquitectura de microservicios?

- **A.** Cuando la seguridad es la principal preocupación en la integración
- **B.** Cuando se necesita garantizar la consistencia fuerte en las transacciones
- **C.** Cuando se requiere una comunicación síncrona entre los servicios
- **D.** Cuando múltiples servicios deben reaccionar a un mismo evento sin depender entre sí

**Respuesta correcta:** D. Cuando múltiples servicios deben reaccionar a un mismo evento sin depender entre sí

**Explicación:** El patrón Publisher-Subscriber permite que un productor publique eventos que pueden ser consumidos por múltiples servicios independientes. Por ejemplo, al crear una orden, los servicios de notificaciones, facturación y analítica pueden reaccionar al evento sin que el servicio de órdenes tenga que invocarlos directamente. Puede implementarse con Kafka u otros sistemas de mensajería.

### 55 / 88 · Arquitectura híbrida

**Pregunta:** En una estrategia de migración a la nube, ¿cuál de las siguientes opciones es una ventaja de una arquitectura híbrida sobre una completamente cloud-native?

- **A.** Reduce la complejidad operativa al eliminar la necesidad de VPNs
- **B.** Garantiza un menor costo de mantenimiento en comparación con modelos completamente en la nube
- **C.** Permite mantener sistemas heredados críticos mientras se modernizan partes de la infraestructura
- **D.** Evita la necesidad de utilizar herramientas de orquestación

**Respuesta correcta:** C. Permite mantener sistemas heredados críticos mientras se modernizan partes de la infraestructura

**Explicación:** Una arquitectura híbrida combina infraestructura local (on-premises) con servicios en la nube. Esto permite conservar aplicaciones heredadas mientras otros componentes se modernizan progresivamente. Es útil para empresas que no pueden migrar todos sus sistemas al mismo tiempo, aunque introduce desafíos de conectividad y operación.

### 56 / 88 · Optimización de costos

**Pregunta:** Un banco necesita reducir los costos de operación de su plataforma digital sin comprometer la disponibilidad. ¿Qué estrategia de arquitectura se recomienda?

- **A.** Reemplazar microservicios con una arquitectura monolítica para reducir costos
- **B.** Utilizar bases de datos monolíticas para evitar latencias en consultas
- **C.** Implementar una arquitectura serverless para cargas de trabajo esporádicas
- **D.** Centralizar todas las APIs en un único punto de entrada sin distribución geográfica

**Respuesta correcta:** C. Implementar una arquitectura serverless para cargas de trabajo esporádicas

**Explicación:** Serverless permite pagar principalmente por las ejecuciones y los recursos consumidos, evitando mantener servidores activos durante periodos sin solicitudes. Es especialmente conveniente para procesos ocasionales, como tareas programadas o procesamiento de eventos. No siempre es la alternativa más económica para cargas constantes.

### 57 / 88 · Sharding en NoSQL

**Pregunta:** ¿Qué técnica se recomienda para minimizar la latencia en consultas en una base de datos NoSQL altamente distribuida?

- **A.** Normalización de datos para evitar duplicaciones
- **B.** Uso de índices secundarios en todas las consultas
- **C.** Evitar cachés en memoria para garantizar datos frescos
- **D.** Replicación y particionamiento de datos con estrategias adecuadas de sharding

**Respuesta correcta:** D. Replicación y particionamiento de datos con estrategias adecuadas de sharding

**Explicación:** Sharding divide los datos entre varios nodos para distribuir las consultas y el procesamiento. La replicación permite mantener copias de información en diferentes ubicaciones, mejorando disponibilidad y, en determinadas condiciones, latencia. Una buena estrategia de particionamiento ayuda a evitar nodos sobrecargados.

### 58 / 88 · NoSQL en sistemas financieros

**Pregunta:** ¿Cuál es una limitación importante al usar bases de datos NoSQL en una arquitectura financiera?

- **A.** No admiten esquemas dinámicos en tiempo de ejecución
- **B.** No pueden almacenar datos estructurados
- **C.** Tienen un menor rendimiento en transacciones complejas y consistencia fuerte
- **D.** No permiten escalar horizontalmente

**Respuesta correcta:** C. Tienen un menor rendimiento en transacciones complejas y consistencia fuerte

**Explicación:** Algunas bases NoSQL priorizan escalabilidad y disponibilidad, por lo que las transacciones complejas entre múltiples registros pueden resultar más difíciles o costosas que en bases relacionales. Sin embargo, no es una limitación universal: varias bases NoSQL modernas ofrecen transacciones ACID y consistencia fuerte.

### 59 / 88 · Event Sourcing

**Pregunta:** En una arquitectura orientada a eventos, ¿qué ventaja ofrece Event Sourcing sobre un modelo tradicional de base de datos?

- **A.** Facilita la eliminación de eventos antiguos para optimizar almacenamiento
- **B.** Reduce la necesidad de registros históricos en la base de datos
- **C.** Evita la replicación de datos entre sistemas
- **D.** Permite reconstrucción de estados pasados y auditoría completa

**Respuesta correcta:** D. Permite reconstrucción de estados pasados y auditoría completa

**Explicación:** Event Sourcing almacena los cambios del sistema como una secuencia de eventos en lugar de guardar únicamente el estado actual. Al reproducir esos eventos se puede reconstruir cómo evolucionó una entidad. Esto facilita auditorías, trazabilidad y recuperación de estados anteriores.

### 60 / 88 · Gestión de secretos

**Pregunta:** ¿Cuál es la mejor práctica para gestionar secretos en una arquitectura basada en microservicios?

- **A.** Almacenar secretos en variables de entorno dentro del código fuente
- **B.** Utilizar un gestor de secretos como Azure Key Vault
- **C.** Incluir credenciales en los archivos de configuración de cada microservicio
- **D.** Encriptar secretos dentro de los logs de la aplicación

**Respuesta correcta:** B. Utilizar un gestor de secretos como Azure Key Vault

**Explicación:** Un gestor de secretos permite almacenar y administrar credenciales, contraseñas, claves y certificados de forma centralizada y segura. También facilita la rotación de secretos, auditoría y control de acceso mediante permisos. Alternativas similares son AWS Secrets Manager y HashiCorp Vault.

### 61 / 88 · OAuth 2.0 y JWT

**Pregunta:** En la gestión de identidad en una arquitectura de microservicios, ¿cuál de las siguientes estrategias es más segura?

- **A.** Permitir accesos sin autenticación dentro de la red interna
- **B.** Autenticación con sesiones almacenadas en cada servicio
- **C.** Implementación de autenticación basada en IP
- **D.** Uso de OAuth 2.0 con JWT para acceso centralizado

**Respuesta correcta:** D. Uso de OAuth 2.0 con JWT para acceso centralizado

**Explicación:** OAuth 2.0 permite delegar autorización mediante tokens de acceso. JWT puede utilizarse como formato de esos tokens para transmitir información verificable entre servicios. Cada microservicio debe validar la firma y las restricciones del token. Cuando se necesita autenticar usuarios, normalmente se utiliza OpenID Connect sobre OAuth 2.0.

### 62 / 88 · Microfrontends

**Pregunta:** ¿Cuál es una ventaja clave de una arquitectura basada en microfrontends?

- **A.** Permite la integración de múltiples tecnologías en el mismo frontend
- **B.** Reduce la complejidad de despliegue de los equipos de backend
- **C.** Elimina la necesidad de un gateway de APIs
- **D.** Facilita la centralización del desarrollo en un solo equipo

**Respuesta correcta:** A. Permite la integración de múltiples tecnologías en el mismo frontend

**Explicación:** Los microfrontends permiten dividir una interfaz grande en componentes o aplicaciones independientes desarrolladas por distintos equipos. Incluso pueden utilizar frameworks diferentes, como React y Angular, dentro de una misma solución. Esto favorece la autonomía de equipos, aunque introduce mayor complejidad de integración.

### 63 / 88 · Observabilidad

**Pregunta:** ¿Qué se debe priorizar en una estrategia de monitoreo de aplicaciones en la nube?

- **A.** Observabilidad de métricas, logs y trazas para análisis en tiempo real
- **B.** Monitoreo de logs solamente en fallos críticos
- **C.** Deshabilitar logs detallados para mejorar rendimiento
- **D.** Uso exclusivo de herramientas de terceros sin integración con la plataforma cloud

**Respuesta correcta:** A. Observabilidad de métricas, logs y trazas para análisis en tiempo real

**Explicación:** La observabilidad se apoya en tres pilares: métricas, logs y trazas. Las métricas permiten detectar problemas de rendimiento, los logs explican eventos y errores, y las trazas muestran cómo viajan las solicitudes entre microservicios. OpenTelemetry permite instrumentar aplicaciones para recopilar esta información.

### 64 / 88 · Caché distribuida

**Pregunta:** En un entorno de alta disponibilidad, ¿qué mecanismo permite minimizar la latencia en servicios distribuidos?

- **A.** Implementación de caché distribuida
- **B.** Reemplazo de balanceadores de carga por configuraciones estáticas
- **C.** Evitar la replicación de bases de datos para mejorar velocidad
- **D.** Uso de colas de mensajes síncronas

**Respuesta correcta:** A. Implementación de caché distribuida

**Explicación:** Una caché distribuida almacena datos consultados frecuentemente en memoria para evitar acceder repetidamente a bases de datos o servicios remotos. Esto reduce tiempos de respuesta y carga de infraestructura. Redis es una tecnología habitual para implementar este mecanismo.

## TPM Architecture — Preguntas 65 a 72

### 65 / 88 · Deuda técnica

**Pregunta:** ¿Cuál de las siguientes puede considerarse una causa de deuda técnica?

- **A.** Tecnología obsoleta
- **B.** Todas las anteriores
- **C.** Presión de tiempo: priorizar rapidez sobre calidad
- **D.** Cambios constantes de alcance o del diseño y desarrollo de funcionalidades

**Respuesta correcta:** B. Todas las anteriores

**Explicación:** La deuda técnica puede originarse por decisiones de implementación apresuradas, tecnologías difíciles de mantener y modificaciones continuas sin refactorización adecuada. Estas situaciones aumentan el costo futuro de mantenimiento y evolución del software.

### 66 / 88 · Características de sistemas distribuidos

**Pregunta:** ¿Cuál de las siguientes no se considera habitualmente una característica de los sistemas distribuidos?

- **A.** Escalabilidad
- **B.** Transparencia
- **C.** No repudio
- **D.** Concurrencia

**Respuesta correcta:** C. No repudio

**Explicación:** La escalabilidad, transparencia y concurrencia son características habituales de los sistemas distribuidos. El no repudio, en cambio, es una propiedad de seguridad que permite demostrar que una entidad realizó determinada acción, por ejemplo, mediante firmas digitales. Puede implementarse en sistemas distribuidos, pero no es una característica arquitectónica que los defina.

### 67 / 88 · Docker y Kubernetes

**Pregunta:** ¿Cuáles son algunas de las herramientas más comunes para implementar microservicios?

- **A.** Node.js y JavaScript
- **B.** Kubernetes y Docker
- **C.** Amazon SageMaker y Cloud Functions

**Respuesta correcta:** B. Kubernetes y Docker

**Explicación:** Docker permite empaquetar aplicaciones y sus dependencias en contenedores. Kubernetes permite administrar, desplegar, escalar y recuperar esos contenedores en un clúster. Estas herramientas son ampliamente utilizadas en arquitecturas de microservicios, aunque no son obligatorias.

### 68 / 88 · Identificación de deuda técnica

**Pregunta:** ¿Cuál de las siguientes NO debe utilizarse para identificar deuda técnica?

- **A.** Realizar análisis exploratorio para detectar errores en el lado del usuario
- **B.** Monitorear rendimiento, velocidad y sesiones sin fallos
- **C.** Realizar una retrospectiva exhaustiva para comprender y priorizar futuras funcionalidades
- **D.** Realizar revisiones periódicas de código y asegurar que esté documentado, optimizado y sea legible

**Respuesta correcta:** C. Realizar una retrospectiva exhaustiva para comprender y priorizar futuras funcionalidades

**Explicación:** La deuda técnica se identifica mediante revisiones de código, análisis de calidad, problemas de mantenimiento y métricas de funcionamiento. Una retrospectiva enfocada exclusivamente en priorizar funcionalidades futuras no evalúa directamente la deuda técnica. Sin embargo, una retrospectiva que incluya problemas técnicos sí puede ayudar a identificarla.

### 69 / 88 · CDN

**Pregunta:** ¿Qué servicio usarías para reducir costos y mejorar velocidad de entrega almacenando contenido estático cerca de los usuarios?

- **A.** Balanceo de carga
- **B.** DNS
- **C.** CDN
- **D.** Cloud Spanner

**Respuesta correcta:** C. CDN

**Explicación:** Una CDN (Content Delivery Network) distribuye y almacena contenido estático, como imágenes, CSS y JavaScript, en servidores geográficamente cercanos a los usuarios. Esto reduce latencia y tráfico hacia el servidor de origen. Amazon CloudFront y Cloudflare son ejemplos.

### 70 / 88 · MySQL y MSSQL

**Pregunta:** ¿Cuál es la diferencia entre MySQL y MSSQL?

- **A.** Son dos sistemas gestores de bases de datos diferentes
- **B.** MySQL solo sirve para uso personal y MSSQL para empresas
- **C.** MySQL es la versión de código abierto de MSSQL
- **D.** Son versiones distintas del mismo gestor de bases de datos

**Respuesta correcta:** A. Son dos sistemas gestores de bases de datos diferentes

**Explicación:** MySQL y Microsoft SQL Server son sistemas de gestión de bases de datos relacionales independientes. Tienen diferencias en herramientas, características, dialectos SQL y licenciamiento. Ambos pueden utilizarse para aplicaciones empresariales de gran escala.

### 71 / 88 · Riesgos en sistemas distribuidos

**Pregunta:** ¿Cuál de estas opciones NO representa un riesgo para los sistemas distribuidos?

- **A.** Menor velocidad y rendimiento debido a que la escalabilidad dificulta el mantenimiento
- **B.** Problemas de gobernanza ante leyes como GDPR
- **C.** Seguridad: mayor exposición por la naturaleza distribuida
- **D.** Fallos de red cuando un servicio no está disponible y afecta el rendimiento

Respuesta correcta propuesta: A. Menor velocidad y rendimiento debido a que la escalabilidad dificulta el mantenimiento

**Explicación:** La escalabilidad busca aumentar la capacidad del sistema para manejar más carga, por lo que no debe entenderse como una causa inevitable de menor rendimiento. Los sistemas distribuidos sí enfrentan riesgos reales de seguridad, cumplimiento normativo y fallos de comunicación. No obstante, también pueden sufrir problemas de latencia y complejidad, por lo que esta respuesta debe interpretarse como la menos adecuada de las alternativas.

### 72 / 88 · Data Warehouse

**Pregunta:** ¿Cuál de estas bases de datos funcionaría mejor como almacén de datos analítico (data warehouse)?

- **A.** Redis
- **B.** MySQL
- **C.** MongoDB
- **D.** Redshift

**Respuesta correcta:** D. Redshift

**Explicación:** Amazon Redshift es un servicio diseñado para almacenamiento y análisis de grandes volúmenes de datos. Está optimizado para consultas analíticas OLAP, agregaciones e inteligencia de negocios. Redis se utiliza principalmente como almacén en memoria, mientras MySQL y MongoDB suelen emplearse para otras necesidades operativas.

## TPM Engineering — Preguntas 73 a 81

### 73 / 88 · HTML

**Pregunta:** ¿Qué es HTML?

- **A.** Una API para desarrollar aplicaciones web rápidas
- **B.** Un lenguaje de programación backend
- **C.** Un protocolo de comunicación
- **D.** Un lenguaje frontend que entienden los navegadores

**Respuesta correcta:** D. Un lenguaje frontend que entienden los navegadores

**Explicación:** HTML (HyperText Markup Language) es un lenguaje de marcado utilizado para estructurar el contenido de las páginas web. Define elementos como títulos, párrafos, formularios, tablas y enlaces. El navegador interpreta HTML para construir el DOM. No es un lenguaje de programación.

### 74 / 88 · Tecnologías backend

**Pregunta:** ¿Cuáles de estas tecnologías se utilizan en desarrollo backend?

- **A.** Python
- **B.** Java
- **C.** HTML
- **D.** Bootstrap
- **E.** React
- **F.** CSS
- **G.** NodeJS

**Respuestas correctas:** A. Python; B. Java; G. NodeJS

**Explicación:** Python y Java permiten implementar servicios, APIs, lógica de negocio y acceso a bases de datos. Node.js es un entorno de ejecución de JavaScript que también permite desarrollar aplicaciones del lado del servidor. HTML, CSS, Bootstrap y React están orientados principalmente al desarrollo de interfaces.

### 75 / 88 · Java vs. JavaScript

**Pregunta:** ¿Cuál es la diferencia entre Java y JavaScript?

- **A.** JavaScript es una versión ligera de Java
- **B.** Java es una versión ligera de JavaScript
- **C.** Java es la versión compilada del lenguaje interpretado JavaScript
- **D.** Son lenguajes completamente diferentes

**Respuesta correcta:** D. Son lenguajes completamente diferentes

**Explicación:** Java y JavaScript son lenguajes independientes que comparten algunas similitudes sintácticas. Java utiliza tipado estático y normalmente se compila a bytecode para ejecutarse en la JVM. JavaScript pertenece al estándar ECMAScript y puede ejecutarse en navegadores o en servidores mediante Node.js.

### 76 / 88 · Menú QR

**Pregunta:** Una cadena de restaurantes necesita un menú digital basado en QR que permita filtrar productos según ubicación e idioma. ¿Qué solución es más adecuada?

- **A.** Una aplicación web no requiere instalación y es más fácil de mantener, desarrollar y actualizar
- **B.** Una aplicación móvil, porque trabaja sin conexión y aprovecha mejor los recursos del sistema
- **C.** Una aplicación móvil, porque todos tienen teléfono y es sencilla de instalar
- **D.** Aplicaciones web porque suelen ser más rápidas que las móviles y el tiempo importa cuando hay hambre

**Respuesta correcta:** A. Una aplicación web no requiere instalación y es más fácil de mantener, desarrollar y actualizar

**Explicación:** Un código QR puede dirigir directamente a una página web que el cliente abre desde su navegador. No necesita instalar una aplicación y el restaurante puede actualizar centralmente productos, idiomas y disponibilidad. Esto reduce la fricción para los usuarios y facilita el mantenimiento.

### 77 / 88 · Control de versiones

**Pregunta:** ¿Qué es un sistema de control de versiones (VCS)?

- **A.** Un sistema que permite a los usuarios finales subir o bajar versiones fácilmente
- **B.** Un sistema para gestionar el código fuente de la aplicación
- **C.** Un sistema para resolver problemas de compatibilidad durante nuevas versiones
- **D.** Un sistema para gestionar versiones y artefactos de despliegue

**Respuesta correcta:** B. Un sistema para gestionar el código fuente de la aplicación

**Explicación:** Un VCS registra los cambios realizados sobre los archivos de un proyecto, permitiendo consultar versiones anteriores, crear ramas, colaborar y revertir modificaciones. Git es uno de los sistemas de control de versiones más utilizados. GitHub y GitLab proporcionan plataformas adicionales para gestionar y colaborar sobre repositorios.

### 78 / 88 · Pruebas unitarias JavaScript

**Pregunta:** ¿Cuál de las siguientes es una herramienta para crear pruebas unitarias en JavaScript?

- **A.** React
- **B.** NodeJS
- **C.** JUnit
- **D.** Jest
- **E.** Pytest

**Respuesta correcta:** D. Jest

**Explicación:** Jest es un framework de pruebas para JavaScript y TypeScript. Permite escribir pruebas unitarias, configurar mocks, realizar aserciones y obtener reportes de cobertura. JUnit se utiliza principalmente para Java y pytest para Python.

### 79 / 88 · Aplicaciones híbridas

**Pregunta:** ¿Cuáles de estas tecnologías sirven para desarrollar aplicaciones híbridas?

- **A.** React Native
- **B.** Kotlin
- **C.** Python
- **D.** Ionic
- **E.** Swift
- **F.** Java
- **G.** Flutter

**Respuestas correctas:** A. React Native; D. Ionic; G. Flutter

**Explicación:** React Native, Ionic y Flutter permiten desarrollar aplicaciones para múltiples plataformas reutilizando gran parte del código. Ionic utiliza tecnologías web, React Native integra componentes nativos y Flutter utiliza su propio motor de renderizado. Técnicamente, no todas son híbridas en sentido estricto, pero sí son soluciones multiplataforma.

### 80 / 88 · Requisitos no funcionales

**Pregunta:** La usabilidad, el rendimiento y la fiabilidad son ejemplos de:

- **A.** Requisitos de red y datos
- **B.** Requisitos funcionales
- **C.** Requisitos no funcionales
- **D.** Requisitos tecnológicos

**Respuesta correcta:** C. Requisitos no funcionales

**Explicación:** Los requisitos no funcionales describen atributos de calidad de un sistema, como rendimiento, disponibilidad, seguridad y usabilidad. Los requisitos funcionales describen lo que el sistema debe hacer, como crear usuarios o registrar órdenes. Los no funcionales determinan las condiciones de calidad bajo las que esas funcionalidades deben ejecutarse.

### 81 / 88 · Beneficios de pruebas unitarias

**Pregunta:** ¿Cuál NO es una ventaja de implementar pruebas unitarias?

- **A.** Ayudan a detectar errores pronto
- **B.** Aportan documentación
- **C.** Reducen el tiempo de desarrollo a corto plazo
- **D.** Mejoran la confiabilidad del software

**Respuesta correcta:** C. Reducen el tiempo de desarrollo a corto plazo

**Explicación:** Implementar pruebas unitarias requiere tiempo inicial para escribir, configurar y mantener los tests. Por eso no siempre reduce el esfuerzo inmediato de desarrollo. Sus mayores ventajas aparecen al detectar errores tempranamente, facilitar refactorizaciones y reducir regresiones durante la evolución del software.

## TPM Management — Preguntas 82 a 88

### 82 / 88 · Agile

**Pregunta:** ¿Cuál de las siguientes opciones describe mejor el objetivo principal de Agile?

- **A.** Entregar valor continuo al usuario lo antes posible
- **B.** Hacer crecer exponencialmente la organización en poco tiempo
- **C.** Promover un ambiente creativo que haga felices y productivos a los trabajadores
- **D.** Generar más ingresos para la organización

**Respuesta correcta:** A. Entregar valor continuo al usuario lo antes posible

**Explicación:** Agile busca entregar incrementos de valor de manera temprana y continua, obteniendo retroalimentación para adaptar el producto a las necesidades de los usuarios. En lugar de esperar hasta el final de un proyecto para entregar resultados, promueve entregas frecuentes y mejora continua.

### 83 / 88 · Gestión de riesgos del cambio

**Pregunta:** ¿Cuál sería un beneficio de gestionar los riesgos del cambio?

- **A.** Centrarse en situaciones negativas y volverlas positivas
- **B.** Preparar planes de mitigación para reducir pronto la resistencia y el impacto negativo
- **C.** Reducir la cantidad de empleados que renuncian
- **D.** Controlar todos los cambios mientras ocurren

**Respuesta correcta:** B. Preparar planes de mitigación para reducir pronto la resistencia y el impacto negativo

**Explicación:** La gestión de riesgos del cambio permite anticipar obstáculos, evaluar su impacto y preparar acciones para reducirlos. Esto ayuda a minimizar resistencia, interrupciones y problemas organizacionales durante la implementación de nuevas tecnologías o procesos.

### 84 / 88 · Matriz de riesgos

**Pregunta:** Una matriz de riesgos permite visualizar y clasificar los riesgos. ¿Sus categorías son obligatoriamente bajo, medio y alto?

- **A.** No: la organización puede definir las categorías
- **B.** Sí: bajo, medio y alto son las categorías de la matriz
- **C.** No: deben ser sin riesgo, bajo, medio, alto y crítico

**Respuesta correcta:** A. No: la organización puede definir las categorías

**Explicación:** Cada organización puede establecer sus propios niveles de clasificación según los criterios de impacto y probabilidad. Algunas utilizan tres niveles, como bajo, medio y alto; otras incluyen crítico o muy bajo. Lo importante es mantener criterios definidos y consistentes.

### 85 / 88 · Orientación a resultados

**Pregunta:** ¿Cuál sería un criterio orientado a resultados?

- **A.** Indicadores que reflejan el avance del equipo hacia la meta
- **B.** Recompensas basadas en el flujo del proceso
- **C.** Lo más importante es cumplir metas y resultados en el plazo establecido
- **D.** Gerentes que apoyan mucho y colaboran con su equipo

**Respuesta correcta:** C. Lo más importante es cumplir metas y resultados en el plazo establecido

**Explicación:** La orientación a resultados se enfoca en alcanzar objetivos concretos y medibles dentro de los plazos acordados. No basta con realizar actividades o seguir procesos correctamente: es necesario evaluar si realmente se lograron los resultados esperados.

### 86 / 88 · Sprint Planning

**Pregunta:** Al inicio del Sprint Planning, los Product Owners empiezan a priorizar historias de usuario para el Sprint. ¿Es correcto?

- **A.** No: el Product Owner debió priorizarlas antes
- **B.** No: hay que priorizarlas al final de la planificación
- **C.** Sí: se priorizarán considerando los aportes del equipo
- **D.** Sí: el resto del equipo esperará hasta terminar la priorización

**Respuesta correcta:** A. No: el Product Owner debió priorizarlas antes

**Explicación:** El Product Owner es responsable de ordenar y mantener actualizado el Product Backlog antes del Sprint Planning. Durante la planificación, el Scrum Team analiza el trabajo prioritario y establece un Sprint Goal, considerando la capacidad del equipo. La reunión no debería comenzar desde cero con la priorización.

### 87 / 88 · Gestión del cambio

**Pregunta:** Para implementar un cambio correctamente necesitas el apoyo de patrocinadores. ¿En qué principio del cambio debes considerar su participación?

- **A.** Planificar el cambio
- **B.** Comunicar el cambio
- **C.** Implementar el cambio
- **D.** Comprender el cambio

**Respuesta correcta:** A. Planificar el cambio

**Explicación:** Los patrocinadores deben involucrarse desde la planificación para proporcionar respaldo, recursos y apoyo organizacional. Su participación temprana ayuda a definir responsabilidades y facilita la comunicación e implementación del cambio durante las siguientes etapas.

### 88 / 88 · Consultoría

**Pregunta:** ¿Cuál de estas personas actúa como consultor?

- **A.** Un reparador que cambia el botón de encendido del computador
- **B.** Un florista que te asesora al elegir flores para tu aniversario
- **C.** Un empleado de supermercado que verifica el precio de un producto
- **D.** Un mesero que te entrega el menú para que escojas qué comer

**Respuesta correcta:** B. Un florista que te asesora al elegir flores para tu aniversario

**Explicación:** Un consultor utiliza su experiencia para analizar una necesidad y recomendar una solución apropiada. El florista asesora al cliente y lo ayuda a decidir según sus preferencias y objetivos. Las demás opciones describen principalmente tareas operativas o entrega de información.

## Nota breve para ColorNote

DEVSU — Evaluación técnica de 88 preguntas

- DevOps: balanceadores L4/L7, SSL/TLS, Git, disponibilidad, logs y contenedores.
- Seguridad: autenticación, autorización, MFA, SGSI e ingeniería social.
- Desarrollo web: REST, POST, SSR, WebSockets, caché, HATEOAS y Observer.
- Arquitectura: SOLID, DDD, SOA, Fork-Join, multitenencia y microservicios.
- Cloud: AWS, EventBridge, S3, EFS, EBS, elasticidad, resiliencia, serverless y NTP.
- Patrones: CQRS, Circuit Breaker, Pub/Sub y Event Sourcing.
- Ingeniería: Docker, Kubernetes, Redis, Redshift, Jest, pruebas unitarias y requisitos no funcionales.
- Gestión: Agile, Scrum, riesgos, liderazgo y planificación del cambio.

Importante: Las respuestas 23, 35, 37 y 71 tienen ambigüedades técnicas. La pregunta 38 admite dos alternativas válidas (A y C), y la opción B de la pregunta 7 está incompleta en el material original.
