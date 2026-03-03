## 1. Installer le plugin

```bash
$ wp plugin install escalated --activate
```

## 2. Configurer les parametres

Rendez-vous dans **Escalated -> Settings** dans wp-admin pour configurer les departements, les politiques SLA, les regles d'escalade et les canaux de messagerie.

## 3. Ajouter les shortcodes

Placez les shortcodes sur n'importe quelle page pour offrir aux clients un portail de support :

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Remarque :** Le plugin WordPress est autonome -- il n'utilise pas Inertia.js. Toute l'interface est rendue via les ecrans d'administration natifs de WordPress et les modeles frontend bases sur les shortcodes.
