# Autorisatie

Escalated gebruikt twee autorisatiegates om de toegang tot agent- en beheerweergaven te regelen. Definieer deze in je applicatie om te bepalen wie tickets kan beheren.

> **Let op:** Escalated deelt automatisch `page.props.escalated` met alle Inertia-responses, met daarin het routevoorvoegsel en de agent-/beheerderstatus van de huidige gebruiker.
