# Correo entrante

Crea y responde tickets directamente desde correos electronicos entrantes. Escalated soporta webhooks de **Mailgun**, **Postmark**, **AWS SES** y sondeo **IMAP** como respaldo.

## Como funciona

1. Tu proveedor de correo recibe un mensaje en tu direccion de soporte (por ejemplo, `support@yourapp.com`)
2. El proveedor lo reenvia a tu aplicacion via webhook (o el sondeo IMAP lo recupera)
3. Escalated normaliza el payload y busca coincidencias de hilo mediante la referencia del asunto (por ejemplo, `[ESC-00001]`) o los encabezados `In-Reply-To`
4. Los correos que coinciden agregan una respuesta; los que no coinciden crean un nuevo ticket (o ticket de invitado para remitentes desconocidos)

## Configuracion

Habilita el correo entrante y configura tu adaptador en la configuracion de administracion, o mediante variables de entorno. La configuracion de administracion tiene prioridad sobre los valores de entorno/configuracion.

## URLs de webhooks

Apunta el webhook entrante de tu proveedor de correo a estas URLs. Estas rutas no requieren autenticacion (utilizan verificacion de firma en su lugar).

| Proveedor | URL del webhook |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## Sondeo IMAP

Para proveedores de correo sin soporte de webhooks, usa el comando de sondeo IMAP de forma programada.

## Funcionalidades

- **Deteccion de hilos** mediante referencia en el asunto y encabezados In-Reply-To / References
- **Tickets de invitados** para remitentes desconocidos con nombres derivados automaticamente
- **Reapertura automatica** de tickets resueltos o cerrados cuando llega una respuesta por correo
- **Deteccion de duplicados** mediante encabezados Message-ID para evitar procesamiento duplicado
- **Gestion de adjuntos** con limites configurables de tamano y cantidad
- **Registro de auditoria** -- cada correo entrante se registra para depuracion y cumplimiento
- **Configurable por administracion** -- todas las configuraciones gestionables desde el panel de administracion con respaldo de variables de entorno/configuracion
