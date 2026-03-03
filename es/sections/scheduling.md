# Programacion

Escalated proporciona comandos artisan para la gestion automatizada del ciclo de vida de tickets. Agregalos a tu programador de tareas.

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

## Comandos disponibles

- `escalated:check-sla` -- Verifica los tickets abiertos contra las politicas de SLA y despacha eventos `SlaBreached`
- `escalated:evaluate-escalations` -- Ejecuta las reglas de escalamiento contra los tickets que coinciden y aplica las acciones configuradas
- `escalated:run-automations` -- Ejecuta las reglas de automatizacion basadas en tiempo contra los tickets elegibles
- `escalated:close-resolved` -- Cierra los tickets que han estado en estado "resolved" durante el numero de dias configurado
- `escalated:purge-activities` -- Elimina las entradas del registro de actividad mas antiguas que el periodo de retencion configurado
- `escalated:purge-expired` -- Purga tickets, archivos adjuntos y registros de auditoria segun la configuracion de la politica de retencion
- `escalated:poll-imap` -- Consulta el buzon de correo IMAP configurado para respuestas de correo entrante
