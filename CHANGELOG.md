# Changelog

Toutes les évolutions notables du projet sont notées ici.
Format : [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/), versions : [Semantic Versioning](https://semver.org/lang/fr/).

## [Non publié]

### Ajouté
- `docs/lecons-projets.md` : leçons de tous les projets (déploiement, offres gratuites, secrets, mobile, paiement).
- `docs/quota-github-actions.md` : quota de minutes partagé, règles pour l'économiser, déploiement à la main.
- `docs/ftp-sftp-filezilla.md` : FileZilla pour OVH et Ionos (configuration, envoi manuel, fichier d'état de l'action FTP, pièges).
- Section « Déploiement à la main » dans `docs/02-deploiement.md` et section « GitHub Actions et serveurs » dans `CLAUDE.md`.

### Modifié
- Branche principale renommée `master` → `main`, comme tous les dépôts Loudevia.
- `CLAUDE.md` contient désormais toutes les consignes (format des dépôts récents) ; `AGENTS.md` renvoie vers lui.
- `.claude/settings.json` active les plugins officiels (code-review, security-guidance, frontend-design, context7, commit-commands, claude-md-management).
- CI déclenchée sur `main` seulement.
- CI et exemples de déploiement : `timeout-minutes: 10` ; déploiements ignorés quand seule la doc change ; exemple OVH en FTPS avec interrupteur `OVH_DEPLOY`.
- CI : le workflow échouait au démarrage depuis la version 2.0.0 (`hashFiles()` dans le `env` du job, non permis) ; le test du `package-lock.json` passe dans chaque étape.
- Tableau des effets d'un merge : Kizuna-Sekai passe chez OVH, ajout de post-a-thought.

## [2.0.0] - 2026-10-29

### Ajouté
- Configuration GitHub : CI (lint et build), modèles d'issues et de pull request, Dependabot, CODEOWNERS.
- `AGENTS.md`, `CLAUDE.md` et `.claude/settings.json` pour les agents IA.
- `CONTRIBUTING.md` (branches, Conventional Commits, squash merge) et `SECURITY.md`.
- `.editorconfig`, `.gitignore` (Node, Vite, Next.js, Expo), `.env.example`, `.nvmrc` (Node 22).
- Exemples de workflows de déploiement : Ionos (SFTP), OVH (FTP), GitHub Pages.
- Guide d'utilisation du modèle (`TEMPLATE.md`) et index de documentation (`docs/`).

### Modifié
- README réécrit en français, au format des projets Loudevia (stack, commandes, variables, déploiement, statut).
- `LICENSE.txt` renommé en `LICENSE`.

### Supprimé
- `BLANK_README.md` (fusionné dans le README) et la capture d'écran d'exemple.

## [1.0.0]

Version d'origine du [Best-README-Template](https://github.com/othneildrew/Best-README-Template).
