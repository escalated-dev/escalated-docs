# E-mail de Entrada

Crie e responda tickets diretamente a partir de e-mails recebidos. O Escalated suporta webhooks de **Mailgun**, **Postmark**, **AWS SES** e polling **IMAP** como alternativa.

## Como Funciona

1. Seu provedor de e-mail recebe uma mensagem no seu endereco de suporte (ex.: `support@yourapp.com`)
2. O provedor encaminha para sua aplicacao via webhook (ou o polling IMAP busca a mensagem)
3. O Escalated normaliza o payload e verifica correspondencia de thread via referencia no assunto (ex.: `[ESC-00001]`) ou cabecalhos `In-Reply-To`
4. E-mails correspondentes adicionam uma resposta; e-mails sem correspondencia criam um novo ticket (ou ticket de visitante para remetentes desconhecidos)

## Configuracao

Ative o e-mail de entrada e configure seu adaptador nas configuracoes administrativas, ou via variaveis de ambiente. As configuracoes administrativas tem prioridade sobre valores de env/config.

## URLs de Webhook

Aponte o webhook de entrada do seu provedor de e-mail para estas URLs. Estas rotas nao requerem autenticacao (usam verificacao de assinatura).

| Provedor | URL do Webhook |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## Polling IMAP

Para provedores de e-mail sem suporte a webhook, use o comando de polling IMAP em um agendamento.

## Recursos

- **Deteccao de thread** via referencia no assunto e cabecalhos In-Reply-To / References
- **Tickets de visitante** para remetentes desconhecidos com nomes de exibicao derivados automaticamente
- **Reabertura automatica** de tickets resolvidos ou fechados quando uma resposta chega via e-mail
- **Deteccao de duplicatas** via cabecalhos Message-ID para evitar processamento duplicado
- **Tratamento de anexos** com limites configuraveis de tamanho e quantidade
- **Log de auditoria** -- cada e-mail de entrada e registrado para depuracao e conformidade
- **Configuravel pelo administrador** -- todas as configuracoes gerenciaveis pelo painel administrativo com fallback para env/config
