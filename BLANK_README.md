<!--
  Modèle de README. Remplace chaque [crochet] et supprime les sections inutiles.
  Règle d'or : quelqu'un qui découvre le dépôt doit pouvoir lancer le projet
  en moins de 5 minutes en lisant uniquement ce fichier.
-->

<div align="center">
  <img src="images/logo.png" alt="Logo [Nom du projet]" width="80" height="80">

  <h1>[Nom du projet]</h1>

  <p>[Une phrase : ce que fait le projet et pour qui.]</p>

  <p>
    <a href="https://exemple.fr"><strong>Voir en ligne</strong></a>
    ·
    <a href="docs/README.md">Documentation</a>
    ·
    <a href="https://github.com/[utilisateur]/[depot]/issues/new?template=bug.yml">Signaler un bug</a>
  </p>

  <!-- Badges : remplace [utilisateur]/[depot]. Supprime ceux qui ne servent pas. -->
  <a href="https://github.com/[utilisateur]/[depot]/actions/workflows/ci.yml"><img src="https://github.com/[utilisateur]/[depot]/actions/workflows/ci.yml/badge.svg" alt="CI"></a>
</div>

---

## Sommaire

- [Le projet](#le-projet)
- [Stack](#stack)
- [Démarrage rapide](#démarrage-rapide)
- [Commandes](#commandes)
- [Variables d'environnement](#variables-denvironnement)
- [Structure](#structure)
- [Déploiement](#déploiement)
- [Documentation](#documentation)
- [Statut et feuille de route](#statut-et-feuille-de-route)
- [Contacts](#contacts)
- [Journal du projet](#journal-du-projet)

## Le projet

![Capture d'écran](images/screenshot.png)

[Deux ou trois phrases : le contexte, le problème résolu, le public visé.]

| | |
| --- | --- |
| Client | [Nom du client] |
| Type | [Site vitrine / e-commerce / application mobile / plateforme] |
| Production | [https://exemple.fr](https://exemple.fr) |
| Langues | [FR / EN] |

## Stack

[React 19](https://react.dev) · [TypeScript](https://www.typescriptlang.org) · [Vite](https://vite.dev) · [Tailwind CSS 4](https://tailwindcss.com) · [React Router](https://reactrouter.com)

<!-- Exemples d'autres stacks utilisées :
  Next.js 16 · Supabase (Postgres, Auth, Storage) · Stripe · Resend · Vercel
  Expo (React Native) · Expo Router · Firebase · EAS Build
-->

## Démarrage rapide

Prérequis : [Node.js](https://nodejs.org) 22 (voir `.nvmrc`).

```bash
npm ci           # installe les dépendances exactes du package-lock.json
cp .env.example .env.local
npm run dev      # http://localhost:5173
```

[Si le projet tourne sans configuration (données de démonstration, mode mock), le dire ici.]

## Commandes

| Commande | Effet |
| --- | --- |
| `npm run dev` | Serveur de développement avec rechargement à chaud |
| `npm run lint` | Analyse statique du code (oxlint ou ESLint) |
| `npm run build` | Vérifie les types puis construit la version de production dans `dist/` |
| `npm run preview` | Sert la version construite en local |
| `npm test` | Lance les tests (Vitest) |

## Variables d'environnement

Copie `.env.example` en `.env.local`. Ne jamais committer de vraie valeur secrète.

| Variable | Rôle | Où la trouver | Secrète ? |
| --- | --- | --- | --- |
| `VITE_EXEMPLE_URL` | [URL de l'API] | [Tableau de bord du service] | Non (publique) |
| `EXEMPLE_SECRET_KEY` | [Clé serveur] | [Tableau de bord du service] | **Oui**, serveur uniquement |

> Toute variable préfixée `VITE_`, `NEXT_PUBLIC_` ou `EXPO_PUBLIC_` est visible par tout le monde dans le navigateur ou l'application.

## Structure

```
src/
  assets/        images, logos
  components/    composants réutilisables (Header, Footer, boutons…)
  pages/         une page par route
  i18n/          fr.ts, en.ts (si bilingue)
  lib/           clients d'API, utilitaires
  App.tsx
  main.tsx
public/          fichiers servis tels quels (robots.txt, sitemap.xml, .htaccess)
docs/            documentation détaillée
```

## Déploiement

[Choisir et adapter :]

- **Automatique** : chaque push sur `main` construit et publie le site (`.github/workflows/deploy.yml`).
- **Hébergeur** : [Ionos / OVH / Vercel / EAS]. Secrets GitHub nécessaires :

| Secret | Où le trouver |
| --- | --- |
| `[HEBERGEUR]_HOST` | [Espace client > Hébergement > SFTP] |
| `[HEBERGEUR]_USER` | [même page] |
| `[HEBERGEUR]_PASSWORD` | [même page] |
| `[HEBERGEUR]_DIR` | [dossier relié au domaine, jamais `/`] |

## Documentation

| Document | Contenu |
| --- | --- |
| [docs/README.md](docs/README.md) | Index de la documentation |
| [AGENTS.md](AGENTS.md) | Conventions du projet (lues aussi par Claude et les autres agents IA) |
| [CHANGELOG.md](CHANGELOG.md) | Historique des versions |

## Statut et feuille de route

| Fait | À faire |
| --- | --- |
| [Fonctionnalité livrée] | [Fonctionnalité prévue] |

## Contacts

| Rôle | Contact |
| --- | --- |
| Développement | Loudevia, [lounes.behloul@loudevia.fr](mailto:lounes.behloul@loudevia.fr) |
| Client | [Nom, email] |
| Hébergeur | [Nom], compte au nom de [titulaire] |

## Journal du projet

| Date | Événement | Détail |
| --- | --- | --- |
| [AAAA-MM-JJ] | Création du dépôt | À partir du modèle Loudevia |
