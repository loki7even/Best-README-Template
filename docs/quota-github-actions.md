# Quota GitHub Actions et déploiement à la main

Guide commun à tous les projets de Lounes. Leçon tirée de novembre 2026 : les constructions des installeurs Atelier et Formateur (Windows et macOS) du dépôt LOUDEVIA ont épuisé le quota mensuel du compte, ce qui a bloqué la CI et les déploiements de **tous** les dépôts privés en même temps.

## Ce qu'il faut savoir

| Point | Détail |
| --- | --- |
| Le quota est partagé | Les minutes sont comptées sur le compte GitHub, pas par dépôt : un dépôt gourmand bloque tous les autres |
| Offre gratuite, dépôts privés | 2 000 minutes par mois et 500 Mo de stockage pour les artefacts |
| Dépôts publics | Minutes illimitées sur les machines standard (ce modèle est public, les dépôts clients ne le sont pas) |
| Multiplicateurs | Une minute Linux compte 1, une minute Windows compte 2, une minute macOS compte 10 |
| Arrondi | Chaque job est arrondi à la minute supérieure : 5 jobs de 10 secondes coûtent 5 minutes |
| Durée maximale par défaut | 6 heures par job : un job bloqué peut vider le quota à lui seul, d'où `timeout-minutes` |
| Quand le quota est épuisé | Les workflows ne démarrent plus (ou échouent tout de suite) jusqu'au prochain cycle de facturation, sauf budget payant autorisé |
| Où suivre la consommation | GitHub > photo de profil > Settings > Billing and licensing > Usage, filtre « Actions » (détail par dépôt) |

Vercel, Netlify et EAS construisent sur leurs propres machines : leurs déploiements ne consomment pas de minutes GitHub (seule la CI lint + build en consomme).

## Règles pour économiser les minutes

Ces règles sont déjà appliquées dans `.github/workflows/ci.yml` et dans les [exemples de workflows](exemples-workflows/). Elles reprennent la décision prise pour LOUDEVIA et Post a thought le 19 novembre 2026.

- [ ] **Rien ne tourne après une fusion sur `main`** : la CI tourne sur la pull request, inutile de tout revérifier après la fusion.
- [ ] **Mise en ligne à la demande** : le workflow de déploiement n'a que `workflow_dispatch` (Actions > Run workflow), ou l'envoi se fait depuis le PC (`deployer`, FileZilla), ce qui ne coûte aucune minute. Une mise en ligne à chaque fusion seulement si le client y tient, avec l'accord de Lounes.
- [ ] **CI limitée au dossier concerné** dans un dépôt qui contient plusieurs projets (`paths:` sur `pull_request`, exemple : LOUDEVIA vérifie le site seulement quand `Loudevia/**` change). Attention : si ce check est obligatoire sur `main`, une PR qui ne touche pas ces chemins reste bloquée en attente ; ne pas le rendre obligatoire, ou garder la CI sans filtre.
- [ ] **Dependabot une fois par mois** : chaque PR qu'il ouvre lance la CI.
- [ ] **Installeurs de logiciels construits sur le PC** plutôt que sur des machines Windows ou macOS de GitHub : script `construire.ps1` de LOUDEVIA ([construction-locale.md](https://github.com/loki7even/LOUDEVIA/blob/main/docs/construction-locale.md)). macOS seulement à la demande, quand un Mac n'est pas disponible.
- [ ] `timeout-minutes` sur chaque job (10 pour une CI ou un déploiement de site).
- [ ] `concurrency` avec `cancel-in-progress: true` sur la CI : un nouveau push annule le run précédent de la même branche.
- [ ] Si un déploiement reste automatique à la fusion : l'ignorer quand seuls la doc ou les Markdown changent (`paths-ignore`).
- [ ] Machines Windows et macOS uniquement à la demande (`workflow_dispatch`) ou sur `main`, jamais sur chaque push (exemple : workflows `atelier.yml` et `formateur.yml` de LOUDEVIA).
- [ ] Pas de tâche planifiée (`schedule`) sans raison : une par semaine au plus (exemple : Gazelle republie le lundi pour rafraîchir les avis Google).
- [ ] Peu de jobs : regrouper lint, build et tests dans un seul job.
- [ ] Artefacts : garder seulement la dernière version (`retention-days` court, ou un job de nettoyage comme dans LOUDEVIA). Quand les 500 Mo sont pleins, les jobs échouent à l'envoi de l'artefact (« Artifact storage quota has been hit »).
- [ ] Dependabot regroupe les mises à jour mineures dans une seule PR par semaine : une seule CI au lieu de dix.

## Quand le quota est atteint

Trois options, de la plus simple à la plus coûteuse :

1. **Attendre** la remise à zéro au début du cycle de facturation (date visible dans Billing and licensing > Usage) et déployer à la main en attendant (section suivante).
2. **Autoriser un petit dépassement payant** : Billing and licensing > Budgets and alerts, budget Actions de quelques euros (une minute Linux coûte environ 0,006 $).
3. **Corriger la cause** : repérer le dépôt et le workflow responsables dans le détail de l'usage, puis appliquer les règles ci-dessus.

## Déployer à la main (sans GitHub Actions)

À utiliser quand Actions est bloqué (quota, panne) ou pour un projet qui n'a pas encore de workflow. Le principe est toujours le même : vérifier et construire sur le PC, puis envoyer le contenu du dossier produit (`dist/` pour Vite) dans le dossier du site sur le serveur.

### 1. Vérifier sur le PC ce que la CI aurait vérifié

```bash
git switch main && git pull
npm ci
npm run lint
npm run build
```

Si la protection de `main` exige le check `CI` et qu'il ne peut pas tourner, l'administrateur du dépôt peut fusionner quand même (case « Merge without waiting for requirements to be met » sur la PR), uniquement après avoir lancé ces commandes sans erreur.

### 2. Envoyer le site

| Hébergeur | Outil conseillé | Guide |
| --- | --- | --- |
| OVH (hébergement web) | FileZilla, en FTP explicite sur TLS (ou SFTP sur les offres qui incluent SSH) | [ftp-sftp-filezilla.md](ftp-sftp-filezilla.md) |
| Ionos (webspace) | Outil `deployer` de LOUDEVIA (façon normale de mettre en ligne Loudevia et Post a thought depuis le 19 novembre 2026) (PowerShell + WinSCP, n'envoie que les fichiers modifiés), ou FileZilla en SFTP | [deploiement-manuel.md de LOUDEVIA](https://github.com/loki7even/LOUDEVIA/blob/main/docs/deploiement-manuel.md) et [ftp-sftp-filezilla.md](ftp-sftp-filezilla.md) |
| Vercel | Rien à faire : Vercel construit lui-même à chaque push, sans Actions. En cas de besoin : `npx vercel --prod` depuis le dossier du projet | Documentation du projet |
| Expo (EAS) | `eas build` lancé à la main ; `eas build --local` construit sur le PC si les builds gratuits du mois sont épuisés | Dossier technique Loudevia, section 7 |

### 3. Après coup

- [ ] Ouvrir le site en navigation privée (Ctrl+F5) et vérifier la page modifiée et une page profonde.
- [ ] Noter l'envoi manuel dans le journal du projet (date, commit envoyé).
- [ ] Quand Actions remarche, relancer une fois le workflow de déploiement (Actions > workflow > Run workflow) pour que le serveur et `main` soient de nouveau synchronisés par l'automate. Pour OVH, lire d'abord la section « Après un envoi à la main » du [guide FileZilla](ftp-sftp-filezilla.md).

## Les identifiants

Les serveurs, utilisateurs et mots de passe FTP ou SFTP ne sont jamais écrits dans le dépôt ni dans la doc : ils restent dans le gestionnaire de mots de passe et dans les secrets GitHub. La doc d'un projet dit seulement **où** les retrouver (exemple : « OVH > Hébergements > onglet FTP - SSH »).
