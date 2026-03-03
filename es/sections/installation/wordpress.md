## 1. Instalar el plugin

```bash
$ wp plugin install escalated --activate
```

## 2. Configurar ajustes

Navega a **Escalated -> Settings** en wp-admin para configurar departamentos, politicas SLA, reglas de escalamiento y canales de correo electronico.

## 3. Agregar shortcodes

Coloca shortcodes en cualquier pagina para ofrecer a los clientes un portal de soporte:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Nota:** El plugin de WordPress es independiente -- no utiliza Inertia.js. Toda la interfaz se renderiza mediante pantallas nativas de administracion de WordPress y plantillas frontend basadas en shortcodes.
