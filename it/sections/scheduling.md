# Pianificazione

Escalated fornisce comandi artisan per la gestione automatizzata del ciclo di vita dei ticket. Aggiungili al tuo scheduler.

```php
use Illuminate\Support\Facades\Schedule;

// Controlla le violazioni SLA
Schedule::command('escalated:check-sla')->everyMinute();

// Valuta le regole di escalation
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// Esegui le automazioni basate sul tempo
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// Chiudi automaticamente i ticket risolti dopo i giorni configurati
Schedule::command('escalated:close-resolved')->daily();

// Elimina le vecchie voci del log attività
Schedule::command('escalated:purge-activities')->weekly();

// Elimina i dati secondo le impostazioni di conservazione
Schedule::command('escalated:purge-expired')->daily();

// Controlla la casella IMAP in entrata (solo se si utilizza l'adattatore IMAP in entrata)
Schedule::command('escalated:poll-imap')->everyMinute();
```

## Comandi disponibili

- `escalated:check-sla` -- Controlla i ticket aperti rispetto alle policy SLA e invia gli eventi `SlaBreached`
- `escalated:evaluate-escalations` -- Esegue le regole di escalation sui ticket corrispondenti e applica le azioni configurate
- `escalated:run-automations` -- Esegue le regole di automazione basate sul tempo sui ticket idonei
- `escalated:close-resolved` -- Chiude i ticket che sono nello stato "resolved" da un numero di giorni configurato
- `escalated:purge-activities` -- Elimina le voci del log attività più vecchie del periodo di conservazione configurato
- `escalated:purge-expired` -- Elimina ticket, allegati e log di audit in base alle impostazioni della politica di conservazione
- `escalated:poll-imap` -- Controlla la casella IMAP configurata per le email in entrata
