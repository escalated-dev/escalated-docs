# Planification

Escalated fournit des commandes artisan pour la gestion automatisee du cycle de vie des tickets. Ajoutez-les a votre planificateur de taches.

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

## Commandes disponibles

- `escalated:check-sla` -- Verifie les tickets ouverts par rapport aux politiques SLA et declenche les evenements `SlaBreached`
- `escalated:evaluate-escalations` -- Execute les regles d'escalade sur les tickets correspondants et applique les actions configurees
- `escalated:run-automations` -- Execute les regles d'automatisation basees sur le temps sur les tickets eligibles
- `escalated:close-resolved` -- Cloture les tickets en statut "resolved" depuis le nombre de jours configure
- `escalated:purge-activities` -- Supprime les entrees du journal d'activite plus anciennes que la periode de retention configuree
- `escalated:purge-expired` -- Purge les tickets, pieces jointes et journaux d'audit selon les parametres de la politique de retention
- `escalated:poll-imap` -- Interroge la boite aux lettres IMAP configuree pour les reponses par e-mail entrantes
