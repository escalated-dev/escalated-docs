# Configuration

Escalated works out of the box with sensible defaults. Configuration is optional but available for customization.

> **Configuration options**
>
> - `routes.prefix` -- The URL prefix for all Escalated routes (default: `support`)
> - `routes.middleware` -- Middleware applied to customer routes (default: `['web', 'auth']`)
> - `user_model` -- The user model class (default: `App\Models\User`)
> - `table_prefix` -- Prefix for database tables (default: `escalated_`)
> - `tickets.allow_customer_close` -- Whether customers can close their own tickets (default: `true`)
> - `tickets.auto_close_resolved_after_days` -- Auto-close resolved tickets after N days (default: `7`)
> - `sla.business_hours_only` -- Only count business hours for SLA targets (default: `false`)
> - `notifications.channels` -- Notification channels (default: `['mail', 'database']`)

## Admin settings and modules

Recent platform updates add configuration and management screens for:

- Custom fields with conditional visibility rules
- Custom statuses and business hours schedules
- Roles (RBAC), skills-based routing, and agent capacity
- Audit log review
- Automations and outbound webhooks
- CSAT survey behavior
- SSO and two-factor authentication
- Data retention policies and purge behavior
- Email channel settings
- Custom objects and records

## Publishing assets

```bash
# Publish config file
$ php artisan vendor:publish --tag=escalated-config

# Publish email templates for customization
$ php artisan vendor:publish --tag=escalated-views

# Publish migrations (if you need to customize)
$ php artisan vendor:publish --tag=escalated-migrations
```
