# Configuracao

O Escalated funciona com valores padrao adequados. A configuracao e opcional, mas esta disponivel para personalizacao.

> **Opcoes de configuracao**
>
> - `routes.prefix` -- O prefixo de URL para todas as rotas do Escalated (padrao: `support`)
> - `routes.middleware` -- Middleware aplicado as rotas do cliente (padrao: `['web', 'auth']`)
> - `user_model` -- A classe do modelo de usuario (padrao: `App\Models\User`)
> - `table_prefix` -- Prefixo para tabelas do banco de dados (padrao: `escalated_`)
> - `tickets.allow_customer_close` -- Se os clientes podem fechar seus proprios tickets (padrao: `true`)
> - `tickets.auto_close_resolved_after_days` -- Fechar automaticamente tickets resolvidos apos N dias (padrao: `7`)
> - `sla.business_hours_only` -- Contar apenas horario comercial para metas de SLA (padrao: `false`)
> - `notifications.channels` -- Canais de notificacao (padrao: `['mail', 'database']`)

## Configuracoes administrativas e modulos

Atualizacoes recentes da plataforma adicionam telas de configuracao e gerenciamento para:

- Campos personalizados com regras de visibilidade condicional
- Status personalizados e cronogramas de horario comercial
- Funcoes (RBAC), roteamento baseado em habilidades e capacidade de agentes
- Revisao do log de auditoria
- Automacoes e webhooks de saida
- Comportamento de pesquisa CSAT
- SSO e autenticacao de dois fatores
- Politicas de retencao de dados e comportamento de limpeza
- Configuracoes de canal de e-mail
- Objetos e registros personalizados

## Publicando recursos

```bash
# Publicar arquivo de configuracao
$ php artisan vendor:publish --tag=escalated-config

# Publicar templates de e-mail para personalizacao
$ php artisan vendor:publish --tag=escalated-views

# Publicar migracoes (caso precise personalizar)
$ php artisan vendor:publish --tag=escalated-migrations
```
