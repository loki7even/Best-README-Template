# Leçons des projets

Mis à jour le 18 novembre 2026

Ce que les projets de Lounes ont appris à leurs dépens, rassemblé ici pour ne pas le réapprendre. Chaque ligne cite le dépôt où le détail se trouve. Ajouter une ligne à chaque piège nouveau, et la règle correspondante dans le modèle (`CLAUDE.md`, workflows ou checklist de `TEMPLATE.md`).

## Les deux leçons principales

| Leçon | Règle retenue | Guide |
| --- | --- | --- |
| Le quota de minutes GitHub Actions est partagé entre tous les dépôts privés du compte. En novembre 2026, les installeurs Windows et macOS de LOUDEVIA l'ont épuisé et ont bloqué CI et déploiements partout | Machines Windows et macOS à la demande seulement, `timeout-minutes` sur chaque job, pas de tâche planifiée inutile ; quand le quota est atteint, vérifier et déployer à la main | [quota-github-actions.md](quota-github-actions.md) |
| Chez OVH, FileZilla est le moyen le plus sûr de voir et de manipuler le serveur (envoi à la main, `.htaccess`, sauvegarde, ménage) | FTP explicite sur TLS, fichiers cachés affichés, mots de passe protégés par un mot de passe principal ; après un envoi à la main, supprimer le fichier d'état de l'action FTP | [ftp-sftp-filezilla.md](ftp-sftp-filezilla.md) |

## Déploiement et hébergement

| Leçon | Règle retenue | Source |
| --- | --- | --- |
| Un merge sur `main` met le site en production | Chaque `CLAUDE.md` dit ce que déclenche un merge ; tableau commun dans [maintenance-dependances.md](maintenance-dependances.md) | Tous les dépôts |
| Un miroir avec suppression (`lftp --delete`) vers la racine du webspace efface les autres sites | Dossier cible dédié par site (`/loudevia`, `/lagames`, `/poemes`) ; le workflow refuse `/` | LOUDEVIA, LAGames |
| Couper les mises en ligne automatiques doit être simple (maintenance, passation, hébergement pas encore prêt) | Job conditionné par une variable de dépôt (`if: vars.OVH_DEPLOY == 'oui'`) plutôt que de supprimer le workflow | Kizuna-Sekai |
| `vite preview` sert l'accueil sur toutes les adresses et fausse le test d'un site pré-rendu | Tester `dist/` avec `python3 -m http.server` | Kizuna-Sekai |
| Le `.htaccess` (redirections HTTPS, réécriture SPA, en-têtes) est un fichier caché, facile à oublier lors d'un envoi à la main | Le garder dans `public/` pour qu'il parte avec le build ; l'afficher dans FileZilla | Kizuna-Sekai, LAGames |
| Un domaine sans registre du commerce (`.dz`) ou pas encore acheté retarde la mise en ligne | Publier d'abord sur un sous-domaine déjà payé (`client.loudevia.fr`), l'URL du site dans une seule constante | LAGames |
| HSTS activé trop tôt bloque le site si le certificat a un souci | Activer l'en-tête HSTS seulement après quelques jours de HTTPS sans erreur | LAGames, Kizuna-Sekai |
| Les enregistrements MX, SPF et DKIM font marcher les e-mails du domaine | Ne jamais les modifier ni « réinitialiser la zone DNS » en reliant un site | Kizuna-Sekai |
| Un premier déploiement tardif fait découvrir les problèmes d'hébergement à la fin | Envoyer une page vide sur l'hébergeur dès l'initialisation | Modèle site web LOUDEVIA |

## Offres gratuites et leurs limites

| Service | Limite qui a compté | Source |
| --- | --- | --- |
| GitHub Actions | 2 000 minutes par mois (Windows x2, macOS x10), 500 Mo d'artefacts | LOUDEVIA |
| Vercel Hobby | Cron Jobs une fois par jour au plus (refusé au déploiement sinon), fonctions limitées à 60 secondes | Cetavi |
| Supabase Free | Deux projets actifs par compte ; un projet sans activité est mis en pause au bout d'une semaine | pharmahub (Cetavi mis en pause pour libérer la place) |
| Firestore (Firebase Spark) | 50 000 lectures par jour : un seul utilisateur malveillant peut couper le service | WTFast |
| EAS (Expo) | Nombre de builds cloud limité par mois ; `eas build --local` construit sur le PC | WTFast |

## Secrets et clés

| Leçon | Règle retenue | Source |
| --- | --- | --- |
| Une clé qui ne sert qu'au build (Google Places) n'a rien à faire dans le navigateur | Pas de préfixe `VITE_` ; elle reste dans les secrets GitHub et n'est lue que par le script de build | GazelleTransports |
| Une clé « publique par nature » (Web3Forms, Supabase publishable) reste quand même hors du dépôt | `.env.local` et secrets GitHub ; le workflow s'arrête avec un message clair si elle manque | GazelleTransports, LAGames |
| Les identifiants FTP, SFTP, OVH, Ionos ou Google se retrouvent vite dans une doc | La doc dit où les trouver, jamais leur valeur | Kizuna-Sekai |

## Applications mobiles

| Leçon | Règle retenue | Source |
| --- | --- | --- |
| Le nom de package Android ne peut plus changer une fois l'app créée dans Play Console | Choisir l'identifiant définitif avant le premier envoi ; seul le nom affiché peut changer | WTFast |
| Le tout premier AAB ne peut pas partir par l'API | L'envoyer à la main dans Play Console, puis EAS Submit | Dossier technique LOUDEVIA § 8.6 |
| Des réglages enregistrés mais jamais lus par le code passent inaperçus | Relire le code de bout en bout avant un test fermé (audit de 59 points sur BlindzRun) | WTFast |

## Paiement

| Leçon | Règle retenue | Source |
| --- | --- | --- |
| Stripe n'accepte pas toutes les entreprises (exemple : Polynésie française) | Vérifier le pays du client avant de choisir le prestataire ; paiement derrière une interface (`PaymentProvider`) pour pouvoir changer | pharmahub |
