# Autorizacao

O Escalated utiliza dois gates de autorizacao para controlar o acesso as visualizacoes de agente e administrador. Defina-os na sua aplicacao para controlar quem pode gerenciar tickets.

> **Nota:** O Escalated compartilha automaticamente `page.props.escalated` em todas as respostas Inertia, contendo o prefixo da rota e o status de agente/administrador do usuario atual.
