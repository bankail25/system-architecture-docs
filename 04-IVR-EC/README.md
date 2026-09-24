# **Automatización ETL y Enriquecimiento de Incidencias: IVR-EC**

**Propósito del Proyecto**
Diseñar e implementar un flujo automatizado de extracción, transformación y carga (ETL) que monitoree de forma periódica las incidencias en BMC Remedy y cruce datos con la plataforma Elasticsearch para enriquecer registros incompletos. El sistema flexibiliza la aplicación de reglas de negocio al desacoplarlas de usuarios individuales mediante una base de datos dinámica, ofreciendo visibilidad y control inmediato al equipo a través de notificaciones automáticas.
****

**Problema que Resuelve**

• **Sustitución de mecanismos rígidos:** Reemplaza un agente externo que carecía de la flexibilidad para incorporar nuevas reglas de negocio según las necesidades de la operación.   
• **Liberación de carga operativa:** Suprime la intervención manual en tareas rutinarias y repetitivas de búsqueda, validación y captura de datos, procesando un volumen estimado de **50 tickets diarios**.   
• **Incremento sustancial de KPIs:** La tasa de cumplimiento y optimización del servicio aumentó del **75% al 90%**, reduciendo notablemente las penalizaciones operativas.   
• **Gobernanza y trazabilidad:** Permite ajustar criterios de búsqueda y validación directamente en base de datos sin depender de cuentas personales, informando al equipo en tiempo real sobre cada ticket actualizado.
****

**Stack Tecnológico**

• **Python:** Lenguaje principal para la lógica del ETL, validación de reglas y orquestación de tareas.   
• **APScheduler:** Programador interno de tareas recurrentes para ejecutar las consultas de forma periódica y desatendida.   
• **Requests:** Cliente HTTP para la comunicación con los servicios SOAP de Remedy y la API de Elasticsearch.   
• **Pydantic:** Modelado riguroso, tipado y validación de esquemas de datos.   
• **Pandas:** Procesamiento, limpieza y estructuración tabular de la información extraída.   
• **Prisma (Python Client) & MongoDB:** Capa de acceso y base de datos de persistencia dinámica donde se gestionan los parámetros y reglas de negocio.   
• **Poetry:** Gestión moderna de dependencias y empaquetado del entorno.   
• **Docker:** Contenedorización de la solución para un despliegue aislado, ligero y portable en producción.   
• **Telegram Bot API:** Canal de mensajería instantánea para reportar y auditar cada ticket actualizado.

**Alcance y Funcionalidades Clave**

• **Monitoreo programado vía SOAP:** Consulta periódica a BMC Remedy configurada a través de APScheduler para filtrar tickets candidatos basados en queries dinámicos.   
• **Cruce y enriquecimiento con Elasticsearch:** Búsqueda automatizada de los datos faltantes en Elastic y posterior actualización directa sobre la incidencia en Remedy.   
• **Administración desacoplada de reglas:** Configuración dinámica de criterios y parámetros almacenados en MongoDB, permitiendo dar de alta o baja reglas operativas sin anclarse a un usuario específico.   
• **Despliegue contenerizado:** Ejecución continua dentro de un contenedor Docker que asegura estabilidad y portabilidad del entorno ETL.   
• **Alertas y control por Telegram:** Emisión automática de notificaciones cada vez que un ticket es enriquecido, garantizando visibilidad inmediata y auditoría para el equipo.