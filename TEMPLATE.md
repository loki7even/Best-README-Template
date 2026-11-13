# Utiliser ce modèle

Ce dépôt est le point de départ de tous les nouveaux projets. Il fournit un README à remplir, la configuration GitHub (CI, modèles d'issues et de PR, Dependabot), les consignes pour Claude Code et la documentation de base. Il ne contient pas de code applicatif : le code se crée par-dessus (Vite, Next.js, Expo…).

Pour le déroulé complet d'un projet client (devis, maquettes, mise en ligne, maintenance), suivre aussi les modèles de la bibliothèque Loudevia : `docs/modeles/modele-site-web.md` et `docs/modeles/modele-application.md` du dépôt Loudevia.

## 1. Créer le dépôt

1. Sur GitHub, ouvrir ce dépôt puis **Use this template > Create a new repository**.
2. Nommer le dépôt, le laisser **privé** par défaut.
3. Cloner le nouveau dépôt.

## 2. Ajouter le code

Générer le projet dans le dossier cloné, puis garder les fichiers du modèle quand l'outil propose de les écraser :

```bash
# Site vitrine (React + Vite + TypeScript + Tailwind)
npm create vite@latest . -- --template react-ts
npm install
npm install -D tailwindcss @tailwindcss/vite oxlint

# Application web avec back-end (Next.js)
npx create-next-app@latest . --ts --app --eslint

# Application mobile (Expo)
npx create-expo-app@latest .
```

Vérifier que `package.json` contient bien les scripts `lint` et `build` : la CI les lance automatiquement dès qu'un `package-lock.json` existe.

## 3. Personnaliser

- [ ] `README.md` : remplacer tous les `[crochets]`, supprimer les sections inutiles
- [ ] `images/logo.png` : remplacer par le logo du projet
- [ ] `CLAUDE.md` : remplacer les `[crochets]` (projet, structure, stack, règles propres)
- [ ] `.env.example` : lister les variables (sans valeurs)
- [ ] `LICENSE` : garder MIT pour un projet open source, sinon remplacer par une mention « tous droits réservés » au nom du client
- [ ] `.github/CODEOWNERS` : vérifier le propriétaire
- [ ] `.github/ISSUE_TEMPLATE/config.yml` : remplacer `Best-README-Template` par le nom du nouveau dépôt dans le lien de sécurité
- [ ] `CHANGELOG.md` : repartir d'une section `[Non publié]` vide
- [ ] Déploiement : copier le workflow voulu depuis `docs/exemples-workflows/` vers `.github/workflows/deploy.yml` et créer les secrets
- [ ] Dépendances : ajouter le dépôt au tableau « Ce qu'un merge sur `main` déclenche » du guide `docs/maintenance-dependances.md` dans Best-README-Template, et compléter la ligne Dépendances de `CLAUDE.md`
- [ ] Supprimer ce fichier `TEMPLATE.md`

## 4. Réglages GitHub (une fois par dépôt)

- **Settings > Branches** : règle sur `main`, pull request obligatoire, check `CI` obligatoire.
- **Settings > General** : branche par défaut `main` (sinon Dependabot n'ouvre aucune PR) ; activer *Automatically delete head branches* et *Allow squash merging* (désactiver les autres modes pour un historique propre).
- **Settings > Code security** : activer Dependabot alerts, secret scanning et push protection.
- **Settings > Secrets and variables > Actions** : secrets de déploiement.

## 5. Outils IA

- `CLAUDE.md` contient toutes les consignes (structure, commandes, conventions, sécurité). `AGENTS.md` renvoie vers lui pour les autres agents (Codex, Copilot, Cursor…). Pour un projet Next.js, `next dev` peut ajouter un bloc dans `AGENTS.md` : le garder.
- `.claude/settings.json` active les plugins officiels (`code-review`, `security-guidance`, `frontend-design`, `context7`…) dès l'ouverture du dépôt dans Claude Code, et autorise sans confirmation les commandes sûres (`npm run lint`, `npm run build`, `git status`…). Les ajouts personnels vont dans `.claude/settings.local.json`, ignoré par git.
- Dans Claude Code, `/init` peut compléter `CLAUDE.md` une fois le code généré. Ajouter un plugin propre au projet dans `enabledPlugins` (par exemple `firebase@claude-plugins-official`).
