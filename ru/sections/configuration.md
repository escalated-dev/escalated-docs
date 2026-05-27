# Конфигурация

Escalated работает из коробки с разумными настройками по умолчанию. Конфигурация опциональна, но доступна для кастомизации.

> **Параметры конфигурации**
>
> - `routes.prefix` -- URL-префикс для всех маршрутов Escalated (по умолчанию: `support`)
> - `routes.middleware` -- Middleware для клиентских маршрутов (по умолчанию: `['web', 'auth']`)
> - `user_model` -- Класс модели пользователя (по умолчанию: `App\Models\User`)
> - `table_prefix` -- Префикс таблиц базы данных (по умолчанию: `escalated_`)
> - `tickets.allow_customer_close` -- Могут ли клиенты закрывать свои тикеты (по умолчанию: `true`)
> - `tickets.auto_close_resolved_after_days` -- Автозакрытие решённых тикетов через N дней (по умолчанию: `7`)
> - `sla.business_hours_only` -- Учитывать только рабочие часы для целей SLA (по умолчанию: `false`)
> - `notifications.channels` -- Каналы уведомлений (по умолчанию: `['mail', 'database']`)

## Настройки и модули администрирования

Последние обновления платформы добавляют экраны конфигурации и управления для:

- Настраиваемые поля с условными правилами видимости
- Настраиваемые статусы и расписания рабочих часов
- Роли (RBAC), маршрутизация на основе навыков и ёмкость агентов
- Просмотр журнала аудита
- Автоматизации и исходящие вебхуки
- Поведение опроса CSAT
- SSO и двухфакторная аутентификация
- Политики хранения данных и поведение удаления
- Настройки каналов электронной почты
- Пользовательские объекты и записи

## Публикация ресурсов

```bash
# Publish config file
$ php artisan vendor:publish --tag=escalated-config

# Publish email templates for customization
$ php artisan vendor:publish --tag=escalated-views

# Publish migrations (if you need to customize)
$ php artisan vendor:publish --tag=escalated-migrations
```
