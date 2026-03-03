# Powiadomienia

Escalated wykorzystuje natywny system powiadomień Twojego frameworka. Powiadomienia e-mail i bazodanowe są wysyłane automatycznie dla kluczowych zdarzeń, takich jak nowe zgłoszenia, odpowiedzi, przypisania, zmiany statusu i naruszenia SLA.

- Przypisany agent powiadamiany o nowych odpowiedziach
- Zgłaszający powiadamiany o odpowiedziach agentów i zmianach statusu
- **Obserwujący zgłoszenie** otrzymują te same powiadomienia co przypisany agent -- odpowiedzi i zmiany statusu
- Alerty o naruszeniu SLA wysyłane do przypisanego agenta i członków działu

Dostosuj szablony e-mail, publikując widoki: `php artisan vendor:publish --tag=escalated-views`
