# **Plataforma de Monitoreo y Asignación de Alarmas: DashIVR**

#### Propósito del Proyecto

Centralizar, visualizar y gestionar en tiempo real el ciclo de vida de las alarmas generadas en Elasticsearch mediante una aplicación web de página única (SPA). El sistema asegura que ninguna incidencia crítica quede en el olvido, facilitando su delegación inmediata a operadores en activo y orquestando el enriquecimiento automático del ticket asociado en BMC Remedy una vez asignado.

#### Problema que Resuelve

- **Eliminación de alarmas perdidas y mejora en KPIs:** Erradica el extravío de alertas del sistema, impulsando un **incremento del 40% en positividad y productividad operativa** durante la validación de registros críticos.
- **Asignación inteligente según disponibilidad:** Evita cuellos de botella y tickets desatendidos al verificar el estatus del operador (activo/inactivo) antes de permitir la asignación.
- **Automatización del enriquecimiento en Remedy:** Suprime la necesidad de actualizar manualmente los sistemas de mesa de ayuda; al momento de asignar la alarma, se conecta de forma inmediata a Remedy para completar los datos del ticket.
- **Fluidez y agilidad para el operador:** Al ser una SPA con sincronización reactiva en segundo plano, el equipo navega sin recargas de página lentas ni pérdidas de contexto, manteniendo una atención continua frente a volúmenes altos de eventos.

#### Stack Tecnológico

- **Frontend:** React, Vite, Material UI (MUI).
- **Gestión de Estado y Reactividad:** TanStack Query (refresco reactivo, sincronización y caché de datos) y React-Redux (gestión de estado global).
- **Backend:** NestJS (arquitectura modular, tipada y estructurada para el API/CRUD).
- **Servicio de Enriquecimiento (Worker/Script):** Python, `requests` y protocolos SOAP (consumo y actualización de tickets en BMC Remedy).
- **Bases de Datos & Fuentes de Información:**
    - **Elasticsearch:** Motor de búsqueda y origen de eventos y alarmas analíticas.
    - **PostgreSQL:** Persistencia relacional de operadores, roles, disponibilidad y control de auditoría de asignaciones.
- **Cliente HTTP:** Axios.

#### Alcance y Funcionalidades Clave

- **Tablero reactivo de alarmas (CRUD):** Visualización en tiempo real de eventos generados por Elasticsearch mediante peticiones asíncronas optimizadas con TanStack Query.
- **Gestión y validación de disponibilidad:** Control de acceso y reglas de asignación que impiden adjudicar incidencias a personal inactivo o desconectado.
- **Integración híbrida backend-SOAP:** Flujo orquestado donde NestJS atiende la interacción visual y delega a Python el consumo de los servicios SOAP de Remedy para nutrir la incidencia en el instante de la asignación.
- **Interfaz ergonómica y rápida:** Componentes basados en Material UI adaptados a flujos de trabajo de soporte crítico y monitoreo continuo.