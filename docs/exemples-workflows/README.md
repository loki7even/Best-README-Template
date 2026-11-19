# Exemples de workflows de déploiement

Copier le fichier voulu vers `.github/workflows/deploy.yml`, puis créer ses secrets dans GitHub > Settings > Secrets and variables > Actions. Chaque workflow lit la version de Node dans `.nvmrc` et publie le dossier `dist/` (Vite).

| Fichier | Hébergeur | Méthode | Secrets |
| --- | --- | --- | --- |
| [deploy-ionos.yml](deploy-ionos.yml) | Ionos (webspace) | SFTP avec `lftp`, miroir avec suppression | `IONOS_SFTP_HOST`, `IONOS_SFTP_USER`, `IONOS_SFTP_PASSWORD`, `IONOS_SFTP_DIR` |
| [deploy-ovh.yml](deploy-ovh.yml) | OVH (hébergement web) | FTPS, envoi des fichiers modifiés | `OVH_FTP_SERVER`, `OVH_FTP_USERNAME`, `OVH_FTP_PASSWORD`, plus la variable `OVH_DEPLOY` = `oui` |
| [deploy-github-pages.yml](deploy-github-pages.yml) | GitHub Pages | Action officielle | aucun (activer Pages > Source : GitHub Actions) |

Chaque exemple a déjà les réglages qui économisent le quota de minutes Actions : `timeout-minutes: 10`, pas de redéploiement quand seule la doc change (`paths-ignore`), un seul job. Avant d'en ajouter un autre (tâche planifiée, machine Windows ou macOS), lire [quota-github-actions.md](../quota-github-actions.md). Si Actions est bloqué, le même envoi se fait à la main : [ftp-sftp-filezilla.md](../ftp-sftp-filezilla.md).

Pour Next.js, Vercel déploie seul depuis GitHub : pas de workflow nécessaire. Pour Expo, utiliser EAS (`eas build`, `eas submit`).
