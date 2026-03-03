# Harmonogramowanie

Escalated udostępnia komendy artisan do automatycznego zarządzania cyklem życia zgłoszeń. Dodaj je do swojego harmonogramu.

```php
use Illuminate\Support\Facades\Schedule;

// Check for SLA breaches
Schedule::command('escalated:check-sla')->everyMinute();

// Evaluate escalation rules
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// Run time-based automations
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// Auto-close resolved tickets after configured days
Schedule::command('escalated:close-resolved')->daily();

// Purge old activity log entries
Schedule::command('escalated:purge-activities')->weekly();

// Purge data according to retention settings
Schedule::command('escalated:purge-expired')->daily();

// Poll inbound IMAP mailbox (only if using IMAP inbound adapter)
Schedule::command('escalated:poll-imap')->everyMinute();
```

## Dostępne komendy

- `escalated:check-sla` -- Sprawdza otwarte zgłoszenia pod kątem polityk SLA i wysyła zdarzenia `SlaBreached`
- `escalated:evaluate-escalations` -- Uruchamia reguły eskalacji dla pasujących zgłoszeń i stosuje skonfigurowane akcje
- `escalated:run-automations` -- Uruchamia reguły automatyzacji czasowych dla kwalifikujących się zgłoszeń
- `escalated:close-resolved` -- Zamyka zgłoszenia, które są w statusie „resolved" przez skonfigurowaną liczbę dni
- `escalated:purge-activities` -- Usuwa wpisy dziennika aktywności starsze niż skonfigurowany okres retencji
- `escalated:purge-expired` -- Czyści zgłoszenia, załączniki i dzienniki audytu zgodnie z ustawieniami polityki retencji
- `escalated:poll-imap` -- Odpytuje skonfigurowaną skrzynkę IMAP w poszukiwaniu przychodzących odpowiedzi e-mail
