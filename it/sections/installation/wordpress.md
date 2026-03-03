## 1. Installare il plugin

```bash
$ wp plugin install escalated --activate
```

## 2. Configurare le impostazioni

Vai su **Escalated -> Settings** in wp-admin per configurare dipartimenti, policy SLA, regole di escalation e canali email.

## 3. Aggiungere gli shortcode

Inserisci gli shortcode in qualsiasi pagina per offrire ai clienti un portale di supporto:

```shortcodes
[escalated_tickets]        // Lista ticket
[escalated_create_ticket]  // Form nuovo ticket
[escalated_view_ticket]    // Dettaglio ticket
```

> **Nota:** Il plugin WordPress è autonomo -- non utilizza Inertia.js. Tutta l'interfaccia è renderizzata tramite le schermate native dell'admin WordPress e i template frontend basati su shortcode.
