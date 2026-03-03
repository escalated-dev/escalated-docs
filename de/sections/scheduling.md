# Zeitplanung

Escalated stellt Artisan-Befehle für die automatische Verwaltung des Ticket-Lebenszyklus bereit. Fügen Sie diese Ihrem Scheduler hinzu.

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

## Verfügbare Befehle

- `escalated:check-sla` -- Prüft offene Tickets gegen SLA-Richtlinien und löst `SlaBreached`-Events aus
- `escalated:evaluate-escalations` -- Führt Eskalationsregeln gegen passende Tickets aus und wendet konfigurierte Aktionen an
- `escalated:run-automations` -- Führt zeitbasierte Automatisierungsregeln gegen berechtigte Tickets aus
- `escalated:close-resolved` -- Schließt Tickets, die seit der konfigurierten Anzahl von Tagen den Status "Resolved" haben
- `escalated:purge-activities` -- Löscht Aktivitätsprotokolleinträge, die älter als die konfigurierte Aufbewahrungsfrist sind
- `escalated:purge-expired` -- Bereinigt Tickets, Anhänge und Audit-Logs gemäß den Aufbewahrungsrichtlinien
- `escalated:poll-imap` -- Ruft die konfigurierte IMAP-Mailbox für eingehende E-Mail-Antworten ab
