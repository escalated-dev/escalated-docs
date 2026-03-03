# Планирование

Escalated предоставляет artisan-команды для автоматического управления жизненным циклом тикетов. Добавьте их в ваш планировщик.

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

## Доступные команды

- `escalated:check-sla` -- Проверяет открытые тикеты на соответствие политикам SLA и отправляет события `SlaBreached`
- `escalated:evaluate-escalations` -- Запускает правила эскалации для подходящих тикетов и применяет настроенные действия
- `escalated:run-automations` -- Запускает временные правила автоматизации для подходящих тикетов
- `escalated:close-resolved` -- Закрывает тикеты, которые находились в статусе «resolved» в течение настроенного количества дней
- `escalated:purge-activities` -- Удаляет записи журнала активности старше настроенного периода хранения
- `escalated:purge-expired` -- Удаляет тикеты, вложения и записи аудита согласно настройкам политики хранения
- `escalated:poll-imap` -- Опрашивает настроенный почтовый ящик IMAP для входящей почты
