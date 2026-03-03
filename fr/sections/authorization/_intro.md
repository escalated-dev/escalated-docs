# Autorisation

Escalated utilise deux gates d'autorisation pour controler l'acces aux vues agent et administration. Definissez-les dans votre application pour controler qui peut gerer les tickets.

> **Remarque :** Escalated partage automatiquement `page.props.escalated` dans toutes les reponses Inertia, contenant le prefixe de route et le statut agent/admin de l'utilisateur actuel.
