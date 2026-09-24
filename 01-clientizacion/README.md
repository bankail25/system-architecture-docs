# Clientizacion

**Propósito del Proyecto**

Diseñar e implementar un servicio automatizado y continuo para consultar, cruzar y enriquecer la información de tickets de soporte entre dos plataformas críticas: **ElasticSearch** y **BMC Remedy (SOAP)**. El objetivo principal es suprimir la revisión y llenado manual de incidencias, procesando la carga de trabajo en segundo plano para cumplir rigurosamente con los acuerdos de servicio y liberar el tiempo del equipo operativo.

#### Problema que Resuelve

- **Eliminación de penalizaciones por SLA:** Se incrementó la tasa de optimización operativa del **75% al 98%**, logrando erradicar por completo (**0%**) las penalizaciones por retraso en el servicio.
- **Cuello de botella en la operación:** Antes, validar y enriquecer cada ticket tomaba 1 hora o más de forma manual; con el flujo automático, el volumen diario de **10 a 100 tickets** se procesa de forma ágil e inmediata.
- **Notificación oportuna de anomalías:** Resuelve la incertidumbre ante datos incompletos mediante alertas en tiempo real, evitando que los tickets queden estancados sin supervisión.

#### Stack Tecnológico

- **Python:** Lenguaje base para la orquestación del flujo, validación de reglas de negocio y ejecución concurrente.
- **`requests` / Integración SOAP:** Consumo de servicios web SOAP de BMC Remedy y consultas directas a los endpoints de ElasticSearch.
- **`python-dotenv` (`load_dotenv`):** Administración segura de credenciales, tokens y variables de entorno del sistema.
- **Docker:** Contenedorización de la solución para garantizar un despliegue aislado, ligero y portable.
- **Cron / Scheduler en Python:** Programación de tareas periódicas que evalúan el estado de los tickets recurrentemente.
- **Telegram Bot API:** Canal de comunicación inmediata para enviar alertas al equipo operativo si un ticket no cumple con los datos requeridos.

#### Alcance y Funcionalidades Clave

- **Procesamiento y enriquecimiento simultáneo:** Inspección recurrente que analiza múltiples tickets al mismo tiempo, actualizando Remedy únicamente cuando ElasticSearch confirma la información completa.
- **Monitoreo automatizado en contenedor:** Ejecución constante y desatendida mediante tareas programadas internas (`cronjob` en Python) dentro de un entorno Dockerizado.
- **Sistema de alertas por Telegram:** Si los datos en las plataformas de origen vienen incompletos o inconsistentes, el sistema emite una notificación instantánea al equipo de soporte con el ID del ticket para su revisión puntual.