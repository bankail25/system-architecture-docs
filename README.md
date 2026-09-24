# Documentación de Arquitectura de Sistemas y Automatizaciones

Repositorio centralizado con la documentación técnica, arquitectónica y operativa de los desarrollos, flujos ETL, bots conversacionales y servicios concurrentes diseñados para la optimización de procesos de soporte, mesa de ayuda (BMC Remedy), ingesta y monitoreo analítico (Elasticsearch).

---

## 📊 Tabla Resumen de Proyectos

| Módulo | Nombre del Proyecto | Propósito Principal | Stack Tecnológico Clave |
| :--- | :--- | :--- | :--- |
| **01** | [Clientización](./01-clientizacion) | Cruce y enriquecimiento automático de tickets entre ElasticSearch y BMC Remedy. | Python, SOAP, Docker, Telegram Bot API |
| **02** | [Inicio-Fin-CRQ](./02-inicio-fin-crq) | Autoservicio conversacional en Telegram para el ciclo de vida de órdenes CRQ en Remedy. | Node.js, TypeScript (grammY), Python, PostgreSQL, SOAP |
| **03** | [DashIVR](./03-DashIVR) | SPA para monitoreo en tiempo real, asignación de alarmas y enriquecimiento en Remedy. | React, Vite, MUI, TanStack Query, NestJS, Python, PostgreSQL, Elastic |
| **04** | [IVR-EC](./04-IVR-EC) | Pipeline ETL desacoplado con reglas dinámicas para enriquecimiento de incidencias. | Python, APScheduler, Pandas, Pydantic, MongoDB, Prisma, Docker |
| **05** | [Reporte Folios](./05-reporte-folios) | Validación masiva y concurrente de matrices Excel (.xlsx) vía bot de Telegram hacia CSV. | Python, ThreadPoolExecutor, Pandas, Pydantic, SOAP, Elastic, Docker |
| **06** | [Ingesta Concurrente Alarmas](./06-ingesta-concurrente-alarmas) | Microservicio concurrente de alta velocidad para ingesta SOAP y persistencia dual. | Go (Golang, Worker Pool), PostgreSQL, MongoDB, gocron |
| **08** | [Notificación App](./08-Notificacion-app) | Bot de consulta acelerada y trazabilidad de tickets en Elasticsearch con parseo flexible. | Go (Golang, Worker Pool), Telegram API, go-elasticsearch, Docker |
| **09** | [Web Scraping Operativo IVRPBX](./09-WebScraping-operativo-ivrpbx) | Automatización y scraping para gestión y cierre de tickets en plataformas legacy sin API. | Python, APScheduler, Requests (Session/Cookies), Regex, Telegram API, Elastic |

---

## 🛠️ Resumen Detallado por Módulo

### 1. [Clientización](./01-clientizacion)
- **Propósito:** Servicio automatizado en segundo plano para consultar, cruzar y enriquecer tickets entre Elasticsearch y BMC Remedy (SOAP), eliminando la captura manual.
- **Impacto y Resultados:** 
  - Cumplimiento operativo incrementado del **75% al 98%**, logrando **0% de penalizaciones por SLA**.
  - Procesamiento ágil de **10 a 100 tickets diarios** (reduciendo el tiempo por ticket de más de 1 hora a procesamiento inmediato).
- **Stack:** Python, `requests` (SOAP), `python-dotenv`, Docker, Telegram Bot API.

### 2. [Inicio-Fin-CRQ](./02-inicio-fin-crq)
- **Propósito:** Bot conversacional de autoservicio que permite a los usuarios gestionar el ciclo de vida de órdenes de cambio (CRQ) en Remedy (iniciar, enriquecer, cerrar) de forma autónoma y con control de accesos.
- **Impacto y Resultados:**
  - Atención desatendida de **20 a 50 solicitudes diarias**.
  - Incremento en el cumplimiento de metas operativas del **60% al 90%**, liberando a los operadores de tareas mecánicas.
- **Stack:** Node.js, TypeScript (grammY), Python, PostgreSQL, SOAP XML, ELK Stack, Docker.

### 3. [DashIVR](./03-DashIVR)
- **Propósito:** Plataforma web SPA para centralizar, visualizar y asignar en tiempo real las alarmas de Elasticsearch a operadores activos, detonando el enriquecimiento automático del ticket en Remedy.
- **Impacto y Resultados:**
  - Erradicación de alarmas extraviadas con un **incremento del 40% en positividad y productividad**.
  - Asignación inteligente validando disponibilidad del operador en tiempo real.
- **Stack:** React, Vite, Material UI, TanStack Query, Redux, NestJS, Python (Worker SOAP), PostgreSQL, Elasticsearch.

### 4. [IVR-EC](./04-IVR-EC)
- **Propósito:** Flujo ETL programado para monitorear incidencias en Remedy y cruzarlas con Elasticsearch, administrando reglas de negocio dinámicas desacopladas en base de datos documental.
- **Impacto y Resultados:**
  - Sustitución de agentes rígidos y procesamiento desatendido de ~**50 tickets diarios**.
  - Aumento de KPIs del **75% al 90%** con trazabilidad y notificaciones en tiempo real por Telegram.
- **Stack:** Python, APScheduler, Requests, Pydantic, Pandas, Prisma Client, MongoDB, Poetry, Docker, Telegram Bot API.

### 5. [Reporte Folios](./05-reporte-folios)
- **Propósito:** Bot interactivo para procesar matrices de folios en Excel (.xlsx), validando simultáneamente el estado de cierre y consistencia en Remedy y Elasticsearch con entrega de un consolidado en CSV.
- **Impacto y Resultados:**
  - Eliminación de 2 horas diarias de validación manual folio por folio para lotes de **100 a 150 tickets**.
  - Incremento del cumplimiento operativo del **60% al 95%**.
- **Stack:** Python, `python-telegram-bot`, `concurrent.futures` (ThreadPoolExecutor), Pandas, Pydantic, SOAP Remedy, Elasticsearch, Docker.

### 6. [Ingesta Concurrente y Enriquecimiento de Alarmas](./06-ingesta-concurrente-alarmas)
- **Propósito:** Microservicio de alta concurrencia en Go para la extracción de información complementaria en BMC Remedy (SOAP) y enriquecimiento de alarmas en Elasticsearch con arquitectura multi-salto de red.
- **Impacto y Resultados:**
  - Manejo continuo de **50 a 100 alarmas diarias** mediante patrón *Worker Pool*.
  - Doble persistencia segura: transaccional en PostgreSQL (cliente) y réplica documental en MongoDB.
- **Stack:** Go (Golang, goroutines/channels), PostgreSQL (`pq`), MongoDB (`mongo-driver`), `gocron`, `godotenv`.

### 7. [Notificación App](./08-Notificacion-app)
- **Propósito:** Bot en Go de alta eficiencia para la consulta concurrente de tickets y extracción de trazabilidad histórica en Elasticsearch mediante lenguaje natural o listas de folios en texto libre.
- **Impacto y Resultados:**
  - Reducción de tiempos de consulta de **15 minutos a pocos segundos**.
  - Aumento de eficiencia operativa del **70% al 95%** soportando **30 a 40 consultas diarias por usuario**.
- **Stack:** Go (Golang), Worker Pool (`sync.WaitGroup`), Regex, `telegram-bot-api`, `go-elasticsearch`, Docker.

### 8. [Web Scraping Operativo: IVRPBX](./09-WebScraping-operativo-ivrpbx)
- **Propósito:** Bot autónomo de extracción web y enriquecimiento para plataformas legacy sin APIs o servicios SOAP, ejecutando validación, actualización de estados, cierres y alertas automáticas.
- **Impacto y Resultados:**
  - Reducción del tiempo de validación por ticket de 30-40 minutos a atención desatendida (**30 a 50 tickets diarios**).
  - Salto en eficiencia del **60% al 95%** y erradicación total de penalizaciones.
- **Stack:** Python, APScheduler, Requests (Session/Cookies), Regex, Telegram Bot API, Elasticsearch, Docker.

---

## 🏛️ Patrones Arquitectónicos y Ecosistema Común

1. **Integración con BMC Remedy & Elasticsearch:** Puentes de comunicación bidireccional entre la mesa de ayuda transaccional (SOAP) y el repositorio analítico/operativo (Elasticsearch).
2. **Concurrencia y Rendimiento:** Implementación de modelos concurrentes (Goroutines en Go, ThreadPoolExecutor y APScheduler en Python) para mitigar cuellos de botella e interactuar eficientemente con sistemas externos.
3. **Interfaces Desacopladas y Ágiles:** Uso extendido de bots de **Telegram** para interacción y alertas en tiempo real, junto con aplicaciones web modernas (**React/NestJS**) para visualización de métricas y asignación de alarmas.
4. **Contenedorización y Portabilidad:** Empaquetado en **Docker** en los diferentes módulos para garantizar despliegues estables, aislados y reproducibles.
