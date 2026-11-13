# [Nom du projet] : consignes pour Claude

[Ce que fait le projet en une phrase, pour qui.] Tout est rédigé en français, ton direct, phrases complètes. Documentation complète dans [docs/README.md](docs/README.md).

## Structure

| Chemin | Rôle |
| --- | --- |
| `src/pages/` | [Une page par route] |
| `src/components/` | [Composants réutilisables, CSS à côté du composant si pas de Tailwind] |
| `src/lib/` | [Utilitaires et clients de services (Supabase, Stripe…)] |
| `src/i18n/` | [Textes affichés si le site est bilingue : jamais de texte en dur] |
| `docs/` | Documentation du projet, numérotée (`01-architecture.md`…) |

Stack : [React 19, TypeScript, Vite, Tailwind CSS 4 / Next.js / Expo…]. Hébergement : [Ionos / OVH / Vercel / EAS].

## Commandes

```bash
npm ci
npm run dev
npm run lint     # à lancer avant chaque commit
npm run build    # à faire passer avant chaque PR (la CI lance lint + build)
```

## Conventions

- Composants en `PascalCase`, hooks en `useCamelCase`, fichiers utilitaires en `camelCase`.
- Identifiants et noms de fichiers en anglais, commentaires et documentation en français.
- Commits au format Conventional Commits (`feat:`, `fix:`, `docs:`…), voir `CONTRIBUTING.md`.
- Une branche et une pull request par changement ; ne jamais pousser directement sur `main`.
- Dépendances : les PR Dependabot suivent [docs/maintenance-dependances.md](docs/maintenance-dependances.md) (mineures fusionnées à CI verte, une par une ; majeures soumises à Lounes). [Ce qu'un merge sur `main` déclenche : déploiement chez …, ou rien.]
- Toute nouvelle page est privée par défaut (noindex, hors menu et sitemap) jusqu'à ce que Lounes demande de la rendre publique.

## Sécurité

- Aucun secret dans le code ni dans un fichier commité : uniquement dans `.env.local` (ignoré) et dans les secrets GitHub ou de l'hébergeur.
- Toute nouvelle variable d'environnement est ajoutée, sans valeur, à `.env.example`.
- Les clés serveur (Supabase service role, Stripe secret…) ne s'utilisent que côté serveur, jamais dans un composant client ni une variable `VITE_` / `NEXT_PUBLIC_`.
- Changement de schéma Supabase : skill `supabase-migration`. Avant une mise en ligne : skill `site-mise-en-ligne`.

## Règles propres au projet

- [Piège connu, fichier à ne pas toucher, décision à respecter…]
