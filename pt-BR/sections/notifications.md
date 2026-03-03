# Notificacoes

O Escalated utiliza o sistema de notificacoes nativo do seu framework. Notificacoes por e-mail e banco de dados sao enviadas automaticamente para eventos-chave como novos tickets, respostas, atribuicoes, mudancas de status e violacoes de SLA.

- O responsavel pelo ticket e notificado sobre novas respostas
- O solicitante e notificado sobre respostas dos agentes e mudancas de status
- **Seguidores do ticket** recebem as mesmas notificacoes que o responsavel -- respostas e mudancas de status
- Alertas de violacao de SLA enviados ao responsavel e membros do departamento

Personalize os templates de e-mail publicando as views: `php artisan vendor:publish --tag=escalated-views`
