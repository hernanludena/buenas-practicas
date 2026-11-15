# Diplomado Ejecutivo en Modernización de la Arquitectura de Software y Cloud

**Institución:** LT Tech (Lite Thinking University of Technology)  
**Duración indicada:** 1 semestre  
**Fuente:** folleto PDF «2026-software-architecture-cloud-modernization», páginas 5–22.  
**Estado:** Índice registrado; estudio pendiente de iniciar.

> Guía de estudio personal basada en el temario público del folleto. Los títulos y temas se mantienen; las agrupaciones internas son una organización de seguimiento. No representa matrícula ni certificación oficial.

## Certificación 1 — Gobierno y Estrategia de Arquitectura de Software (pp. 5–7)
- Introducción y contexto: contextualización e introducción a arquitectura; arquitecto y equipo; responsabilidades.
- Marcos y modelos: arquitectura empresarial, TOGAF, Zachman; modelos visuales C4 y ArchiMate.
- Principios y atributos: atributos de calidad, características y decisiones arquitectónicas, componentes lógicos.
- Modelado y documentación: orientación a objetos; UML vs C4; diagramas de clases y otros; planos; validación.
- Estilos: monolítica, capas, cliente-servidor, serverless, microkernel, event-driven.
- Patrones y principios: diseño vs arquitectura; SOLID; inyección e inversión de dependencias; IoC.
- Patrones creacionales, estructurales y de comportamiento; técnicas basadas en componentes y dirigidas por datos; selección según requisitos no funcionales.
- Presentación y sistemas distribuidos: Broker, MVC, MVT, MVC + Observer; patrones cloud de despliegue y actualización.
- IA aplicada a patrones; tendencias: serverless, hexagonal, microservicios, distribuidas, IA, cloud, sostenibilidad y cuántica.
- Gobernanza: migración legacy; decisiones estratégicas/tácticas, esfuerzo y trade-offs; Zero Trust, Security by Design, IA para decisiones.
- Métricas: políticas, estándares, acoplamiento, cohesión, mantenibilidad, auditoría, riesgos detectados con IA; casos prácticos.

## Certificación 2 — Arquitectura Moderna y Diseño Evolutivo de Software (pp. 8–9)
- Clean Architecture: definición, regla de dependencia, capas, beneficios, adaptación, revisión de código, evaluación, tráfico, Threat Modeling, mínimo privilegio e IA para calidad.
- Puertos y adaptadores: concepto, cohesión, acoplamiento.
- Escalabilidad: vertical, horizontal, balanceador, arquitectura limpia escalable.
- Agilidad: proyectos ágiles, arquitectura evolutiva, DevOps, DevSecOps, GitOps.
- Diseño evolutivo: adaptabilidad, deuda técnica, limpieza ante cambios, Security by Design, Threat Modeling, IA.
- Arquitectura de soluciones: responsabilidades, principios, migración cloud, patrones y arquitectura cuántica.
- Capas: web, aplicación, base de datos; evolución a hexagonal, limpia y eventos.
- TDD: unitarias, integración, cobertura, falacia de cobertura, calidad, práctica.
- Soluciones: interfaces, virtualización, nube distribuida, móviles, rol y competencias de arquitectos, organización; retos.

## Certificación 3 — Modernización de Arquitecturas y Transformación Tecnológica (pp. 10–12)
- Introducción: definición, arquitectura más allá de tecnología, componentes modernos.
- Principios: límites de dominio, bajo acoplamiento, múltiples ámbitos, evolución como portafolio.
- Liderazgo: preparar organización, sistemas legacy, desafíos, fallas y costos, disposición a cambio e inversión, comunicación y justificación.
- Mentalidad: Ley de Conway, colaboración, estrategia corporativa, silos, IA para Wardley.
- Wardley Mapping: ciclo, creación, evolución, decisiones.
- Taxonomía de productos: componentes, diseño, oportunidades, riesgos; productos vs características/componentes/variantes/viajes.
- EventStorming: panorama, sesión, problemas, facilitación, IA para dominios y eventos.
- Modernización de productos: requisitos, modelo de dominio, procesos.
- Aspectos clave: portafolio TI, Team Topologies, acoplamiento, plataformas internas, ingeniería de datos, equipos habilitadores, roadmap, mejora, seguridad legacy, Backstage, IDP, DORA, ISO 27001, GDPR, SOC 2, DevEx.
- Indicadores: deuda técnica, velocidad, costos, seguimiento, IA predictiva; retos.

## Certificación 4 — Arquitectura de Microservicios y Sistemas Distribuidos (pp. 13–15)
- Monolitos: problemas (acoplamiento, abstracciones, aislamiento, efectos secundarios, despliegue, pruebas, tecnología, ciclo); beneficios (refactorización, migración, punto de partida, infraestructura); tipos clásico, distribuido, modular; Istio y SuperApps.
- Micro-frontends: transición, principios, arquitectura, desafíos.
- Microservicios: principios, comparación, descomposición, comunicación y patrones, buenas prácticas, cuándo usarlos.
- Descomposición: modularidad, beneficios, módulos funcionales/técnicos, capacidad empresarial, subdominio, bounded context DDD, evaluación.
- Asincronía: comunicación, ventajas, desafíos, programación reactiva, multithreading, Kafka, RabbitMQ, IA para eventos.
- Antipatrones: aislamiento, monolíticos, monolitos distribuidos, bibliotecas compartidas, microservicios.
- Métricas: latencia, escalabilidad, tolerancia a fallos, monitoreo.
- Observabilidad: métricas, logs, trazas, Prometheus, Grafana, OpenTelemetry; Circuit Breaker, Retry, Bulkhead, alta disponibilidad, IA para anomalías.
- Avanzados: Saga (orquestación/coreografía), CQRS, Event Sourcing, API Gateway, BFF; retos.

## Certificación 5 — Arquitecturas Cloud-Native y Estrategias Multinube Empresariales (pp. 16–19)
- Cuentas: Azure, AWS, Google Cloud y OCI.
- Multinube: razones, resiliencia, costos, interoperabilidad, gobernanza, seguridad; Terraform, Crossplane, Anthos.
- Contenedores: Docker, imágenes, registros, orquestadores, Kubernetes (arquitectura/componentes), Istio, modularidad.
- Implementación: Sidecar, Service Mesh, DevOps, CI/CD, DevSecOps, Blue-Green/Rolling/Canary, IaC, IA para pipelines, GitOps ArgoCD/Flux.
- Resiliencia y observabilidad: Retry, Circuit Breaker (estados), Bulkhead, logs y trazas, OpenTelemetry/Zipkin, Prometheus/Grafana, dashboards, IA.
- Serverless: microservicios sin servidor, AWS Lambda, mapeo AWS, eventos.
- Rendimiento: latencia, throughput, concurrencia, caché, IA; FinOps, tagging, rightsizing, Infracost, CloudHealth.
- Seguridad: autenticación/autorización, OAuth, JWT, APIs, RPO/RTO, Trivy, Clair, Sentinel, OPA, pruebas en CI/CD.
- Workloads: stateful/stateless, batch/real-time, compute/memory; Rehost/Replatform/Refactor/Rearchitect; EC2/ECS/Fargate, AKS/ACI/App Service, GKE/Cloud Run; placement.
- Gobierno: Azure Arc, AWS Outposts, Anthos, tagging, compliance, IDP y autoservicio.
- Redes: VPC Peering, Transit Gateway, ExpressRoute, Direct Connect, DNS híbrido, routing.
- Datos: distribución, replicación, S3/Blob/Cloud Storage.
- HA/DR: activo-activo, activo-pasivo, failover, backup, continuidad.
- Well-Architected: AWS (seis pilares), Azure y Google Cloud; comparación; retos.

## Certificación 6 — Inteligencia Artificial y AIOps para Arquitectura de Software (pp. 20–21)
- IA: débil, fuerte, generativa; predicción/prescripción, ética, gobernanza.
- Ciencia de datos: Big Data, feature engineering, supervisado/no supervisado/refuerzo.
- ML/DL: Transformers, CNN, RNN, AutoML, XAI.
- AIOps: operaciones híbridas/multinube, observabilidad, anomalías, fallos, recursos.
- IA generativa: modelos propietarios/abiertos, LLMs, RAG, bases vectoriales, embeddings, agentes, ReAct, Plan-and-Execute, MCP, AI Gateway, LLMOps, LLM-as-judge, prompt versioning, drift.
- Seguridad: PII masking, guardrails, políticas; IA para DevOps/MLOps, revisión, tests, incidentes.
- Futuro: multimodal, edge, automatización, computación cuántica y criptografía poscuántica; retos.

## Certificación 7 — Blockchain y Transformación Digital Descentralizada (p. 22)
- Blockchain: arquitectura, PoW/PoS/PoA, smart contracts, ERC-20/721/4973, seguridad, trazabilidad.
- Web3: wallets, DApps, DeFi, identidad y credenciales verificables, DAOs.
- Tokenización: NFT, Soulbound, activos físicos/financieros, regulación.
- Infraestructura: sidechains, Layer 2, interoperabilidad, IPFS, costos Ethereum/Polygon/BNB/Solana.
- Transformación: IA, IoT, sostenibilidad, automatización, banca, educación, supply chain.
- Tendencias: metaverso, regulación, economía digital; retos.

## Método de estudio
Por cada tema: 1) concepto explicado de básico a avanzado; 2) ejemplo Java/Spring/AWS cuando corresponda; 3) diagrama o código; 4) decisiones y trade-offs; 5) preguntas tipo entrevista; 6) reto práctico; 7) resumen ColorNote. Marcar progreso en este documento a medida que avancemos.

## Progreso
- [ ] Certificación 1
- [ ] Certificación 2
- [ ] Certificación 3
- [ ] Certificación 4
- [ ] Certificación 5
- [ ] Certificación 6
- [ ] Certificación 7

**Próxima lección:** Certificación 1 → Introducción y contexto → Contextualización de la arquitectura de software.
