# Scheduling

Escalated provides artisan commands for automated ticket lifecycle management. Add them to your scheduler.

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

## Available commands

- `escalated:check-sla` -- Checks open tickets against SLA policies and dispatches `SlaBreached` events
- `escalated:evaluate-escalations` -- Runs escalation rules against matching tickets and applies configured actions
- `escalated:run-automations` -- Runs time-based automation rules against eligible tickets
- `escalated:close-resolved` -- Closes tickets that have been in "resolved" status for the configured number of days
- `escalated:purge-activities` -- Deletes activity log entries older than the configured retention period
- `escalated:purge-expired` -- Purges tickets, attachments, and audit logs based on retention policy settings
- `escalated:poll-imap` -- Polls the configured IMAP mailbox for inbound email replies
