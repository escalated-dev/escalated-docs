# Planning

Escalated biedt artisan-commando's voor geautomatiseerd beheer van de ticketlevenscyclus. Voeg ze toe aan je planner.

```php
use Illuminate\Support\Facades\Schedule;

// Controleren op SLA-schendingen
Schedule::command('escalated:check-sla')->everyMinute();

// Escalatieregels evalueren
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// Tijdgebaseerde automatiseringen uitvoeren
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// Opgeloste tickets automatisch sluiten na geconfigureerde dagen
Schedule::command('escalated:close-resolved')->daily();

// Oude activiteitenlogvermeldingen opschonen
Schedule::command('escalated:purge-activities')->weekly();

// Gegevens opschonen volgens bewaringsinstellingen
Schedule::command('escalated:purge-expired')->daily();

// IMAP-mailbox pollen (alleen bij gebruik van IMAP-adapter)
Schedule::command('escalated:poll-imap')->everyMinute();
```

## Beschikbare commando's

- `escalated:check-sla` -- Controleert openstaande tickets tegen SLA-beleid en dispatcht `SlaBreached`-events
- `escalated:evaluate-escalations` -- Voert escalatieregels uit tegen overeenkomende tickets en past geconfigureerde acties toe
- `escalated:run-automations` -- Voert tijdgebaseerde automatiseringsregels uit tegen in aanmerking komende tickets
- `escalated:close-resolved` -- Sluit tickets die het geconfigureerde aantal dagen de status "resolved" hebben
- `escalated:purge-activities` -- Verwijdert activiteitenlogvermeldingen ouder dan de geconfigureerde bewaarperiode
- `escalated:purge-expired` -- Schoont tickets, bijlagen en auditlogboeken op op basis van bewaringsbeleidsinstellingen
- `escalated:poll-imap` -- Pollt de geconfigureerde IMAP-mailbox voor inkomende e-mailreacties
