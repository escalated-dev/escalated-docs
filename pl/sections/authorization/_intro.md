# Autoryzacja

Escalated używa dwóch bramek autoryzacyjnych do kontroli dostępu do widoków agentów i administratorów. Zdefiniuj je w swojej aplikacji, aby kontrolować, kto może zarządzać zgłoszeniami.

> **Uwaga:** Escalated automatycznie udostępnia `page.props.escalated` we wszystkich odpowiedziach Inertia, zawierając prefiks tras oraz status agenta/administratora bieżącego użytkownika.
