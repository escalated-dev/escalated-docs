# Configuratie

Escalated werkt direct uit de doos met verstandige standaardwaarden. Configuratie is optioneel maar beschikbaar voor aanpassing.

> **Configuratieopties**
>
> - `routes.prefix` -- Het URL-voorvoegsel voor alle Escalated-routes (standaard: `support`)
> - `routes.middleware` -- Middleware toegepast op klantroutes (standaard: `['web', 'auth']`)
> - `user_model` -- De gebruikersmodelklasse (standaard: `App\Models\User`)
> - `table_prefix` -- Voorvoegsel voor databasetabellen (standaard: `escalated_`)
> - `tickets.allow_customer_close` -- Of klanten hun eigen tickets mogen sluiten (standaard: `true`)
> - `tickets.auto_close_resolved_after_days` -- Opgeloste tickets automatisch sluiten na N dagen (standaard: `7`)
> - `sla.business_hours_only` -- Alleen kantooruren tellen voor SLA-doelen (standaard: `false`)
> - `notifications.channels` -- Notificatiekanalen (standaard: `['mail', 'database']`)

## Beheerinstellingen en modules

Recente platformupdates voegen configuratie- en beheerschermen toe voor:

- Aangepaste velden met conditionele zichtbaarheidsregels
- Aangepaste statussen en kantoorurenroosters
- Rollen (RBAC), op vaardigheden gebaseerde routering en agentcapaciteit
- Auditlogboekcontrole
- Automatiseringen en uitgaande webhooks
- CSAT-enquetegedrag
- SSO en tweefactorauthenticatie
- Gegevensbewaringsbeleid en opschoningsgedrag
- E-mailkanaalinstellingen
- Aangepaste objecten en records

## Middelen publiceren

```bash
# Configuratiebestand publiceren
$ php artisan vendor:publish --tag=escalated-config

# E-mailtemplates publiceren voor aanpassing
$ php artisan vendor:publish --tag=escalated-views

# Migraties publiceren (als je wilt aanpassen)
$ php artisan vendor:publish --tag=escalated-migrations
```
