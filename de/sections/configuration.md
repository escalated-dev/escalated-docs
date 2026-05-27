# Konfiguration

Escalated funktioniert sofort mit sinnvollen Standardeinstellungen. Die Konfiguration ist optional, steht aber zur Anpassung zur Verfügung.

> **Konfigurationsoptionen**
>
> - `routes.prefix` -- Das URL-Präfix für alle Escalated-Routen (Standard: `support`)
> - `routes.middleware` -- Middleware für Kundenrouten (Standard: `['web', 'auth']`)
> - `user_model` -- Die User-Model-Klasse (Standard: `App\Models\User`)
> - `table_prefix` -- Präfix für Datenbanktabellen (Standard: `escalated_`)
> - `tickets.allow_customer_close` -- Ob Kunden ihre eigenen Tickets schließen können (Standard: `true`)
> - `tickets.auto_close_resolved_after_days` -- Gelöste Tickets nach N Tagen automatisch schließen (Standard: `7`)
> - `sla.business_hours_only` -- Nur Geschäftszeiten für SLA-Ziele berücksichtigen (Standard: `false`)
> - `notifications.channels` -- Benachrichtigungskanäle (Standard: `['mail', 'database']`)

## Admin-Einstellungen und Module

Aktuelle Plattform-Updates fügen Konfigurations- und Verwaltungsoberflächen hinzu für:

- Benutzerdefinierte Felder mit bedingten Sichtbarkeitsregeln
- Benutzerdefinierte Status und Geschäftszeiten-Zeitpläne
- Rollen (RBAC), fähigkeitsbasiertes Routing und Agentenkapazität
- Audit-Log-Überprüfung
- Automatisierungen und ausgehende Webhooks
- CSAT-Umfrageverhalten
- SSO und Zwei-Faktor-Authentifizierung
- Datenaufbewahrungsrichtlinien und Bereinigungsverhalten
- E-Mail-Kanaleinstellungen
- Benutzerdefinierte Objekte und Datensätze

## Assets veröffentlichen

```bash
# Konfigurationsdatei veröffentlichen
$ php artisan vendor:publish --tag=escalated-config

# E-Mail-Vorlagen zur Anpassung veröffentlichen
$ php artisan vendor:publish --tag=escalated-views

# Migrationen veröffentlichen (falls Anpassung nötig)
$ php artisan vendor:publish --tag=escalated-migrations
```
