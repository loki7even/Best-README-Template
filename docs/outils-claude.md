# Outils Claude conseillés

Connecteurs MCP, plugins et skills qui accélèrent le développement, classés par type de projet.
Les connecteurs s'activent une fois pour toutes dans claude.ai > Paramètres > Connecteurs ; les plugins s'installent depuis le catalogue claude.ai ou dans Claude Code avec `/plugin`.

## Déjà configuré dans ce dépôt

| Outil | Où | Rôle |
| --- | --- | --- |
| Context7 (MCP) | `.mcp.json` | Documentation à jour des librairies (React, Next.js, Expo, Tailwind…), évite le code basé sur d'anciennes versions |
| frontend-design | `.claude/settings.json` | Interfaces plus soignées et moins génériques |
| security-guidance | `.claude/settings.json` | Alerte sur les secrets en dur, XSS, injections pendant que Claude code |
| code-review | `.claude/settings.json` | `/code-review` sur une pull request |

## Selon le type de projet

| Type | Connecteurs | Plugins | Pourquoi |
| --- | --- | --- | --- |
| **Tous** | GitHub, Context7 | frontend-design, security-guidance, code-review, playwright | Issues et PR, doc à jour, revue, tests dans un vrai navigateur |
| **Site vitrine** (Vite, Ionos / OVH) | Figma (si maquettes) | playwright | Contrôle visuel 360 / 768 / 1 280 px, liens, formulaires avant mise en ligne |
| **Next.js + Supabase + Stripe + Resend** (Vercel) | Supabase, Stripe, Resend, Vercel, Sentry | supabase, stripe | Migrations et RLS, paiements et webhooks, e-mails, déploiements et logs |
| **Application Expo** (Firebase ou Supabase) | Expo, Sentry | expo, firebase ou supabase | Builds EAS, soumission aux stores, crashs, règles Firestore |
| **Stockage de fichiers / CDN** | Cloudflare | | Buckets R2, Workers, DNS |

## Pour l'activer dans un projet

- **Plugin partagé par tout le dépôt** : l'ajouter à `enabledPlugins` dans `.claude/settings.json`, par exemple `"supabase@claude-plugins-official": true`.
- **Serveur MCP partagé** : l'ajouter à `.mcp.json`. Ne jamais y écrire de clé : utiliser `${NOM_VARIABLE}`, lue depuis l'environnement.
- **Réglage personnel** : `.claude/settings.local.json` (ignoré par git).
