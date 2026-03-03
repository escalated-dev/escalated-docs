# Autorisierung

Escalated verwendet zwei Autorisierungs-Gates zur Steuerung des Zugriffs auf Agenten- und Admin-Ansichten. Definieren Sie diese in Ihrer Anwendung, um festzulegen, wer Tickets verwalten darf.

> **Hinweis:** Escalated teilt automatisch `page.props.escalated` mit allen Inertia-Antworten, einschließlich des Routenpräfixes und des Agenten-/Admin-Status des aktuellen Benutzers.
