# AWS: certificaciones y arquitectura aplicada

Apuntes de estudio de Cloud Practitioner y Developer Associate y decisiones de arquitectura para Delivery Loja Enterprise (Java 21, Spring Boot, ECS/EC2). Fecha: noviembre de 2026. Verificar siempre la guía vigente de cada examen.

## Rutas de certificación
- Foundational: Cloud Practitioner, AI Practitioner.
- Associate: Solutions Architect, Developer, CloudOps Engineer, Data Engineer, Machine Learning Engineer.
- Professional: Solutions Architect, DevOps Engineer.
- Specialty: consultar el catálogo oficial actualizado.
- Ruta arquitectura sugerida: Cloud Practitioner → Solutions Architect Associate → Solutions Architect Professional.
- Ruta desarrollo sugerida: Cloud Practitioner → Developer Associate → DevOps Engineer Professional.
- No existen prerrequisitos obligatorios entre estos exámenes.

## Cloud Practitioner (CLF-C02)
| Dominio | Peso | Temas |
|---|---:|---|
| Conceptos de nube | 24% | IaaS/PaaS/SaaS, regiones y AZ, elasticidad, alta disponibilidad, Well-Architected |
| Seguridad y cumplimiento | 30% | Responsabilidad compartida, IAM, MFA, KMS, WAF, Shield, CloudTrail |
| Tecnología y servicios | 34% | EC2, Lambda, ECS, S3, RDS, DynamoDB, VPC, Route 53, ELB, CloudFront, SQS/SNS |
| Facturación y soporte | 12% | Free Tier, On-Demand, Reserved, Spot, Budgets, Cost Explorer, planes de soporte |

Orientación: reconocer el propósito de los servicios y escenarios de uso, no programarlos.

## Developer Associate (DVA-C02)
| Dominio | Peso | Tecnologías representativas |
|---|---:|---|
| Desarrollo con servicios AWS | 32% | Lambda, API Gateway, DynamoDB, S3, SQS, SNS, EventBridge, Step Functions |
| Seguridad | 26% | IAM, Cognito, KMS, Secrets Manager, OAuth2/OIDC/JWT |
| Despliegue | 24% | CodeBuild, CodeDeploy, CodePipeline, CloudFormation, SAM, Beanstalk |
| Troubleshooting y optimización | 18% | CloudWatch, X-Ray, logs, reintentos, idempotencia, rendimiento |

**Versiones:** porcentajes anteriores son de DVA-C02; revisar la guía de DVA-C03 si corresponde al examen elegido.

## Route 53, ELB, ALB y NLB
- Route 53 resuelve DNS hacia el endpoint (ALB o API Gateway); no es un salto HTTP en cada solicitud. DNS failover puede cambiar respuestas DNS según health checks y políticas, sujeto a cachés/TTL.
- ELB es la familia de balanceadores. No es un balanceador adicional delante de ALB.
- ALB: capa 7, HTTP/HTTPS, reglas por host/path, WebSocket; apropiado para APIs REST y Spring Boot en ECS.
- NLB: capa 4, TCP/UDP/TLS; útil para protocolos de transporte, alto rendimiento, baja latencia y requisitos específicos de red.
- GWLB: appliances virtuales de seguridad; CLB: legado.
- GPS no exige NLB: si el tracking usa HTTPS/WebSocket, ALB es compatible. Si usa protocolo TCP/UDP propio, considerar NLB.
- Riesgo SPOF: diseñar alta disponibilidad multi-AZ, health checks y escalado; no asumir que una sola instancia backend es HA.

## API Gateway frente a ALB
- API Gateway tiene HTTP API, REST API y WebSocket API. REST API ofrece, entre otras capacidades, usage plans y API keys; HTTP API suele ser más sencillo/económico para casos compatibles.
- ALB balancea y enruta tráfico HTTP; API Gateway administra exposición, autorización, throttling, cuotas y consumidores de APIs.
- Tener 3, 20 o 50 microservicios **no obliga** a usar API Gateway. Alta carga tampoco lo obliga.
- Ejemplo bancario B2B: socios consumen `POST /transfers` con autorización, cuotas por consumidor, monitoreo y versionado. Las API keys y cuotas no reemplazan autenticación/autorización robusta, controles antifraude ni límites de negocio.
- Para partners de delivery: exponer contratos específicos como `POST /partner/orders` en lugar de reutilizar indiscriminadamente endpoints internos.
- Si se justifica usar ambos: cliente → DNS Route 53 → API Gateway → VPC Link → ALB interno → servicios ECS (según tipo de API/integración admitida).

## Cognito y Spring Security
1. Login: app web/móvil → Cognito User Pool (opcional federación Google/Facebook) → tokens OAuth2/OIDC.
2. Solicitud API: app con access token Bearer → ALB → Spring Boot.
3. Spring Security OAuth2 Resource Server valida JWT (firma, issuer, expiración y audience/client según configuración) y autoriza por scopes/roles.
4. Reglas de negocio permanecen en backend: un cliente solo puede leer sus pedidos.
5. API Gateway puede añadir un JWT authorizer (según tipo de API); **no es obligatorio** para integrar Cognito.
6. ALB dispone de funciones de autenticación OIDC/Cognito en ciertos escenarios, pero no debe confundirse con un autorizador JWT genérico de APIs.

## Delivery Loja Enterprise: propuesta incremental
**Base:** app móvil/web → Route 53 (resolución DNS) → ALB público HTTPS → servicios Spring Boot en ECS sobre EC2 → PostgreSQL. Cognito autentica usuarios; Spring Security protege cada servicio. Merchants y Dispatch pueden tener despliegue/BD separados según las decisiones del proyecto. Considerar Redis, Kafka/outbox, observabilidad, autoscaling y multi-AZ según carga real y presupuesto.

**Evolución opcional:** API Gateway frente a servicios privados cuando se requieran políticas centralizadas, API products, cuotas por partners o integraciones B2B. Evaluar costo, latencia, seguridad y complejidad adicional. No añadir API Gateway solo por tener múltiples canales web/móvil.

## Preguntas rápidas de examen
- `/orders` y `/users` hacia backends distintos según ruta HTTP → ALB.
- Conexiones UDP de rastreo con protocolo propio → considerar NLB.
- Ejecutar código sin administrar servidores → Lambda.
- Resolver `api.midominio.com` → Route 53.
- Autenticar usuarios y emitir tokens → Cognito User Pools.
- Administrar APIs externas con cuotas y planes de uso → API Gateway REST API.
- Enviar tareas desacopladas → SQS; publicar a múltiples suscriptores → SNS; rutear eventos por reglas → EventBridge.

## Referencias oficiales
- [AWS Certification](https://aws.amazon.com/certification/)
- [Cloud Practitioner exam](https://aws.amazon.com/certification/certified-cloud-practitioner/)
- [Developer Associate exam](https://aws.amazon.com/certification/certified-developer-associate/)
- [Elastic Load Balancing](https://docs.aws.amazon.com/elasticloadbalancing/latest/userguide/what-is-load-balancing.html)
- [API Gateway](https://docs.aws.amazon.com/apigateway/latest/developerguide/welcome.html)
- [API Gateway private integrations](https://docs.aws.amazon.com/apigateway/latest/developerguide/http-api-vpc-links.html)
- [Amazon Cognito](https://docs.aws.amazon.com/cognito/latest/developerguide/what-is-amazon-cognito.html)
- [Spring Security OAuth2 Resource Server](https://docs.spring.io/spring-security/reference/servlet/oauth2/resource-server/jwt.html)
