# Configurazione

Escalated funziona immediatamente con valori predefiniti sensati. La configurazione è opzionale ma disponibile per la personalizzazione.

> **Opzioni di configurazione**
>
> - `routes.prefix` -- Il prefisso URL per tutte le route di Escalated (predefinito: `support`)
> - `routes.middleware` -- Middleware applicato alle route dei clienti (predefinito: `['web', 'auth']`)
> - `user_model` -- La classe del modello utente (predefinito: `App\Models\User`)
> - `table_prefix` -- Prefisso per le tabelle del database (predefinito: `escalated_`)
> - `tickets.allow_customer_close` -- Se i clienti possono chiudere i propri ticket (predefinito: `true`)
> - `tickets.auto_close_resolved_after_days` -- Chiusura automatica dei ticket risolti dopo N giorni (predefinito: `7`)
> - `sla.business_hours_only` -- Conteggia solo le ore lavorative per gli obiettivi SLA (predefinito: `false`)
> - `notifications.channels` -- Canali di notifica (predefinito: `['mail', 'database']`)

## Impostazioni e moduli amministrativi

Gli aggiornamenti recenti della piattaforma aggiungono schermate di configurazione e gestione per:

- Campi personalizzati con regole di visibilità condizionale
- Stati personalizzati e pianificazione degli orari lavorativi
- Ruoli (RBAC), routing basato su competenze e capacità degli agenti
- Revisione del registro di audit
- Automazioni e webhook in uscita
- Comportamento dei sondaggi CSAT
- SSO e autenticazione a due fattori
- Politiche di conservazione dei dati e comportamento di eliminazione
- Impostazioni dei canali email
- Oggetti personalizzati e record

## Pubblicazione degli asset

```bash
# Pubblica il file di configurazione
$ php artisan vendor:publish --tag=escalated-config

# Pubblica i template email per la personalizzazione
$ php artisan vendor:publish --tag=escalated-views

# Pubblica le migrazioni (se necessario personalizzare)
$ php artisan vendor:publish --tag=escalated-migrations
```
