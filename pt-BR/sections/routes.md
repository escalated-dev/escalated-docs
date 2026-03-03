# Rotas

O Escalated registra tres grupos de rotas sob o prefixo configurado (padrao: `/support`).

## Rotas do cliente

| Metodo | URL | Descricao |
| ------ | --- | ----------- |
| GET | /support | Lista de tickets do cliente |
| GET | /support/create | Formulario de novo ticket |
| POST | /support | Criar ticket |
| GET | /support/kb | Pagina inicial da base de conhecimento |
| GET | /support/kb/{slug} | Artigo da base de conhecimento |
| POST | /support/kb/{slug}/feedback | Feedback do artigo |
| GET | /support/{reference} | Detalhe do ticket |
| POST | /support/{reference}/reply | Responder ao ticket |
| POST | /support/{reference}/close | Fechar ticket |
| POST | /support/{reference}/reopen | Reabrir ticket |
| POST | /support/{reference}/rate | Enviar avaliacao de satisfacao |

## Rotas do agente

Requer o gate `escalated-agent`.

| Metodo | URL | Descricao |
| ------ | --- | ----------- |
| GET | /support/agent | Painel do agente |
| GET | /support/agent/tickets | Fila de tickets |
| GET | /support/agent/tickets/{reference} | Detalhe do ticket |
| POST | /support/agent/tickets/{reference}/reply | Resposta publica |
| POST | /support/agent/tickets/{reference}/note | Nota interna |
| POST | /support/agent/tickets/{reference}/assign | Atribuir agente |
| POST | /support/agent/tickets/{reference}/status | Alterar status |
| POST | /support/agent/tickets/{reference}/priority | Alterar prioridade |
| POST | /support/agent/tickets/bulk | Acoes em massa |
| POST | /support/agent/tickets/{reference}/follow | Alternar seguir |
| POST | /support/agent/tickets/{reference}/macro | Aplicar macro |
| POST | /support/agent/tickets/{reference}/presence | Reportar presenca |
| POST | /support/agent/tickets/{reference}/typing | Reportar status de digitacao |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Alternar fixacao de nota |

## Rotas do administrador

Requer o gate `escalated-admin`. Administradores tem todas as rotas de agente alem das paginas de gerenciamento.

| Metodo | URL | Descricao |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Painel de analiticos |
| GET | /support/admin/departments | Gerenciamento de departamentos |
| GET | /support/admin/sla-policies | Gerenciamento de politicas de SLA |
| GET | /support/admin/escalation-rules | Construtor de regras de escalonamento |
| GET | /support/admin/tags | Gerenciamento de tags |
| GET | /support/admin/canned-responses | Templates de respostas prontas |
| GET | /support/admin/macros | Gerenciamento de macros |
| GET | /support/admin/custom-fields | Campos e formularios personalizados |
| GET | /support/admin/statuses | Status personalizados |
| GET | /support/admin/business-hours | Cronogramas de horario comercial |
| GET | /support/admin/roles | Funcoes e permissoes de agentes |
| GET | /support/admin/audit-log | Trilha de auditoria |
| GET | /support/admin/skills | Gerenciamento de habilidades |
| GET | /support/admin/capacity | Controles de capacidade de agentes |
| GET | /support/admin/automations | Automacoes baseadas em tempo |
| GET | /support/admin/webhooks | Webhooks de saida |
| GET | /support/admin/webhooks/{webhook}/deliveries | Log de entregas de webhook |
| GET | /support/admin/kb-articles | Artigos da base de conhecimento |
| GET | /support/admin/kb-categories | Categorias da base de conhecimento |
| GET | /support/admin/reports/dashboard | Painel de relatorios |
| GET | /support/admin/reports/agents | Relatorio de produtividade de agentes |
| GET | /support/admin/reports/sla | Relatorio de desempenho de SLA |
| GET | /support/admin/reports/csat | Relatorio CSAT |
| GET | /support/admin/settings/csat | Configuracoes de pesquisa CSAT |
| GET | /support/admin/settings/sso | Configuracoes de SSO |
| GET | /support/admin/settings/two-factor | Configuracoes de autenticacao de dois fatores |
| GET | /support/admin/settings/data-retention | Configuracoes de retencao de dados |
| GET | /support/admin/settings/email | Configuracoes de canal de e-mail |
| GET | /support/admin/custom-objects | Objetos personalizados |
| GET | /support/admin/custom-objects/{customObject}/records | Registros de objetos personalizados |
| GET | /support/admin/tickets/merge-search | Buscar alvos de mesclagem |
| POST | /support/admin/tickets/{reference}/merge | Mesclar ticket no alvo |
| GET | /support/admin/tickets/{reference}/links | Listar tickets vinculados |
| POST | /support/admin/tickets/{reference}/links | Vincular ticket relacionado |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Desvincular ticket relacionado |
| GET | /support/admin/tickets/{reference}/side-conversations | Lista de conversas paralelas |
| POST | /support/admin/tickets/{reference}/side-conversations | Iniciar conversa paralela |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Responder em conversa paralela |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Fechar conversa paralela |
| POST | /support/admin/macros | Criar macro |
| PUT | /support/admin/macros/{macro} | Atualizar macro |
| DELETE | /support/admin/macros/{macro} | Excluir macro |

## Rotas de visitante

Nenhuma autenticacao necessaria. Acesso via token unico.

| Metodo | URL | Descricao |
| ------ | --- | ----------- |
| GET | /support/guest/create | Formulario de ticket de visitante |
| POST | /support/guest | Criar ticket de visitante |
| GET | /support/guest/{token} | Visualizar ticket de visitante |
| POST | /support/guest/{token}/reply | Responder ao ticket de visitante |
| POST | /support/guest/{token}/rate | Enviar avaliacao de satisfacao |
