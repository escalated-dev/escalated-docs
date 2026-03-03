## 1. Instale o plugin

```bash
$ wp plugin install escalated --activate
```

## 2. Defina as configuracoes

Navegue ate **Escalated -> Settings** no wp-admin para configurar departamentos, politicas de SLA, regras de escalonamento e canais de e-mail.

## 3. Adicione shortcodes

Insira shortcodes em qualquer pagina para oferecer aos clientes um portal de suporte:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Nota:** O plugin WordPress e independente -- ele nao utiliza Inertia.js. Toda a interface e renderizada por telas nativas de administracao do WordPress e templates de frontend alimentados por shortcodes.
