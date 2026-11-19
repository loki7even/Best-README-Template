# Déploiement

## Environnements

| Environnement | URL | Déclencheur |
| --- | --- | --- |
| Production | [https://exemple.fr] | [À la demande : Actions > Run workflow, ou envoi depuis le PC / push sur `main` si le client l'a demandé] |
| Aperçu | [URL d'aperçu] | pull request |

## Secrets GitHub Actions

| Secret | Où le trouver |
| --- | --- |
| `[NOM]` | [Hébergeur > page] |

## Déploiement à la main

Quand GitHub Actions est bloqué (quota de minutes, panne), suivre [quota-github-actions.md](quota-github-actions.md) : vérifier et construire sur le PC, puis envoyer `dist/` avec [FileZilla](ftp-sftp-filezilla.md) (OVH) ou l'outil `deployer` (Ionos).

| Information | Valeur |
| --- | --- |
| Accès FTP / SFTP | [Hébergeur > écran où retrouver serveur et utilisateur ; mot de passe dans le gestionnaire de mots de passe, jamais ici] |
| Protocole et port | [FTP explicite sur TLS, 21 / SFTP, 22] |
| Dossier du site sur le serveur | [`www/` / `/mon-site`] |
| Fichiers qui vivent seulement sur le serveur | [Aucun / liste : à ne jamais écraser ni supprimer] |

## Domaine et e-mails

- [ ] Domaine relié au dossier du site, certificat SSL actif
- [ ] Redirection HTTPS et réécriture SPA (`public/.htaccess` pour Ionos / OVH)
- [ ] E-mails du domaine : MX, SPF, DKIM, DMARC

## Dépannage

[Problèmes rencontrés et leur solution. Un piège qui peut toucher d'autres projets va aussi dans `lecons-projets.md` du modèle.]
