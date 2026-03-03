## 1. Plugin installieren

```bash
$ wp plugin install escalated --activate
```

## 2. Einstellungen konfigurieren

Navigieren Sie zu **Escalated -> Settings** in wp-admin, um Abteilungen, SLA-Richtlinien, Eskalationsregeln und E-Mail-Kanäle zu konfigurieren.

## 3. Shortcodes hinzufügen

Platzieren Sie Shortcodes auf einer beliebigen Seite, um Kunden ein Support-Portal bereitzustellen:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Hinweis:** Das WordPress-Plugin ist eigenständig -- es verwendet kein Inertia.js. Die gesamte Oberfläche wird über native WordPress-Admin-Bildschirme und Shortcode-basierte Frontend-Vorlagen gerendert.
