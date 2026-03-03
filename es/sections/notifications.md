# Notificaciones

Escalated utiliza el sistema de notificaciones nativo de tu framework. Las notificaciones por correo electronico y base de datos se envian automaticamente para eventos clave como nuevos tickets, respuestas, asignaciones, cambios de estado e incumplimientos de SLA.

- El asignado del ticket recibe notificaciones sobre nuevas respuestas
- El solicitante recibe notificaciones sobre respuestas de agentes y cambios de estado
- Los **seguidores del ticket** reciben las mismas notificaciones que el asignado -- respuestas y cambios de estado
- Las alertas de incumplimiento de SLA se envian al asignado y a los miembros del departamento

Personaliza las plantillas de correo publicando las vistas: `php artisan vendor:publish --tag=escalated-views`
