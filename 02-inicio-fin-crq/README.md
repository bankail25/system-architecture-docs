# Automatización de Ciclo de Vida de Tickets: INICIO-FIN-CRQ

#### Propósito del Proyecto

Diseñar una solución de autoservicio para gestionar de punta a punta las órdenes de trabajo (CRQ) en BMC Remedy —iniciarlas, enriquecerlas y cerrarlas— a través de un canal conversacional ágil y accesible. El sistema elimina la dependencia del contacto manual con los operadores de soporte, permitiendo que los usuarios tramiten sus solicitudes de forma autónoma, segura y en pocos pasos.

#### Problema que Resuelve

- **Saturación operativa y cuellos de botella:** Antes, pocos operadores atendían manualmente a un número significativo de usuarios concurrentes; la solución procesa de forma desatendida entre **20 y 50 solicitudes diarias**.
- **Mejora drástica en KPIs y SLAs:** El cumplimiento de metas operativas pasó del **60% al 90%**, reduciendo considerablemente las penalizaciones por demoras en la atención de tickets.
- **Optimización del tiempo operativo:** Al delegar las tareas mecánicas de gestión de CRQs en el bot, los operadores quedaron libres para resolver incidencias complejas y de alta urgencia.
- **Seguridad y gobernanza en las actividades:** Previene errores y accesos indebidos al garantizar que únicamente el usuario asignado a la orden pueda iniciar o modificar sus etapas correspondientes.

#### Stack Tecnológico

- **Node.js & TypeScript (grammY):** Construcción del bot de Telegram, diseño de flujos conversacionales guiados y procesamiento de comandos.
- **Python:** Backend principal para la orquestación de la lógica de negocio, validaciones y reglas de control.
- **PostgreSQL:** Base de datos para almacenar el mapeo de identidades (ID de Telegram vinculado al usuario) y registrar el estado de las transacciones.
- **Requests & xml.etree.ElementTree:** Módulos para la construcción, consumo y parseo de peticiones SOAP XML hacia la API de BMC Remedy.
- **ELK Stack (Elasticsearch, Logstash, Kibana):** Registro centralizado de logs, auditoría de eventos y monitoreo de la interacción del bot.
- **Docker:** Contenedorización de la solución para garantizar despliegues modulares, reproducibles y aislados.

#### Alcance y Funcionalidades Clave

- **Autoservicio conversacional en Telegram:** Permite a los usuarios iniciar, complementar y cerrar sus órdenes de trabajo mediante comandos sencillos y rápidos.
- **Control de acceso y alta controlada:** Registro previo del ID de Telegram del usuario en base de datos, validado y activado manualmente por los administradores antes de conceder permisos de interacción.
- **Motor de reglas de negocio y pertenencia:** Evaluación previa de los requisitos del ticket en Remedy y verificación estricta de que el solicitante sea el propietario real de la actividad antes de permitir cualquier cambio de estado.
- **Integración SOAP en tiempo real:** Comunicación directa con BMC Remedy para reflejar de forma inmediata el inicio, enriquecimiento y cierre de cada CRQ.