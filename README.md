<div align="center">
  <img src="images/logo.png" alt="Logo" width="80" height="80">

  <h1>Modèle de projet Loudevia</h1>

  <p>Point de départ de chaque nouveau dépôt : README, CI, modèles GitHub et configuration Claude Code prêts à l'emploi.</p>
</div>

---

## Ce que contient le modèle

| Fichier | Rôle |
| --- | --- |
| [`BLANK_README.md`](BLANK_README.md) | README à remplir pour le nouveau projet (il remplace celui-ci) |
| [`AGENTS.md`](AGENTS.md) + [`CLAUDE.md`](CLAUDE.md) | Conventions du projet, lues par Claude Code et les autres agents IA |
| [`.claude/settings.json`](.claude/settings.json) | Plugins Claude conseillés et commandes autorisées sans confirmation |
| [`.mcp.json`](.mcp.json) | Serveurs MCP partagés par le dépôt (documentation à jour via Context7) |
| [`.github/workflows/ci.yml`](.github/workflows/ci.yml) | Lint, tests et build à chaque pull request et push sur `main` |
| [`.github/workflows-modeles/`](.github/workflows-modeles/) | Déploiements prêts à copier : Ionos (SFTP), OVH (FTP), Expo (EAS) |
| [`.github/ISSUE_TEMPLATE/`](.github/ISSUE_TEMPLATE/) | Formulaires de bug et de demande de fonctionnalité |
| [`.github/pull_request_template.md`](.github/pull_request_template.md) | Checklist de pull request |
| [`.github/dependabot.yml`](.github/dependabot.yml) | Mises à jour hebdomadaires des dépendances npm et des actions GitHub |
| [`docs/`](docs/) | Index de documentation et liste des outils IA par type de projet |
| `.editorconfig`, `.gitignore`, `.nvmrc`, `.env.example` | Réglages communs (Node 22, fins de ligne, fichiers ignorés, variables) |
| [`CHANGELOG.md`](CHANGELOG.md) | Journal des versions au format [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/) |
| [`SECURITY.md`](SECURITY.md) | Comment signaler une faille |

## Démarrer un nouveau projet

1. Sur GitHub, clique sur **Use this template > Create a new repository** (dépôt privé par défaut).
   Si le bouton n'apparaît pas : Settings > General > cocher **Template repository**.
2. Crée le projet dans le dépôt (par exemple `npm create vite@latest . -- --template react-ts`, `npx create-next-app@latest .` ou `npx create-expo-app@latest .`).
   Garde les fichiers du modèle si l'outil propose de les écraser.
3. Remplace ce README par le modèle : `mv BLANK_README.md README.md`, puis remplis chaque `[crochet]`.
4. Complète [`AGENTS.md`](AGENTS.md) (stack, structure, conventions propres au projet).
5. Copie le workflow de déploiement voulu de `.github/workflows-modeles/` vers `.github/workflows/deploy.yml` et crée ses secrets.
6. Protège la branche `main` (Settings > Branches) : pull request obligatoire et CI verte.
7. Ajoute le projet au registre de la [bibliothèque Loudevia](https://github.com/loki7even/LOUDEVIA/blob/main/docs/README.md).

Pour un projet client, remplace ou supprime `LICENSE.txt` selon le contrat.

## Bonnes pratiques retenues

- **Tout en français** dans la documentation, les commentaires et les commits ; identifiants de code en anglais.
- **README court et actionnable** : démarrage en moins de 5 minutes, tableaux plutôt que longs paragraphes, détail renvoyé dans `docs/`.
- **`npm ci`** partout (local et CI) pour des installations reproductibles depuis le `package-lock.json`.
- **Secrets** : jamais dans le dépôt. `.env.example` liste les variables sans valeur, les vraies valeurs vont dans GitHub > Settings > Secrets.
- **Déploiement** : uniquement depuis `main`, via un workflow qui ignore proprement l'étape si les secrets manquent.
- **Une branche par fonctionnalité**, fusionnée par pull request avec la CI au vert.
- **Agents IA** : les conventions vivent dans `AGENTS.md`, que Claude Code lit automatiquement via `CLAUDE.md`.

## Outils IA

La liste des connecteurs MCP, plugins et skills conseillés selon le type de projet (site vitrine, Next.js + Supabase + Stripe, application Expo) est dans [docs/outils-claude.md](docs/outils-claude.md).

## Crédits

Inspiré du [Best-README-Template](https://github.com/othneildrew/Best-README-Template) d'Othneil Drew (licence MIT, voir [`LICENSE.txt`](LICENSE.txt)), entièrement réécrit en 2026.
