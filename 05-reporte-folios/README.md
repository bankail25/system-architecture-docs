# Automatización y Validación Masiva: Reporte Folios

#### Propósito del Proyecto

Diseñar e implementar una solución de automatización conversacional que permita a los operadores cargar una matriz de identificadores de tickets de BMC Remedy en formato Excel (.xlsx) para cotejarlos de forma masiva y simultánea contra Elasticsearch. A través de un bot de Telegram, el sistema valida el estado de conclusión y la consistencia de los datos de cada incidencia, devolviendo de inmediato un consolidado descargable en formato CSV para agilizar la toma de decisiones y el control operativo.

#### Problema que Resuelve

- **Eliminación del trabajo manual rutinario:** Sustituye la consulta manual folio por folio en la que un operador invertía cerca de 2 horas al día para revisar entre 100 y 150 tickets.
- **Incremento sustancial en eficiencia y KPIs:** Elevó el cumplimiento operativo del 60% a cerca del 95%, acelerando la entrega de resultados y reduciendo de forma crítica la latencia operativa.
- **Liberación de carga de trabajo:** Descarga al personal de tareas repetitivas y de bajo valor analítico, permitiéndoles concentrarse en actividades de soporte técnico o gestión de mayor prioridad.
- **Procesamiento paralelo sin errores humanos:** Mitiga los riesgos de omisión o inconsistencia en la validación manual gracias a la ejecución simultánea y estructurada entre Remedy y Elastic.

#### Stack Tecnológico

- **Python:** Lenguaje central para la lógica de negocio, manipulación de archivos y control del flujo de ejecución.
- **python-telegram-bot:** Framework para la construcción del bot interactivo, recepción de archivos y entrega de reportes.
- **concurrent.futures (ThreadPoolExecutor):** Orquestación de concurrencia y múltiples hilos para consultar y validar simultáneamente grandes volúmenes de folios sin degradar el rendimiento.
- **Pandas:** Lectura, transformación y cruce de datos de la matriz de entrada (.xlsx) y generación estructurada del archivo de salida (.csv).
- **Requests / SOAP Remedy:** Cliente HTTP para la comunicación y consulta de datos contra los servicios web SOAP de BMC Remedy.
- **Elasticsearch API:** Consumo de endpoints analíticos para corroborar el estado de conclusión y la completitud de la información de cada ticket.
- **Pydantic:** Modelado riguroso, tipado y sanitización de los esquemas de datos entrantes y salientes.
- **Docker:** Contenedorización del entorno para un despliegue aislado, ligero y consistente en producción.

#### Alcance y Funcionalidades Clave

- **Carga de matrices .xlsx vía Telegram:** El operador envía el archivo Excel directamente al bot para detonar el flujo automático sin intermediación de interfaces complejas.
- **Validación paralela con ThreadPoolExecutor:** Ejecución multihilo que consulta en paralelo las APIs de SOAP Remedy y Elasticsearch, verificando simultáneamente si los 100 a 150 folios cuentan con información requerida o si ya fueron concluidos.
- **Generación y entrega de reporte .csv:** Al concluir la validación, el bot genera un archivo .csv consolidado y lo envía al usuario dentro del mismo chat para su análisis y descarga inmediata.
- **Gobernanza y tipado estricto:** Validación de la estructura de datos mediante esquemas de Pydantic, previniendo fallos por formatos inconsistentes o respuestas incompletas de los servicios integrados.