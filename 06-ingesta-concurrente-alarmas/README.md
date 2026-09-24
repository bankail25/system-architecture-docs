# Automatización BTP: Ingesta Concurrente y Enriquecimiento de Alarmas

#### Propósito del Proyecto

Diseñar e implementar un bot de alta concurrencia en Go para extraer información complementaria desde BMC Remedy (vía SOAP) y enriquecer las alarmas monitoreadas en Elasticsearch. El servicio actúa como un puente desacoplado y seguro que enruta los datos a través de una arquitectura multi-salto hacia PostgreSQL (origen para los procesos del cliente) y genera paralelamente un respaldo histórico en MongoDB, permitiendo que otros bots y servicios downstream consuman alarmas con contexto completo sin sobrecargar los sistemas primarios.

#### Problema que Resuelve

- **Incompletitud en alarmas críticas:** Corrige la falta de datos operativos en Elasticsearch, donde las alertas llegaban escuetas y requerían intervención manual para entender el contexto de Remedy.
- **Procesamiento ágil y concurrente:** Gestiona un volumen continuo de **50 a 100 alarmas diarias** mediante un patrón de *worker pool*, evitando tiempos de espera y bloqueos durante la extracción SOAP.
- **Resolución proactiva a nivel operativo:** Detecta y mitiga internamente una necesidad crítica del equipo de soporte antes de que impactara la percepción del servicio o generara inconformidades directas con el cliente.
- **Aislamiento y resiliencia de red:** Resuelve el reto de infraestructura de salvar dos saltos de red hacia el servidor de base de datos del cliente, asegurando la entrega en PostgreSQL y manteniendo una copia de respaldo en MongoDB.

#### Stack Tecnológico

- **Go (Golang):** Lenguaje base de alto rendimiento, implementando concurrencia nativa (*worker pool* con goroutines y channels) para la ingesta paralela sin saturar el endpoint SOAP.
- **PostgreSQL (driver `pq`):** Base de datos principal del cliente donde se depositan los datos procesados, alcanzada mediante saltos intermedios de red para el consumo de bots downstream.
- **MongoDB (driver `mongo-driver`):** Repositorio no relacional utilizado como respaldo (*backup*) histórico y persistencia de seguridad ante fallos de conexión externa.
- **gocron:** Programador en segundo plano para orquestar la periodicidad de las ejecuciones sin depender de cronjobs a nivel sistema operativo.
- **godotenv:** Administración centralizada y segura de credenciales, rutas de red y variables de entorno.
- **SOAP Remedy & Elasticsearch:** Plataformas origen y destino del flujo de supervisión de eventos.

#### Alcance y Funcionalidades Clave

- **Worker Pool Concurrente:** Distribución eficiente de las solicitudes de consulta SOAP en múltiples workers paralelos para agilizar el enriquecimiento de 50 a 100 registros al día.
- **Doble Persistencia (Transaccional + Backup):** Flujo de inserción dual que alimenta la base de datos PostgreSQL del cliente a través de dos saltos de servidor y asegura una réplica documental en MongoDB.
- **Desacoplamiento entre Bots:** Deja la información preprocesada y lista en la base de datos para que bots downstream la tomen y alimenten Elasticsearch sin consultar Remedy de manera redundante.
- **Orquestación Desatendida:** Ejecución automatizada mediante intervalos continuos configurados con `gocron` para mantener el flujo operativo al día.