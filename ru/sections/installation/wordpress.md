## 1. Установите плагин

```bash
$ wp plugin install escalated --activate
```

## 2. Настройте параметры

Перейдите в **Escalated -> Settings** в wp-admin для настройки отделов, политик SLA, правил эскалации и каналов электронной почты.

## 3. Добавьте шорткоды

Разместите шорткоды на любой странице, чтобы предоставить клиентам портал поддержки:

```shortcodes
[escalated_tickets]        // Ticket list
[escalated_create_ticket]  // New ticket form
[escalated_view_ticket]    // Ticket detail
```

> **Примечание:** Плагин WordPress является самодостаточным -- он не использует Inertia.js. Весь интерфейс отображается через встроенные экраны администрирования WordPress и шаблоны фронтенда на основе шорткодов.
