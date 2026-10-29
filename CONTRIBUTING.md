# Contribuer

## Branches

- `main` est protégée et toujours déployable. On n'y pousse jamais directement.
- Une branche par changement, nommée `type/description-courte` : `feat/page-contact`, `fix/menu-mobile`, `docs/readme`.

## Commits

Format [Conventional Commits](https://www.conventionalcommits.org/fr/v1.0.0/) :

```
<type>(<portée optionnelle>): <description à l'impératif>
```

| Type | Usage |
| --- | --- |
| `feat` | nouvelle fonctionnalité |
| `fix` | correction de bug |
| `docs` | documentation seule |
| `style` | mise en forme, sans effet sur le comportement |
| `refactor` | réécriture sans changement de comportement |
| `perf` | performance |
| `test` | tests |
| `chore` | dépendances, configuration, outillage |
| `ci` | workflows GitHub Actions |

Exemples : `feat(contact): ajoute l'envoi du formulaire`, `fix: corrige le débordement du menu sur mobile`.

## Pull requests

1. Avant d'ouvrir la PR : `npm run lint` et `npm run build` passent en local.
2. Remplir le modèle de PR (quoi, pourquoi, comment tester, captures si visuel).
3. La CI doit être verte avant la fusion.
4. Fusion en **squash** : le titre de la PR devient le commit sur `main`, il suit donc le format ci-dessus.
5. Ajouter une ligne dans `CHANGELOG.md` sous `[Non publié]` pour tout changement visible.

## Issues

Utiliser les modèles proposés (bug ou fonctionnalité). Une issue décrit un seul problème ou un seul besoin.
