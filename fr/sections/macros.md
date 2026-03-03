# Macros

Les macros sont des sequences d'actions reutilisables que les agents peuvent appliquer a un ticket en un seul clic. Une seule macro peut changer le statut, definir la priorite, assigner un agent, ajouter une reponse et bien plus -- le tout en une fois.

## Actions des macros

Chaque macro contient une ou plusieurs actions qui s'executent dans l'ordre :

- **Changer le statut** -- definir le statut du ticket
- **Changer la priorite** -- definir la priorite du ticket
- **Assigner un agent** -- assigner le ticket a un agent specifique
- **Changer le departement** -- deplacer le ticket vers un departement
- **Ajouter des etiquettes** -- appliquer des etiquettes au ticket
- **Envoyer une reponse** -- ajouter une reponse publique a la conversation
- **Ajouter une note** -- ajouter une note interne visible uniquement par les agents

## Macros partagees vs. personnelles

- Les **macros partagees** sont visibles par tous les agents et gerees par les administrateurs
- Les **macros personnelles** sont visibles uniquement par l'agent qui les a creees

Les administrateurs gerent les macros depuis la page `Admin -> Macros`. Le constructeur d'actions permet d'ajouter, de reordonner et de configurer chaque etape visuellement.
