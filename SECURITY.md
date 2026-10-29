# Sécurité

## Signaler une faille

Ne pas ouvrir d'issue publique. Écrire à **lounes.behloul@loudevia.fr** ou utiliser *Security > Report a vulnerability* sur GitHub, avec :

- la description de la faille et son impact ;
- les étapes pour la reproduire ;
- la version ou l'URL concernée.

Réponse sous 72 heures ouvrées.

## Bonnes pratiques du dépôt

- Secrets uniquement dans `.env.local` (ignoré par git) et dans les secrets GitHub Actions.
- Dependabot, secret scanning et push protection activés.
- Si un secret a été commité par erreur : le révoquer et le régénérer immédiatement chez le fournisseur, le supprimer de l'historique ne suffit pas.
