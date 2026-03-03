# Tickets

Los tickets son el nucleo de Escalated. Cada ticket es una maquina de estados de larga duracion con un historial completo de conversacion, niveles de prioridad, seguimiento de asignacion y monitoreo de SLA.

> **Nota:** Cada ticket recibe una referencia unica (por ejemplo, `ESC-00001`) y soporta estados personalizados, niveles de prioridad, asignacion de departamentos, etiquetas, seguimiento de SLA y conversaciones enriquecidas con archivos adjuntos. Todos los datos se almacenan en tu base de datos.

## Flujos de trabajo avanzados de tickets

- Flujo de fusion de tickets para combinar duplicados preservando el historial
- Tickets vinculados para flujos de trabajo de incidentes/problemas relacionados
- Conversaciones paralelas para coordinacion interna/externa en paralelo
- Soporte de agente limitado para roles operativos con acceso restringido
- Formularios de campos personalizados con reglas condicionales basadas en el contexto del ticket
