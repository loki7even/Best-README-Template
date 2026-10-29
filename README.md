<!--
  Modèle de README. Remplace chaque valeur entre crochets ([nom-du-projet], [client]…)
  puis supprime les sections inutiles. Le guide complet est dans TEMPLATE.md.
-->

<div align="center">
  <img src="images/logo.png" alt="Logo" width="80" height="80">

  <h1>[Nom du projet]</h1>

  <p>[Une phrase qui dit ce que fait le projet et pour qui.]</p>

  <p>
    <a href="[https://exemple.fr]"><strong>Voir le site</strong></a>
    ·
    <a href="docs/README.md">Documentation</a>
    ·
    <a href="../../issues/new?template=bug.yml">Signaler un bug</a>
    ·
    <a href="../../issues/new?template=feature.yml">Proposer une fonctionnalité</a>
  </p>

  <p>
    <a href="../../actions/workflows/ci.yml"><img src="../../actions/workflows/ci.yml/badge.svg" alt="CI"></a>
  </p>
</div>

## Sommaire

- [Aperçu](#aperçu)
- [Stack](#stack)
- [Démarrage rapide](#démarrage-rapide)
- [Commandes](#commandes)
- [Variables d'environnement](#variables-denvironnement)
- [Structure](#structure)
- [Déploiement](#déploiement)
- [Statut et feuille de route](#statut-et-feuille-de-route)
- [Contribuer](#contribuer)
- [Licence et contacts](#licence-et-contacts)

## Aperçu

[Contexte du projet en deux ou trois phrases : le client, le besoin, le résultat attendu.]

<!-- Capture d'écran : ajoute images/apercu.png puis décommente.
![Aperçu](images/apercu.png)
-->

## Stack

| Couche | Choix |
| --- | --- |
| Front | [React 19, TypeScript, Vite, Tailwind CSS 4] |
| Back / données | [Supabase, API maison, aucun…] |
| Services | [Stripe, Resend…] |
| Hébergement | [Ionos, OVH, Vercel, GitHub Pages…] |
| Qualité | [oxlint ou ESLint, TypeScript strict] |

## Démarrage rapide

Prérequis : Node.js 22 (voir `.nvmrc`) et npm.

```bash
git clone https://github.com/[utilisateur]/[nom-du-projet].git
cd [nom-du-projet]
cp .env.example .env.local   # si le projet utilise des variables
npm ci
npm run dev                  # http://localhost:5173
```

## Commandes

| Commande | Rôle |
| --- | --- |
| `npm run dev` | Serveur de développement |
| `npm run lint` | Vérification du code |
| `npm run build` | Version de production (inclut la vérification TypeScript) |
| `npm run preview` | Sert localement la version de production |

## Variables d'environnement

Toutes les variables sont listées, sans valeur secrète, dans [`.env.example`](.env.example). Ne jamais committer `.env` ou `.env.local`.

| Variable | Rôle | Où la trouver |
| --- | --- | --- |
| `[VITE_EXEMPLE]` | [À quoi elle sert] | [Tableau de bord du service] |

## Structure

```
.github/            CI, modèles d'issues et de PR, Dependabot
docs/               documentation du projet (index dans docs/README.md)
public/             fichiers servis tels quels (.htaccess, robots.txt, favicon)
src/
  assets/           images, logos
  components/       composants réutilisables
  pages/            une page par route
  lib/              utilitaires, clients de services
CLAUDE.md           consignes pour Claude Code (renvoie vers AGENTS.md)
AGENTS.md           conventions du projet pour les agents IA
```

## Déploiement

[Automatique à chaque push sur `main` via `.github/workflows/deploy.yml`.]

Secrets à créer une fois dans GitHub > Settings > Secrets and variables > Actions :

| Secret | Où le trouver |
| --- | --- |
| `[HOST]` | [Hébergeur > page SFTP / FTP] |

Exemples de workflows prêts à copier (Ionos, OVH, GitHub Pages) : [`docs/exemples-workflows/`](docs/exemples-workflows/).

## Statut et feuille de route

| Fait | À venir |
| --- | --- |
| [Fonctionnalité livrée] | [Fonctionnalité prévue] |

Le détail des versions est dans le [CHANGELOG](CHANGELOG.md).

## Contribuer

Le fonctionnement (branches, commits, pull requests) est décrit dans [CONTRIBUTING.md](CONTRIBUTING.md). Pour une faille de sécurité, voir [SECURITY.md](SECURITY.md).

## Licence et contacts

[Distribué sous licence MIT, voir `LICENSE`.] / [Code propriété de [client], tous droits réservés.]

- Développeur : [Loudevia](https://loudevia.fr), lounes.behloul@loudevia.fr
- Client : [nom, email]
- Hébergeur : [nom], compte au nom de [client]

<p align="right"><a href="#sommaire">Retour en haut</a></p>
