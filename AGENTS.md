# Conventions du projet

Ce fichier est lu par Claude Code (via `CLAUDE.md`) et par les autres agents IA.
Garde-le court : uniquement ce qu'un nouvel arrivant ne peut pas deviner en lisant le code.

## Le projet

[Une phrase sur le projet.] Voir `README.md` pour le démarrage et `docs/` pour le détail.

## Stack

[React 19, TypeScript, Vite, Tailwind CSS 4, React Router.]

## Structure

- `src/components` : composants réutilisables, un fichier par composant.
- `src/pages` : une page par route.
- `src/lib` : clients d'API, utilitaires sans interface.
- `src/i18n` : textes de l'interface (jamais de texte en dur si le site est bilingue).

## Conventions

- Composants en `PascalCase`, hooks en `useCamelCase`, fichiers utilitaires en `camelCase`.
- Commentaires et documentation en français, identifiants en anglais.
- Pas de `any` en TypeScript sans commentaire qui justifie.
- [Style : Tailwind / CSS Modules — en choisir un et s'y tenir.]

## Commandes

- `npm run dev` : serveur local.
- `npm run lint` : à lancer avant chaque commit.
- `npm run build` : inclut la vérification TypeScript ; doit passer avant toute pull request.
- `npm test` : [si des tests existent].

## Sécurité

- Aucune clé secrète côté client : les variables `VITE_`, `NEXT_PUBLIC_` et `EXPO_PUBLIC_` sont publiques.
- Ne jamais committer `.env` ou `.env.local`. Ajouter toute nouvelle variable à `.env.example`, sans valeur.

## Git

- Branche `main` protégée, une branche par fonctionnalité, fusion par pull request.
- Messages de commit en français, à l'impératif : « Ajoute le formulaire de contact ».
- Mettre à jour `CHANGELOG.md` (section « Non publié ») à chaque changement visible.
