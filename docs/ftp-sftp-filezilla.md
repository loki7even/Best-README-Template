# Manipuler un serveur FTP ou SFTP avec FileZilla (OVH, Ionos)

Guide commun à tous les projets de Lounes. Pour l'hébergement web OVH, **FileZilla est l'outil de référence** : envoi du site à la main quand GitHub Actions est bloqué, vérification de ce qui est réellement en ligne, sauvegarde avant une grosse modification, ménage dans le dossier `www/`. Il marche aussi pour le webspace Ionos (en SFTP).

Aucun identifiant n'est écrit ici ni dans un dépôt : ils se retrouvent dans l'espace client de l'hébergeur et dans le gestionnaire de mots de passe.

## 1. Installer FileZilla (une fois par PC)

1. Télécharger **FileZilla Client** (pas « Server ») depuis le site officiel `filezilla-project.org`.
2. Pendant l'installation, refuser les logiciels partenaires proposés.
3. Protéger les mots de passe enregistrés : Édition > Paramètres > Interface > Mots de passe > « Enregistrer les mots de passe protégés par un mot de passe principal ». Sans cela, FileZilla les garde en clair sur le disque. Autre choix possible : type d'authentification « Demander le mot de passe » dans chaque site (rien n'est enregistré).
4. Afficher les fichiers cachés, sinon le `.htaccess` est invisible : menu Serveur > « Forcer l'affichage des fichiers cachés ».

## 2. Retrouver les accès

| | OVH (hébergement web) | Ionos (webspace) |
| --- | --- | --- |
| Écran | Espace client > Web Cloud > Hébergements > l'hébergement > onglet **FTP - SSH** | Hébergement > le contrat > **SFTP & SSH** |
| Serveur | Forme `ftp.clusterXXX.hosting.ovh.net` | Forme `access-XXXXXXXXXX.webspace-host.com` |
| Utilisateur | Login FTP principal (ou un login secondaire limité à un dossier) | Utilisateur SFTP |
| Mot de passe | Même écran, « Modifier le mot de passe » (prise en compte en quelques minutes) | Même écran, réinitialisable |
| Protocole | FTP explicite sur TLS, port 21. SFTP (port 22) seulement sur les offres qui incluent SSH (Pro et au-dessus) | SFTP, port 22 |
| Dossier du site | `www/` par défaut (voir l'onglet Multisite pour le dossier relié au domaine) | Celui relié au domaine, ex. `/loudevia`, `/lagames` (jamais la racine) |

## 3. Créer le site dans le gestionnaire (une fois par projet)

Fichier > Gestionnaire de sites (Ctrl+S) > Nouveau site, nommé comme le projet :

| Champ | OVH en FTPS | OVH ou Ionos en SFTP |
| --- | --- | --- |
| Protocole | FTP - Protocole de transfert de fichiers | SFTP - SSH File Transfer Protocol |
| Hôte / Port | serveur de l'onglet FTP - SSH / 21 | serveur / 22 |
| Chiffrement | « Connexion FTP explicite sur TLS » (jamais « FTP simple non sécurisé ») | sans objet |
| Authentification | Normale (avec mot de passe principal) ou Demander le mot de passe | idem |
| Onglet Avancé | Dossier distant par défaut : `/www` | Dossier du site |

À la première connexion, FileZilla montre le certificat (FTPS) ou l'empreinte de la clé (SFTP) : vérifier que le nom correspond à l'hébergeur, puis cocher « Toujours faire confiance ». Si ce message réapparaît plus tard sans changement connu chez l'hébergeur, ne pas se connecter et vérifier d'abord.

## 4. Envoyer le site à la main

1. Construire sur le PC : `npm ci && npm run lint && npm run build`.
2. Se connecter. À gauche, ouvrir le dossier `dist/` du projet ; à droite, le dossier du site (`www/` chez OVH).
3. Envoyer **le contenu** de `dist/`, pas le dossier `dist` lui-même. Vérifier que le `.htaccess` part aussi (fichiers cachés affichés, section 1).
4. Ordre conseillé pour ne pas casser le site pendant l'envoi : d'abord le dossier `assets/` (fichiers aux noms uniques, sans conflit), ensuite `index.html` et les autres pages.
5. À la question « Le fichier existe déjà », choisir « Écraser » et cocher « Toujours utiliser cette action » pour cette file d'attente.
6. Contrôler l'onglet « Transferts échoués » en bas : il doit être vide. Relancer les échecs (clic droit > Réinitialiser et remettre dans la file).
7. Ouvrir le site en navigation privée et vérifier une page profonde (rechargement compris).

FileZilla n'efface pas sur le serveur les fichiers qui n'existent plus dans `dist/`. Les anciens fichiers de `assets/` ne gênent pas le site ; on peut les supprimer de temps en temps, une fois la nouvelle version vérifiée (Affichage > Comparaison de répertoires aide à les repérer).

## 5. Autres usages courants

| Besoin | Geste dans FileZilla |
| --- | --- |
| Sauvegarder avant une grosse modification | Clic droit sur le dossier du site > Télécharger, vers un dossier daté hors du dépôt |
| Vérifier ce qui est vraiment en ligne | Comparer la date des fichiers à droite avec le dernier déploiement ; ouvrir un fichier (clic droit > Afficher/Éditer) |
| Supprimer la page d'attente d'OVH | Supprimer l'ancien `index.html` ou `index.php` de `www/` s'il traîne après le premier envoi |
| Déposer un fichier qui vit seulement sur le serveur (configuration avec secrets, données) | L'envoyer à la main une fois, et le noter dans la doc du projet pour que personne ne l'écrase |
| Tester des accès avant de créer les secrets GitHub | Se connecter avec les mêmes valeurs : si FileZilla passe, le workflow passera |

## 6. Après un envoi à la main (sites OVH déployés par `FTP-Deploy-Action`)

Le workflow OVH (action `SamKirkland/FTP-Deploy-Action`) garde sur le serveur un fichier d'état, `.ftp-deploy-sync-state.json`, avec l'empreinte de chaque fichier qu'il a envoyé. Il n'envoie ensuite que les fichiers dont l'empreinte a changé **par rapport à ce fichier**, pas par rapport au serveur. Après un envoi ou une suppression faits à la main avec FileZilla :

- supprimer `.ftp-deploy-sync-state.json` dans `www/` (fichiers cachés affichés) ;
- relancer le workflow (Actions > Run workflow) : il renvoie alors tout le site et recrée le fichier d'état.

Sans cela, un fichier modifié à la main peut rester sur le serveur alors que `main` contient une autre version.

## 7. Pièges connus

| Symptôme | Cause et solution |
| --- | --- |
| Les pages profondes renvoient une erreur 404 | Le `.htaccess` n'est pas parti : afficher les fichiers cachés et le renvoyer |
| « Connexion refusée » ou « délai dépassé » chez OVH | Mauvais protocole ou port (SFTP sur une offre sans SSH) : passer en FTP explicite sur TLS, port 21 |
| « Échec de l'authentification » juste après un changement de mot de passe | OVH met quelques minutes à appliquer le nouveau mot de passe : attendre, puis mettre à jour le secret GitHub aussi |
| Transferts coupés au milieu d'un gros envoi | Trop de connexions simultanées : Édition > Paramètres > Transferts > 2 transferts simultanés au maximum |
| Le site affiche encore l'ancienne version | Cache du navigateur : Ctrl+F5 ou navigation privée |
| Tout le site a disparu | Envoi dans le mauvais dossier ou suppression à la racine : restaurer depuis la sauvegarde locale ou relancer le workflow. Ne jamais supprimer à la racine du compte FTP |
