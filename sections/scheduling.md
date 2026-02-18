# Scheduling

Escalated provides artisan commands for automated ticket lifecycle management. Add them to your scheduler.

```php
use Illuminate\Support\Facades\Schedule;

// Check for SLA breaches
Schedule::command('escalated:check-sla')->everyMinute();

// Evaluate escalation rules
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// Auto-close resolved tickets after configured days
Schedule::command('escalated:close-resolved')->daily();

// Purge old activity log entries
Schedule::command('escalated:purge-activities')->weekly();
```

## Available commands

- `escalated:check-sla` -- Checks open tickets against SLA policies and dispatches `SlaBreached` events
- `escalated:evaluate-escalations` -- Runs escalation rules against matching tickets and applies configured actions
- `escalated:close-resolved` -- Closes tickets that have been in "resolved" status for the configured number of days
- `escalated:purge-activities` -- Deletes activity log entries older than the configured retention period
