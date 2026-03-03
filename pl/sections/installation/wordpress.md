## 1. Zainstaluj wtyczkę

```bash
$ wp plugin install escalated --activate
```

## 2. Skonfiguruj ustawienia

Przejdź do **Escalated -> Settings** w wp-admin, aby skonfigurować działy, polityki SLA, reguły eskalacji i kanały e-mail.

## 3. Dodaj shortcody

Umieść shortcody na dowolnej stronie, aby udostępnić klientom portal wsparcia:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Uwaga:** Wtyczka WordPress jest samodzielna -- nie korzysta z Inertia.js. Cały interfejs jest renderowany przez natywne ekrany administracyjne WordPress i szablony frontendowe oparte na shortcodach.
