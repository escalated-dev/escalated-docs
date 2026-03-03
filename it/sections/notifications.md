# Notifiche

Escalated utilizza il sistema di notifiche nativo del tuo framework. Le notifiche via email e database vengono inviate automaticamente per gli eventi chiave come nuovi ticket, risposte, assegnazioni, cambi di stato e violazioni SLA.

- L'assegnatario del ticket viene notificato per le nuove risposte
- Il richiedente viene notificato per le risposte degli agenti e i cambi di stato
- I **follower del ticket** ricevono le stesse notifiche dell'assegnatario -- risposte e cambi di stato
- Gli avvisi di violazione SLA vengono inviati all'assegnatario e ai membri del dipartimento

Personalizza i template email pubblicando le view: `php artisan vendor:publish --tag=escalated-views`
