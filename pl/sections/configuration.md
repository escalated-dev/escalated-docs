# Konfiguracja

Escalated działa od razu z rozsądnymi wartościami domyślnymi. Konfiguracja jest opcjonalna, ale dostępna do personalizacji.

> **Opcje konfiguracji**
>
> - `routes.prefix` -- Prefiks URL dla wszystkich tras Escalated (domyślnie: `support`)
> - `routes.middleware` -- Middleware stosowany do tras klientów (domyślnie: `['web', 'auth']`)
> - `user_model` -- Klasa modelu użytkownika (domyślnie: `App\Models\User`)
> - `table_prefix` -- Prefiks tabel bazy danych (domyślnie: `escalated_`)
> - `tickets.allow_customer_close` -- Czy klienci mogą zamykać własne zgłoszenia (domyślnie: `true`)
> - `tickets.auto_close_resolved_after_days` -- Automatyczne zamykanie rozwiązanych zgłoszeń po N dniach (domyślnie: `7`)
> - `sla.business_hours_only` -- Uwzględnianie tylko godzin pracy w obliczeniach SLA (domyślnie: `false`)
> - `notifications.channels` -- Kanały powiadomień (domyślnie: `['mail', 'database']`)

## Ustawienia administracyjne i moduły

Najnowsze aktualizacje platformy dodają ekrany konfiguracji i zarządzania dla:

- Pola niestandardowe z warunkowymi regułami widoczności
- Niestandardowe statusy i harmonogramy godzin pracy
- Role (RBAC), routing oparty na umiejętnościach i pojemność agentów
- Przegląd dziennika audytu
- Automatyzacje i wychodzące webhooki
- Zachowanie ankiet CSAT
- SSO i uwierzytelnianie dwuskładnikowe
- Polityki retencji danych i zachowanie czyszczenia
- Ustawienia kanałów e-mail
- Obiekty niestandardowe i rekordy

## Publikowanie zasobów

```bash
# Publikuj plik konfiguracyjny
$ php artisan vendor:publish --tag=escalated-config

# Publikuj szablony e-mail do personalizacji
$ php artisan vendor:publish --tag=escalated-views

# Publikuj migracje (jeśli potrzebujesz personalizacji)
$ php artisan vendor:publish --tag=escalated-migrations
```
