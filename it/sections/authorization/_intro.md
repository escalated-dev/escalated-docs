# Autorizzazione

Escalated utilizza due gate di autorizzazione per controllare l'accesso alle viste agente e admin. Definiscili nella tua applicazione per controllare chi può gestire i ticket.

> **Nota:** Escalated condivide automaticamente `page.props.escalated` in tutte le risposte Inertia, contenendo il prefisso delle route e lo stato agente/admin dell'utente corrente.
