# Automatización y Web Scraping Operativo: IVRPBX

#### Propósito del Proyecto

Diseñar e implementar un bot autónomo de extracción web y enriquecimiento de datos para gestionar de punta a punta tickets e incidencias operativas en plataformas sin interfaces de programación disponibles (APIs o SOAP). El sistema resuelve la falta de conectividad directa extrayendo la información mediante técnicas de scraping, cruzando datos con Elasticsearch para completar los registros, actualizando estados, ejecutando cierres y notificando a los usuarios vía Telegram de forma automática y desatendida.

#### Problema que Resuelve

- **Eliminación de la sobrecarga operativa manual:** Antes, un operador tardaba entre 30 y 40 minutos en validar un solo ticket, obligando a asignar a varios integrantes del equipo a consultar la plataforma cada 15 minutos para detectar casos desatendidos.
- **Procesamiento continuo y ágil:** Atiende de forma desatendida entre **30 y 50 tickets diarios**, liberando tiempo operativo valioso para el equipo.
- **Salto drástico en KPIs y cero penalizaciones:** La tasa de cumplimiento y eficiencia operativa pasó de un **60% a un 95%**, eliminando por completo las penalizaciones por demoras en la atención.
- **Superación de barreras técnicas de integración:** Resolvió la imposibilidad de conectar sistemas legacy al no existir APIs o servicios SOAP oficiales, implementando un mecanismo de scraping robusto y sanitizado que salvaguarda la integridad de los datos inyectados.
- **Hito de innovación interna:** Sentó un precedente técnico en la organización sobre la viabilidad de automatizar procesos restrictivos, marcando el inicio y liderazgo de una serie de nuevos proyectos de automatización.

#### Stack Tecnológico

- **Python:** Lenguaje principal utilizado para la lógica de scraping, transformaciones de negocio y orquestación del ciclo de vida del ticket.
- **APScheduler:** Programador interno de tareas recurrentes para ejecutar las inspecciones periódicas a intervalos definidos.
- **Requests:** Manejo de sesiones HTTP simuladas, gestión de cookies/headers y envío de payloads para consultar y actualizar la plataforma sin API formal.
- **Regex (re):** Motor de parseo y extracción de patrones de texto para aislar identificadores, datos clave y estados incrustados en las respuestas HTML.
- **Telegram Bot API:** Canal de mensajería instantánea para emitir alertas y notificar a los usuarios sobre el estatus de sus tickets.
- **Docker:** Contenedorización del entorno de ejecución para asegurar estabilidad, aislamiento y portabilidad continua en producción.
- **Elasticsearch (Elastic):** Fuente externa consultada para cruzar y enriquecer la información faltante de cada incidencia.

#### Alcance y Funcionalidades Clave

- **Inspección y Web Scraping Programado:** Consulta automatizada gestionada mediante APScheduler para identificar tickets desatendidos directamente sobre la plataforma web.
- **Cruce y Enriquecimiento con Elasticsearch:** Búsqueda complementaria de datos en Elastic para nutrir la incidencia antes de tomar acciones de actualización.
- **Gestión del Ciclo de Vida del Ticket:** Capacidad programática de cambiar estados, registrar información enriquecida y cerrar tickets de forma segura.
- **Alertas y Notificaciones en Telegram:** Envío automático de notificaciones a través de Telegram para mantener informados a los usuarios sobre la atención y resolución de sus casos.
- **Sanitización y Validación de Datos:** Filtros y validaciones rigurosas para asegurar que las peticiones simuladas preserven la consistencia de la base de datos de la plataforma destino.
- **Despliegue Contenerizado:** Entorno empaquetado en Docker listo para ejecutarse de forma continua, aislada y sin dependencias externas del host.