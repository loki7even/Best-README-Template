# Changelog

Toutes les évolutions notables du projet sont notées ici.
Format : [Keep a Changelog](https://keepachangelog.com/fr/1.1.0/), versions : [Semantic Versioning](https://semver.org/lang/fr/).

## [Non publié]

### Ajouté (19 novembre 2026, économie de tokens)
- `docs/erreurs-connues.md` : registre des erreurs du projet (symptôme, cause, correctif), lu avant tout débogage et complété dès qu'une erreur est corrigée.
- Section « Erreurs et économie de contexte » dans `CLAUDE.md` : registre, `CLAUDE.md` sous 150 lignes, une tâche par session, sous-agent Explore pour les recherches larges.
- Case « erreur ajoutée au registre » dans le modèle de PR.

### Modifié (19 novembre 2026)
- Règle de base : tout déploiement à la demande, jamais à la fusion ni planifié ; les exemples de workflows n'ont plus de bloc `push` commenté.

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
- Mise en ligne à la demande par défaut (exemples de déploiement en `workflow_dispatch`, bloc `push` commenté), CI seulement sur les PR, Dependabot npm mensuel : reprise des décisions du 19 novembre 2026 sur LOUDEVIA.
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
