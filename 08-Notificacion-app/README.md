# Automatización y Consulta Concurrente: Notificación App

#### Propósito del Proyecto

Diseñar e implementar un bot interactivo de alto rendimiento en Telegram desarrollado en Go, orientado a la consulta concurrente y acelerada de tickets y su trazabilidad histórica en Elasticsearch. La herramienta permite a los operadores validar incidencias de manera inmediata mediante mensajes en lenguaje natural o listas de folios sin restricciones de formato, erradicando los prolongados tiempos de espera de las consolas analíticas tradicionales y evitando penalizaciones por demoras en los tiempos de respuesta.

#### Problema que Resuelve

- **Reducción drástica de tiempos de espera:** Supera la lentitud de las búsquedas previas en Elasticsearch, las cuales tardaban 15 minutos o más por consulta, entregando ahora la información y trazabilidad del ticket en segundos.
- **Aumento notable de KPIs y erradicación de penalizaciones:** Elevó la tasa de eficiencia operativa del **70% al 95%**, cumpliendo con los estándares de servicio requeridos y previniendo multas operativas.
- **Optimización del flujo de trabajo del operador:** Soporta de forma ágil y paralela la carga de **30 a 40 consultas diarias por usuario**, liberando tiempo de análisis para la toma de decisiones.
- **Extracción flexible y no restrictiva:** Resuelve la rigidez en la captura de folios; el usuario puede ingresar texto libre o múltiples identificadores en un mismo mensaje sin preocuparse por un formato estricto.
- **Control eficiente de la carga del servidor:** Mitiga el riesgo de sobrecarga o caídas en el clúster de búsqueda ante peticiones masivas, gracias a la limitación estructurada de concurrencia.

#### Stack Tecnológico

- **Go (Golang):** Lenguaje principal seleccionado por su eficiencia en memoria, velocidad de ejecución nativa y manejo ligero de concurrencia mediante goroutines.
- **Patrón de Concurrencia (Worker Pool con `sync.WaitGroup`):** Modelo de arquitectura interna para orquestar y controlar el número de búsquedas simultáneas sin saturar los recursos del clúster.
- **Regex (Expresiones Regulares):** Motor de parseo flexible para identificar y extraer folios válidos a partir de cualquier formato de texto ingresado por el usuario.
- **telegram-bot-api:** Biblioteca para gestionar la interacción conversacional, captura de comandos y envío de trazabilidades a los operadores.
- **go-elasticsearch:** Cliente oficial de Go optimizado para estructurar y ejecutar consultas rápidas contra los índices de Elasticsearch.
- **Docker:** Contenedorización de la solución para garantizar despliegues aislados, consistentes y de fácil portabilidad.
- **Integraciones y Roadmap (SOAP Remedy & Modelos IA):** Ecosistema planificado para cruzar datos con los servicios SOAP de Remedy e incorporar interfaces de lenguaje natural (Text-to-Elasticsearch Query).

#### Alcance y Funcionalidades Clave

- **Parseo flexible mediante Regex:** Capacidad de recibir cadenas de texto libre en el chat de Telegram, identificando y extrayendo de forma no restrictiva uno o múltiples folios.
- **Worker Pool controlado (`sync.WaitGroup`):** Distribución balanceada de las consultas en Elasticsearch a través de un grupo controlado de workers en Go, garantizando paralelismo seguro y recolección sincronizada de los resultados.
- **Extracción y entrega de trazabilidad:** Consulta acelerada que devuelve el estado, historial y trazabilidad completa de cada ticket solicitado para su validación operativa inmediata.
- **Despliegue contenerizado:** Empaquetado ligero en Docker listo para correr de forma ininterrumpida y desacoplada del entorno local.
- **Visión de evolución (IA & Enriquecimiento):** Proyección arquitectónica para conectar directamente con BMC Remedy vía SOAP e integrar un modelo de IA capaz de traducir solicitudes en lenguaje natural a JSONs nativos de Elasticsearch (DSL).