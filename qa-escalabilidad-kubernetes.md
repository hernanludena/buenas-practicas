# QA, escalabilidad y plataforma

Recordatorio de calidad, escalado, tráfico y despliegue. Separa herramientas, roles y estado real del laboratorio.

| Bloque | Nombre | Descripción breve |
|---|---|---|
| QA | Pirámide de pruebas | Cubrir reglas con unitarias, integraciones reales en límites y pocos flujos E2E de usuario. |
| QA | Testcontainers | Levantar PostgreSQL/Kafka desechables para probar integraciones sin depender de servicios compartidos. |
| QA | Playwright / Selenium | Automatizar flujos UI en navegador; complementan, no reemplazan, pruebas de integración del backend. |
| QA | Contratos API/eventos | Verificar OpenAPI, esquemas Avro y compatibilidad para detectar cambios incompatibles antes del despliegue. |
| QA | Calidad en CI | Ejecutar compilación, pruebas, análisis estático/seguridad y cobertura como gates del merge. |
| QA | Cobertura | Usarla como señal junto con escenarios y aserciones; aplicar umbrales según fase y módulos críticos. |
| QA | Escenarios de fallo | Probar timeout, duplicados, reintentos, retornos, caída de proveedor/broker y recuperación/replay. |
| QA | Telemetría como aceptación | Acordar logs, métricas, trazas, alertas y correlación necesarias para operar cada flujo. |
| QA | Privacidad de telemetría | No registrar secretos, tokens ni datos financieros/personales; limitar y proteger analítica de usuario. |
| GitLab CI | CI vs CD | CI compila, prueba y publica artefactos/imágenes; CD actualiza el entorno según estrategia acordada. |
| GitLab CI | Pipeline del laboratorio | El pipeline revisado ejecuta Gradle verify y pruebas; construye/publica imágenes del commit en la rama principal. |
| GitLab CI | Merge Request | Revisar diffs y reportes; usar approvals/ownership gates cuando el riesgo o el dominio lo requiera. |
| GitOps | Argo CD | Compara Git con el cluster y reconcilia el estado deseado; el pipeline actualiza Git, no necesita aplicar kubectl directamente. |
| GitOps | Repositorio de despliegue | Separar manifiestos de runtime del código de aplicación; proteger credenciales y cambios de producción. |
| Kubernetes | Pod / Deployment / ReplicaSet | Pod ejecuta contenedores; Deployment mantiene réplicas y actualiza versiones mediante ReplicaSets. |
| Kubernetes | StatefulSet | Gestiona Pods con identidad/almacenamiento estable; útil para ciertos sistemas stateful, no automáticamente para cada base de datos. |
| Kubernetes | Service | Da una dirección estable y distribuye tráfico entre Pods listos que coinciden con el selector. |
| Kubernetes | Probes | Readiness decide si el Pod recibe tráfico; liveness detecta procesos que deben reiniciarse. |
| Kubernetes | Requests / limits | Requests ayudan a scheduling y cálculo de uso; limits restringen consumo. Definirlos para workloads previsibles. |
| Kubernetes | HPA | Ajusta réplicas de Pods con métricas como CPU/memoria o métricas externas; requiere métricas y requests válidos. |
| Kubernetes | Cluster Autoscaler | Ajusta nodos del clúster cuando falta capacidad; HPA escala Pods. Son capas diferentes. |
| Kubernetes | KEDA | Puede escalar workloads por métricas/eventos como longitud de cola; añadirlo solo si ese patrón se necesita. |
| Tráfico | Ingress | Recurso de entrada HTTP(S); requiere un Ingress Controller instalado. La API Ingress está congelada, no eliminada. |
| Tráfico | Gateway API | API de tráfico más expresiva; GatewayClass define controlador, Gateway recibe tráfico y HTTPRoute/GatewayRoute configura rutas. |
| Tráfico | Ingress NGINX comunitario | Proyecto retirado el 24-mar-2026; no confundirlo con F5 NGINX Ingress Controller, proyecto separado. |
| Tráfico | NGINX reverse proxy | Recibe solicitudes y las reenvía a upstreams; puede balancear tráfico, terminar TLS y aplicar caché según configuración. |
| Tráfico | Istio / Envoy | Service mesh para políticas entre servicios, mTLS, retries y observabilidad; no reemplaza automáticamente un API Gateway. |
| Tráfico | Gateway vs API Gateway | Gateway de Kubernetes enruta tráfico al cluster; API Gateway también gestiona políticas de API como auth, cuotas y rate limits. |
| Argo | Argo Rollouts | Controlador con CRD Rollout para canary/blue-green, pausas, análisis de métricas y promoción/rollback gradual. |
| Argo | Rollout vs Deployment | Rollout puede reemplazar el Deployment de esa app cuando se necesita progressive delivery; no es un reemplazo universal ni funciona sin su controlador. |
| Config | Kustomize | Combina un base común con overlays por entorno (staging/production), manteniendo YAML sin plantillas textuales. |
| Config | Helm | Empaqueta charts y plantillas con values por entorno; herramienta distinta a Kustomize. No asumir que el laboratorio ya lo usa. |
| Kubernetes | CRD | Custom Resource Definition añade un tipo nuevo a la API; también se necesita el controller que lo reconcilia. |
| Estado actual | Playground revisado | Compose es el runtime activo; existen manifiestos Kustomize y un ejemplo Rollout, pero no se confirmó Kubernetes/Argo CD desplegado. |
| Despliegue | GitOps del Playground | La integración con repo GitOps y Argo CD quedó como trabajo futuro; no describirlo como despliegue activo. |

## Flujo de tráfico para recordar

| Capa | Responsabilidad |
|---|---|
| DNS/CDN/WAF | Encuentra el punto de entrada y, si aplica, cachea/protege tráfico externo. |
| Load balancer / Gateway / Ingress Controller | Recibe y enruta tráfico norte-sur al servicio apropiado. |
| Service | Distribuye dentro del cluster entre Pods listos. |
| HPA / autoscaling de nodos | Aumenta réplicas de aplicación y, por separado, capacidad de nodos. |
| Istio | Puede gestionar tráfico este-oeste entre servicios y políticas del mesh. |

## Referencias

- [Kubernetes HPA](https://kubernetes.io/docs/concepts/workloads/autoscaling/horizontal-pod-autoscale/)
- [Kubernetes Ingress y Gateway API](https://kubernetes.io/docs/concepts/services-networking/gateway/)
- [Retiro de Ingress NGINX comunitario](https://kubernetes.io/blog/2025/11/11/ingress-nginx-retirement/)
- [F5 NGINX Ingress Controller](https://docs.nginx.com/nginx-ingress-controller/)
- [Argo CD](https://argo-cd.readthedocs.io/en/stable/)
- [Argo Rollouts](https://argoproj.github.io/argo-rollouts/)
- [Kustomize](https://kubernetes.io/docs/tasks/manage-kubernetes-objects/kustomization/)
