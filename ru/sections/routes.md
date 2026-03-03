# Маршруты

Escalated регистрирует три группы маршрутов под настроенным префиксом (по умолчанию: `/support`).

## Клиентские маршруты

| Метод | URL | Описание |
| ------ | --- | ----------- |
| GET | /support | Список тикетов клиента |
| GET | /support/create | Форма нового тикета |
| POST | /support | Создание тикета |
| GET | /support/kb | Главная страница базы знаний |
| GET | /support/kb/{slug} | Статья базы знаний |
| POST | /support/kb/{slug}/feedback | Обратная связь по статье |
| GET | /support/{reference} | Детали тикета |
| POST | /support/{reference}/reply | Ответ на тикет |
| POST | /support/{reference}/close | Закрытие тикета |
| POST | /support/{reference}/reopen | Повторное открытие тикета |
| POST | /support/{reference}/rate | Отправка оценки удовлетворённости |

## Маршруты агентов

Требуется гейт `escalated-agent`.

| Метод | URL | Описание |
| ------ | --- | ----------- |
| GET | /support/agent | Дашборд агента |
| GET | /support/agent/tickets | Очередь тикетов |
| GET | /support/agent/tickets/{reference} | Детали тикета |
| POST | /support/agent/tickets/{reference}/reply | Публичный ответ |
| POST | /support/agent/tickets/{reference}/note | Внутренняя заметка |
| POST | /support/agent/tickets/{reference}/assign | Назначение агента |
| POST | /support/agent/tickets/{reference}/status | Изменение статуса |
| POST | /support/agent/tickets/{reference}/priority | Изменение приоритета |
| POST | /support/agent/tickets/bulk | Массовые действия с тикетами |
| POST | /support/agent/tickets/{reference}/follow | Переключение подписки |
| POST | /support/agent/tickets/{reference}/macro | Применение макроса |
| POST | /support/agent/tickets/{reference}/presence | Отчёт о присутствии |
| POST | /support/agent/tickets/{reference}/typing | Отчёт о статусе набора |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Переключение закрепления заметки |

## Маршруты администратора

Требуется гейт `escalated-admin`. Администраторы имеют все маршруты агентов плюс страницы управления.

| Метод | URL | Описание |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Аналитический дашборд |
| GET | /support/admin/departments | Управление отделами |
| GET | /support/admin/sla-policies | Управление политиками SLA |
| GET | /support/admin/escalation-rules | Конструктор правил эскалации |
| GET | /support/admin/tags | Управление тегами |
| GET | /support/admin/canned-responses | Шаблоны готовых ответов |
| GET | /support/admin/macros | Управление макросами |
| GET | /support/admin/custom-fields | Настраиваемые поля и формы |
| GET | /support/admin/statuses | Настраиваемые статусы |
| GET | /support/admin/business-hours | Расписания рабочих часов |
| GET | /support/admin/roles | Роли и права агентов |
| GET | /support/admin/audit-log | Журнал аудита |
| GET | /support/admin/skills | Управление навыками |
| GET | /support/admin/capacity | Управление ёмкостью агентов |
| GET | /support/admin/automations | Временные автоматизации |
| GET | /support/admin/webhooks | Исходящие вебхуки |
| GET | /support/admin/webhooks/{webhook}/deliveries | Журнал доставки вебхуков |
| GET | /support/admin/kb-articles | Статьи базы знаний |
| GET | /support/admin/kb-categories | Категории базы знаний |
| GET | /support/admin/reports/dashboard | Дашборд отчётов |
| GET | /support/admin/reports/agents | Отчёт о продуктивности агентов |
| GET | /support/admin/reports/sla | Отчёт о выполнении SLA |
| GET | /support/admin/reports/csat | Отчёт CSAT |
| GET | /support/admin/settings/csat | Настройки опроса CSAT |
| GET | /support/admin/settings/sso | Настройки SSO |
| GET | /support/admin/settings/two-factor | Настройки двухфакторной аутентификации |
| GET | /support/admin/settings/data-retention | Настройки хранения данных |
| GET | /support/admin/settings/email | Настройки канала электронной почты |
| GET | /support/admin/custom-objects | Пользовательские объекты |
| GET | /support/admin/custom-objects/{customObject}/records | Записи пользовательских объектов |
| GET | /support/admin/tickets/merge-search | Поиск целей объединения |
| POST | /support/admin/tickets/{reference}/merge | Объединение тикета с целевым |
| GET | /support/admin/tickets/{reference}/links | Список связанных тикетов |
| POST | /support/admin/tickets/{reference}/links | Связать тикет |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Отвязать связанный тикет |
| GET | /support/admin/tickets/{reference}/side-conversations | Список побочных разговоров |
| POST | /support/admin/tickets/{reference}/side-conversations | Начать побочный разговор |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Ответ в побочном разговоре |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Закрытие побочного разговора |
| POST | /support/admin/macros | Создание макроса |
| PUT | /support/admin/macros/{macro} | Обновление макроса |
| DELETE | /support/admin/macros/{macro} | Удаление макроса |

## Гостевые маршруты

Аутентификация не требуется. Доступ осуществляется по уникальному токену.

| Метод | URL | Описание |
| ------ | --- | ----------- |
| GET | /support/guest/create | Форма гостевого тикета |
| POST | /support/guest | Создание гостевого тикета |
| GET | /support/guest/{token} | Просмотр гостевого тикета |
| POST | /support/guest/{token}/reply | Ответ на гостевой тикет |
| POST | /support/guest/{token}/rate | Отправка оценки удовлетворённости |
