# Rutas

Escalated registra tres grupos de rutas bajo el prefijo configurado (predeterminado: `/support`).

## Rutas de clientes

| Metodo | URL | Descripcion |
| ------ | --- | ----------- |
| GET | /support | Lista de tickets del cliente |
| GET | /support/create | Formulario de nuevo ticket |
| POST | /support | Crear ticket |
| GET | /support/kb | Inicio de la base de conocimiento |
| GET | /support/kb/{slug} | Articulo de la base de conocimiento |
| POST | /support/kb/{slug}/feedback | Retroalimentacion del articulo |
| GET | /support/{reference} | Detalle del ticket |
| POST | /support/{reference}/reply | Responder al ticket |
| POST | /support/{reference}/close | Cerrar ticket |
| POST | /support/{reference}/reopen | Reabrir ticket |
| POST | /support/{reference}/rate | Enviar valoracion de satisfaccion |

## Rutas de agentes

Requiere el gate `escalated-agent`.

| Metodo | URL | Descripcion |
| ------ | --- | ----------- |
| GET | /support/agent | Panel de agentes |
| GET | /support/agent/tickets | Cola de tickets |
| GET | /support/agent/tickets/{reference} | Detalle del ticket |
| POST | /support/agent/tickets/{reference}/reply | Respuesta publica |
| POST | /support/agent/tickets/{reference}/note | Nota interna |
| POST | /support/agent/tickets/{reference}/assign | Asignar agente |
| POST | /support/agent/tickets/{reference}/status | Cambiar estado |
| POST | /support/agent/tickets/{reference}/priority | Cambiar prioridad |
| POST | /support/agent/tickets/bulk | Acciones masivas en tickets |
| POST | /support/agent/tickets/{reference}/follow | Alternar seguimiento |
| POST | /support/agent/tickets/{reference}/macro | Aplicar macro |
| POST | /support/agent/tickets/{reference}/presence | Reportar presencia |
| POST | /support/agent/tickets/{reference}/typing | Reportar estado de escritura |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Alternar fijado en nota |

## Rutas de administracion

Requiere el gate `escalated-admin`. Los administradores tienen todas las rutas de agentes mas paginas de gestion.

| Metodo | URL | Descripcion |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Panel de analiticas |
| GET | /support/admin/departments | Gestion de departamentos |
| GET | /support/admin/sla-policies | Gestion de politicas SLA |
| GET | /support/admin/escalation-rules | Constructor de reglas de escalamiento |
| GET | /support/admin/tags | Gestion de etiquetas |
| GET | /support/admin/canned-responses | Plantillas de respuestas predefinidas |
| GET | /support/admin/macros | Gestion de macros |
| GET | /support/admin/custom-fields | Campos personalizados y formularios |
| GET | /support/admin/statuses | Estados personalizados |
| GET | /support/admin/business-hours | Horarios laborales |
| GET | /support/admin/roles | Roles y permisos de agentes |
| GET | /support/admin/audit-log | Registro de auditoria |
| GET | /support/admin/skills | Gestion de habilidades |
| GET | /support/admin/capacity | Controles de capacidad de agentes |
| GET | /support/admin/automations | Automatizaciones basadas en tiempo |
| GET | /support/admin/webhooks | Webhooks salientes |
| GET | /support/admin/webhooks/{webhook}/deliveries | Registro de entregas de webhooks |
| GET | /support/admin/kb-articles | Articulos de la base de conocimiento |
| GET | /support/admin/kb-categories | Categorias de la base de conocimiento |
| GET | /support/admin/reports/dashboard | Panel de informes |
| GET | /support/admin/reports/agents | Informe de productividad de agentes |
| GET | /support/admin/reports/sla | Informe de cumplimiento de SLA |
| GET | /support/admin/reports/csat | Informe CSAT |
| GET | /support/admin/settings/csat | Configuracion de encuestas CSAT |
| GET | /support/admin/settings/sso | Configuracion de SSO |
| GET | /support/admin/settings/two-factor | Configuracion de dos factores |
| GET | /support/admin/settings/data-retention | Configuracion de retencion de datos |
| GET | /support/admin/settings/email | Configuracion de canal de correo electronico |
| GET | /support/admin/custom-objects | Objetos personalizados |
| GET | /support/admin/custom-objects/{customObject}/records | Registros de objetos personalizados |
| GET | /support/admin/tickets/merge-search | Buscar destinos de fusion |
| POST | /support/admin/tickets/{reference}/merge | Fusionar ticket en destino |
| GET | /support/admin/tickets/{reference}/links | Listar tickets vinculados |
| POST | /support/admin/tickets/{reference}/links | Vincular ticket relacionado |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Desvincular ticket relacionado |
| GET | /support/admin/tickets/{reference}/side-conversations | Lista de conversaciones paralelas |
| POST | /support/admin/tickets/{reference}/side-conversations | Iniciar conversacion paralela |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Responder en conversacion paralela |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Cerrar conversacion paralela |
| POST | /support/admin/macros | Crear macro |
| PUT | /support/admin/macros/{macro} | Actualizar macro |
| DELETE | /support/admin/macros/{macro} | Eliminar macro |

## Rutas de invitados

No requiere autenticacion. Se accede mediante un token unico.

| Metodo | URL | Descripcion |
| ------ | --- | ----------- |
| GET | /support/guest/create | Formulario de ticket de invitado |
| POST | /support/guest | Crear ticket de invitado |
| GET | /support/guest/{token} | Ver ticket de invitado |
| POST | /support/guest/{token}/reply | Responder al ticket de invitado |
| POST | /support/guest/{token}/rate | Enviar valoracion de satisfaccion |
