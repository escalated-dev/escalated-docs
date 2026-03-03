# Trasy

Escalated rejestruje trzy grupy tras pod skonfigurowanym prefiksem (domyślnie: `/support`).

## Trasy klientów

| Metoda | URL | Opis |
| ------ | --- | ----------- |
| GET | /support | Lista zgłoszeń klienta |
| GET | /support/create | Formularz nowego zgłoszenia |
| POST | /support | Utworzenie zgłoszenia |
| GET | /support/kb | Strona główna bazy wiedzy |
| GET | /support/kb/{slug} | Artykuł bazy wiedzy |
| POST | /support/kb/{slug}/feedback | Opinia o artykule |
| GET | /support/{reference} | Szczegóły zgłoszenia |
| POST | /support/{reference}/reply | Odpowiedź na zgłoszenie |
| POST | /support/{reference}/close | Zamknięcie zgłoszenia |
| POST | /support/{reference}/reopen | Ponowne otwarcie zgłoszenia |
| POST | /support/{reference}/rate | Wysłanie oceny satysfakcji |

## Trasy agentów

Wymaga bramki `escalated-agent`.

| Metoda | URL | Opis |
| ------ | --- | ----------- |
| GET | /support/agent | Panel agenta |
| GET | /support/agent/tickets | Kolejka zgłoszeń |
| GET | /support/agent/tickets/{reference} | Szczegóły zgłoszenia |
| POST | /support/agent/tickets/{reference}/reply | Odpowiedź publiczna |
| POST | /support/agent/tickets/{reference}/note | Notatka wewnętrzna |
| POST | /support/agent/tickets/{reference}/assign | Przypisanie agenta |
| POST | /support/agent/tickets/{reference}/status | Zmiana statusu |
| POST | /support/agent/tickets/{reference}/priority | Zmiana priorytetu |
| POST | /support/agent/tickets/bulk | Akcje zbiorcze na zgłoszeniach |
| POST | /support/agent/tickets/{reference}/follow | Przełączenie obserwowania |
| POST | /support/agent/tickets/{reference}/macro | Zastosowanie makra |
| POST | /support/agent/tickets/{reference}/presence | Zgłoszenie obecności |
| POST | /support/agent/tickets/{reference}/typing | Zgłoszenie statusu pisania |
| POST | /support/agent/tickets/{reference}/replies/{reply}/pin | Przełączenie przypięcia notatki |

## Trasy administracyjne

Wymaga bramki `escalated-admin`. Administratorzy mają dostęp do wszystkich tras agentów plus stron zarządzania.

| Metoda | URL | Opis |
| ------ | --- | ----------- |
| GET | /support/admin/reports | Panel analityczny |
| GET | /support/admin/departments | Zarządzanie działami |
| GET | /support/admin/sla-policies | Zarządzanie politykami SLA |
| GET | /support/admin/escalation-rules | Konfigurator reguł eskalacji |
| GET | /support/admin/tags | Zarządzanie tagami |
| GET | /support/admin/canned-responses | Szablony gotowych odpowiedzi |
| GET | /support/admin/macros | Zarządzanie makrami |
| GET | /support/admin/custom-fields | Pola niestandardowe i formularze |
| GET | /support/admin/statuses | Niestandardowe statusy |
| GET | /support/admin/business-hours | Harmonogramy godzin pracy |
| GET | /support/admin/roles | Role i uprawnienia agentów |
| GET | /support/admin/audit-log | Dziennik audytu |
| GET | /support/admin/skills | Zarządzanie umiejętnościami |
| GET | /support/admin/capacity | Kontrola pojemności agentów |
| GET | /support/admin/automations | Automatyzacje czasowe |
| GET | /support/admin/webhooks | Wychodzące webhooki |
| GET | /support/admin/webhooks/{webhook}/deliveries | Dziennik dostarczeń webhooków |
| GET | /support/admin/kb-articles | Artykuły bazy wiedzy |
| GET | /support/admin/kb-categories | Kategorie bazy wiedzy |
| GET | /support/admin/reports/dashboard | Panel raportów |
| GET | /support/admin/reports/agents | Raport produktywności agentów |
| GET | /support/admin/reports/sla | Raport realizacji SLA |
| GET | /support/admin/reports/csat | Raport CSAT |
| GET | /support/admin/settings/csat | Ustawienia ankiet CSAT |
| GET | /support/admin/settings/sso | Ustawienia SSO |
| GET | /support/admin/settings/two-factor | Ustawienia uwierzytelniania dwuskładnikowego |
| GET | /support/admin/settings/data-retention | Ustawienia retencji danych |
| GET | /support/admin/settings/email | Ustawienia kanału e-mail |
| GET | /support/admin/custom-objects | Obiekty niestandardowe |
| GET | /support/admin/custom-objects/{customObject}/records | Rekordy obiektów niestandardowych |
| GET | /support/admin/tickets/merge-search | Wyszukiwanie celów scalania |
| POST | /support/admin/tickets/{reference}/merge | Scalenie zgłoszenia z celem |
| GET | /support/admin/tickets/{reference}/links | Lista powiązanych zgłoszeń |
| POST | /support/admin/tickets/{reference}/links | Powiązanie zgłoszenia |
| DELETE | /support/admin/tickets/{reference}/links/{link} | Usunięcie powiązania zgłoszenia |
| GET | /support/admin/tickets/{reference}/side-conversations | Lista rozmów pobocznych |
| POST | /support/admin/tickets/{reference}/side-conversations | Rozpoczęcie rozmowy pobocznej |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/reply | Odpowiedź w rozmowie pobocznej |
| POST | /support/admin/tickets/{reference}/side-conversations/{sideConversation}/close | Zamknięcie rozmowy pobocznej |
| POST | /support/admin/macros | Utworzenie makra |
| PUT | /support/admin/macros/{macro} | Aktualizacja makra |
| DELETE | /support/admin/macros/{macro} | Usunięcie makra |

## Trasy gości

Nie wymaga uwierzytelniania. Dostęp za pomocą unikalnego tokenu.

| Metoda | URL | Opis |
| ------ | --- | ----------- |
| GET | /support/guest/create | Formularz zgłoszenia gościa |
| POST | /support/guest | Utworzenie zgłoszenia gościa |
| GET | /support/guest/{token} | Wyświetlenie zgłoszenia gościa |
| POST | /support/guest/{token}/reply | Odpowiedź na zgłoszenie gościa |
| POST | /support/guest/{token}/rate | Wysłanie oceny satysfakcji |
