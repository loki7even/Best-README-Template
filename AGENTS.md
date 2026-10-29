# Consignes pour les agents IA

Ce fichier est lu par Claude Code (via `CLAUDE.md`) et par les autres agents. Le compléter dès que le projet a une stack.

## Projet

[Nom du projet] : [ce que fait le projet en une phrase]. Documentation complète dans `docs/README.md`.

## Stack et structure

- **Stack** : [React 19, TypeScript, Vite, Tailwind CSS 4 / Next.js / Expo…]
- **Structure** : [`src/pages` une page par route, `src/components` composants réutilisables, `src/lib` utilitaires et clients de services…]
- **Style** : [Tailwind / CSS Modules à côté du composant…]

## Commandes

- `npm run dev` : serveur local
- `npm run lint` : à lancer avant chaque commit
- `npm run build` : doit passer avant d'ouvrir une pull request (inclut la vérification TypeScript)

## Conventions

- Composants en `PascalCase`, hooks en `useCamelCase`, fichiers utilitaires en `camelCase`.
- Identifiants et noms de fichiers en anglais, commentaires et documentation en français.
- Textes affichés dans les fichiers de langue (`src/i18n/`) si le site est bilingue, jamais en dur.
- Commits au format Conventional Commits (`feat:`, `fix:`, `docs:`…), voir `CONTRIBUTING.md`.
- Une branche et une pull request par changement ; ne jamais pousser directement sur `main`.

## Sécurité

- Aucun secret dans le code ni dans un fichier commité : uniquement dans `.env.local` (ignoré) et dans les secrets GitHub.
- Toute nouvelle variable d'environnement est ajoutée, sans valeur, à `.env.example`.
- Les clés serveur (Supabase service role, Stripe secret…) ne s'utilisent que côté serveur, jamais dans un composant client ni une variable `VITE_` / `NEXT_PUBLIC_`.

## Points d'attention

- [Règle propre au projet, piège connu, fichier à ne pas toucher…]
