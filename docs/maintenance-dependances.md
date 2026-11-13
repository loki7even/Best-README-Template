# Maintenance des dépendances (Dependabot)

Guide commun à tous les projets de Lounes. Il se donne tel quel à la session Claude chargée de la maintenance d'un dépôt, et vaut aussi pour un humain. Chaque dépôt garde dans son `CLAUDE.md` une ligne qui renvoie ici et dit ce qu'un merge sur `main` déclenche chez lui.

## Contexte

- **Dependabot** est le robot de GitHub qui ouvre une PR à chaque nouvelle version d'une bibliothèque. Il est réglé dans `.github/dependabot.yml` :
  - npm chaque lundi, les versions mineures et correctives regroupées dans une seule PR « mineures-et-correctifs » ;
  - GitHub Actions une fois par mois (et cargo ou pip une fois par mois quand le dépôt en contient).
- Dependabot ne travaille que sur la **branche par défaut** du dépôt. Si elle n'est pas `main`, aucune PR n'arrive : la changer dans Settings > General.
- **Un merge sur `main` peut mettre le site en ligne.** Vérifier dans le tableau plus bas ce que déclenche le dépôt avant de merger.
- Ne jamais toucher aux PR de travail ouvertes par les autres sessions (branches `claude/...`), seulement à celles de `dependabot[bot]`.
- Un dépôt peut avoir ses propres règles en plus (exemple : LOUDEVIA, dont Lounes gère lui-même les PR Dependabot). Elles priment sur ce guide.

## Ce qu'un merge sur `main` déclenche

| Dépôt | Effet d'un merge sur `main` |
| --- | --- |
| LOUDEVIA | Déploiement Ionos (site, Hub `/espace`, API PHP) ; PR Dependabot gérées par Lounes |
| GazelleTransports | Déploiement OVH par FTP (site client) |
| LAGames | Déploiement Ionos par SFTP, dossier `/lagames` (site client) |
| Kizuna-Sekai | Déploiement Vercel |
| Cetavi | Déploiement Vercel |
| pharmahub | Déploiement Vercel |
| WTFast (BlindzRun) | Rien : l'application part par un build EAS lancé à la main |
| AmiDo | Rien : le site tourne en local |

Un nouveau projet ajoute sa ligne ici au démarrage.

## Routine (chaque lundi après le passage de Dependabot)

1. Lister les PR ouvertes dont l'auteur est `dependabot[bot]`.
2. Pour chacune, relever : le type de mise à jour (correctif, mineure, majeure), les dossiers touchés, l'état de la CI et l'absence de conflit.
3. Classer chaque PR, puis agir comme indiqué :

| Cas | Action |
| --- | --- |
| Correctif ou mineure, CI verte, sans conflit | Merger (méthode « merge », ou « squash » si le dépôt n'autorise que celle-là), une PR à la fois |
| Mise à jour d'une action GitHub (`ci: bump actions/...`), CI verte | Merger |
| Pip : seul le plancher monte (`>=x`), CI verte | Merger |
| Majeure, ou paquet en `0.x` dont le deuxième chiffre change | Ne pas merger. Lire les notes de version, tester à la main (voir plus bas), puis demander à Lounes |
| CI rouge | Ne pas merger. Chercher la cause dans les journaux. Si la mise à jour ne passe pas sans changer le code, fermer la PR et le signaler |
| Conflit | Commenter `@dependabot rebase`. Si un autre commit a été poussé sur la branche, refaire la mise à jour dans une PR à soi et fermer celle de Dependabot |

4. Vérifier `main` après les merges : tous les workflows au vert sur le dernier commit, déploiement compris.
5. Faire un bilan court à Lounes : ce qui est mergé, ce qui est fermé, ce qui attend son avis et pourquoi.

## Vérifier une mise à jour à la main

Sur une branche qui réunit `main` et la ou les PR, lancer les commandes du `CLAUDE.md` du dépôt, en général :

```bash
npm ci && npm run lint && npm run build
```

Pour une majeure qui touche l'affichage, ouvrir aussi les pages concernées (aperçu Vercel de la PR ou `npm run dev`).

## Versions majeures écartées

Le bloc `ignore` de `.github/dependabot.yml` empêche Dependabot de proposer certaines majeures. Les revoir environ tous les trois mois, et retirer la ligne une fois la mise à jour faite à la main.

| Paquet | Où | Raison (2026-11-13) |
| --- | --- | --- |
| typescript 7 | Tous les dépôts | Nouveau compilateur entièrement refait, encore instable : attendre qu'il mûrisse |
| @types/node (majeure) | Tous les dépôts | Doit suivre la version de Node de la CI, pas la dernière parue |
| vite, @vitejs/plugin-react, react, react-dom, @types/react, @types/react-dom (majeures) | GazelleTransports | Les PR échouaient à l'installation (conflit de dépendances) : migration à faire à la main |
| expo, expo-\*, react-native, react-native-\*, react, react-dom | WTFast | Se mettent à jour ensemble avec `npx expo install --fix` |

Bloc à copier dans l'entrée npm de `.github/dependabot.yml` :

```yaml
    ignore:
      - dependency-name: "typescript"
        update-types: ["version-update:semver-major"]
      - dependency-name: "@types/node"
        update-types: ["version-update:semver-major"]
```

## Pièges connus

- Deux PR qui modifient le même fichier (souvent un workflow, par exemple `actions/setup-node` et `actions/checkout`) entrent en conflit après le premier merge. Commenter `@dependabot rebase` sur la seconde et attendre la CI.
- Un workflow qui pousse des commits sur toutes les branches (captures d'écran, formatage) empêche Dependabot de rebaser. Exclure les branches `dependabot/**` de ce workflow.
- Merger plusieurs PR coup sur coup annule les déploiements intermédiaires quand le workflow a une règle de concurrence. Seul le dernier compte, il doit être vert.
- Depuis un conteneur cloud, le site en ligne peut être bloqué par le proxy. Dans ce cas, demander à Lounes de vérifier le site.
