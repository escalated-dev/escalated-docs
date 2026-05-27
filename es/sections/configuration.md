# Configuracion

Escalated funciona de forma inmediata con valores predeterminados sensatos. La configuracion es opcional pero esta disponible para personalizacion.

> **Opciones de configuracion**
>
> - `routes.prefix` -- El prefijo de URL para todas las rutas de Escalated (predeterminado: `support`)
> - `routes.middleware` -- Middleware aplicado a las rutas de clientes (predeterminado: `['web', 'auth']`)
> - `user_model` -- La clase del modelo de usuario (predeterminado: `App\Models\User`)
> - `table_prefix` -- Prefijo para las tablas de base de datos (predeterminado: `escalated_`)
> - `tickets.allow_customer_close` -- Si los clientes pueden cerrar sus propios tickets (predeterminado: `true`)
> - `tickets.auto_close_resolved_after_days` -- Cerrar automaticamente tickets resueltos despues de N dias (predeterminado: `7`)
> - `sla.business_hours_only` -- Solo contar horas laborales para los objetivos de SLA (predeterminado: `false`)
> - `notifications.channels` -- Canales de notificacion (predeterminado: `['mail', 'database']`)

## Configuraciones y modulos de administracion

Las actualizaciones recientes de la plataforma agregan pantallas de configuracion y gestion para:

- Campos personalizados con reglas de visibilidad condicional
- Estados personalizados y horarios laborales
- Roles (RBAC), enrutamiento basado en habilidades y capacidad de agentes
- Revision del registro de auditoria
- Automatizaciones y webhooks salientes
- Comportamiento de encuestas CSAT
- SSO y autenticacion de dos factores
- Politicas de retencion de datos y comportamiento de purga
- Configuracion de canales de correo electronico
- Objetos y registros personalizados

## Publicar recursos

```bash
# Publicar archivo de configuracion
$ php artisan vendor:publish --tag=escalated-config

# Publicar plantillas de correo para personalizacion
$ php artisan vendor:publish --tag=escalated-views

# Publicar migraciones (si necesitas personalizarlas)
$ php artisan vendor:publish --tag=escalated-migrations
```
