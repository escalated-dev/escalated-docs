# Przychodzące e-maile

Twórz i odpowiadaj na zgłoszenia bezpośrednio z przychodzących wiadomości e-mail. Escalated obsługuje webhooki **Mailgun**, **Postmark**, **AWS SES** oraz odpytywanie **IMAP** jako rozwiązanie zapasowe.

## Jak to działa

1. Twój dostawca e-mail otrzymuje wiadomość na Twój adres wsparcia (np. `support@yourapp.com`)
2. Dostawca przekazuje ją do Twojej aplikacji przez webhook (lub odpytywanie IMAP ją pobiera)
3. Escalated normalizuje dane i sprawdza dopasowanie wątku przez referencję w temacie (np. `[ESC-00001]`) lub nagłówki `In-Reply-To`
4. Dopasowane e-maile dodają odpowiedź; niedopasowane tworzą nowe zgłoszenie (lub zgłoszenie gościa dla nieznanych nadawców)

## Konfiguracja

Włącz przychodzące e-maile i skonfiguruj adapter w ustawieniach administracyjnych lub przez zmienne środowiskowe. Ustawienia administracyjne mają priorytet nad wartościami env/config.

## Adresy URL webhooków

Skieruj webhook przychodzący Twojego dostawcy e-mail na te adresy URL. Te trasy nie wymagają uwierzytelniania (używają zamiast tego weryfikacji podpisu).

| Dostawca | Adres URL webhooka |
| --- | --- |
| Mailgun | `POST /support/inbound/mailgun` |
| Postmark | `POST /support/inbound/postmark` |
| AWS SES | `POST /support/inbound/ses` |

## Odpytywanie IMAP

Dla dostawców e-mail bez obsługi webhooków użyj komendy odpytywania IMAP w harmonogramie.

## Funkcje

- **Wykrywanie wątków** przez referencję w temacie i nagłówki In-Reply-To / References
- **Zgłoszenia gości** dla nieznanych nadawców z automatycznie ustalanymi nazwami wyświetlanymi
- **Automatyczne ponowne otwarcie** rozwiązanych lub zamkniętych zgłoszeń, gdy odpowiedź przychodzi e-mailem
- **Wykrywanie duplikatów** przez nagłówki Message-ID, aby zapobiec podwójnemu przetwarzaniu
- **Obsługa załączników** z konfigurowalnymi limitami rozmiaru i liczby
- **Logowanie audytu** -- każdy przychodzący e-mail jest rejestrowany do celów debugowania i zgodności
- **Konfiguracja administracyjna** -- wszystkie ustawienia zarządzane z panelu administracyjnego z fallbackiem na env/config
