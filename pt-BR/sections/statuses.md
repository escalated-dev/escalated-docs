# Status e Prioridades

O Escalated trata tickets como maquinas de estado. As transicoes de status sao aplicadas e configuraveis.

## Status

- Open
- In Progress
- Waiting on Customer
- Waiting on Agent
- Escalated
- Resolved
- Closed
- Reopened

## Prioridades

- Low
- Medium
- High
- Urgent
- Critical

As transicoes sao configuraveis em `config/escalated.php` na chave `transitions`.

Administradores podem criar e gerenciar status personalizados no painel de administracao (`/support/admin/statuses`).
