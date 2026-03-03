# Agendamento

O Escalated fornece comandos artisan para gerenciamento automatizado do ciclo de vida dos tickets. Adicione-os ao seu agendador.

```php
use Illuminate\Support\Facades\Schedule;

// Verificar violacoes de SLA
Schedule::command('escalated:check-sla')->everyMinute();

// Avaliar regras de escalonamento
Schedule::command('escalated:evaluate-escalations')->everyFiveMinutes();

// Executar automacoes baseadas em tempo
Schedule::command('escalated:run-automations')->everyFiveMinutes();

// Fechar automaticamente tickets resolvidos apos dias configurados
Schedule::command('escalated:close-resolved')->daily();

// Limpar entradas antigas do log de atividades
Schedule::command('escalated:purge-activities')->weekly();

// Limpar dados de acordo com configuracoes de retencao
Schedule::command('escalated:purge-expired')->daily();

// Consultar caixa de entrada IMAP (apenas se usar o adaptador IMAP)
Schedule::command('escalated:poll-imap')->everyMinute();
```

## Comandos disponiveis

- `escalated:check-sla` -- Verifica tickets abertos contra politicas de SLA e despacha eventos `SlaBreached`
- `escalated:evaluate-escalations` -- Executa regras de escalonamento contra tickets correspondentes e aplica acoes configuradas
- `escalated:run-automations` -- Executa regras de automacao baseadas em tempo contra tickets elegiveis
- `escalated:close-resolved` -- Fecha tickets que estao no status "resolved" pelo numero configurado de dias
- `escalated:purge-activities` -- Exclui entradas do log de atividades mais antigas que o periodo de retencao configurado
- `escalated:purge-expired` -- Limpa tickets, anexos e logs de auditoria com base nas configuracoes de politica de retencao
- `escalated:poll-imap` -- Consulta a caixa de correio IMAP configurada para respostas de e-mail recebidas
