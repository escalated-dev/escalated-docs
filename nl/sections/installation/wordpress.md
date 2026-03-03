## 1. Installeer de plugin

```bash
$ wp plugin install escalated --activate
```

## 2. Configureer instellingen

Navigeer naar **Escalated -> Settings** in wp-admin om afdelingen, SLA-beleid, escalatieregels en e-mailkanalen te configureren.

## 3. Voeg shortcodes toe

Plaats shortcodes op elke pagina om klanten een supportportaal te bieden:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Let op:** De WordPress-plugin is op zichzelf staand -- het maakt geen gebruik van Inertia.js. Alle UI wordt weergegeven via native WordPress-beheerschermen en shortcode-gestuurde frontendtemplates.
