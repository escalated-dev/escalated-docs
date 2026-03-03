# Estados y prioridades

Escalated trata los tickets como maquinas de estados. Las transiciones de estado se aplican y son configurables.

## Estados

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Prioridades

- Low
- Medium
- High
- Urgent
- Critical

Las transiciones son configurables a traves de `config/escalated.php` bajo la clave `transitions`.

Los administradores pueden crear y gestionar estados personalizados en el panel de administracion (`/support/admin/statuses`).
