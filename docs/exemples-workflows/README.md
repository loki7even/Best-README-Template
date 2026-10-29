# Exemples de workflows de déploiement

Copier le fichier voulu vers `.github/workflows/deploy.yml`, puis créer ses secrets dans GitHub > Settings > Secrets and variables > Actions. Chaque workflow lit la version de Node dans `.nvmrc` et publie le dossier `dist/` (Vite).

| Fichier | Hébergeur | Méthode | Secrets |
| --- | --- | --- | --- |
| [deploy-ionos.yml](deploy-ionos.yml) | Ionos (webspace) | SFTP avec `lftp`, miroir avec suppression | `IONOS_SFTP_HOST`, `IONOS_SFTP_USER`, `IONOS_SFTP_PASSWORD`, `IONOS_SFTP_DIR` |
| [deploy-ovh.yml](deploy-ovh.yml) | OVH (hébergement web) | FTP, envoi des fichiers modifiés | `OVH_FTP_SERVER`, `OVH_FTP_USERNAME`, `OVH_FTP_PASSWORD` |
| [deploy-github-pages.yml](deploy-github-pages.yml) | GitHub Pages | Action officielle | aucun (activer Pages > Source : GitHub Actions) |

Pour Next.js, Vercel déploie seul depuis GitHub : pas de workflow nécessaire. Pour Expo, utiliser EAS (`eas build`, `eas submit`).
