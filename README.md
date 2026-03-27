# Notes API — TP CI/CD

## Partie 4 — Questions écrites

### Pourquoi `latest` n'est pas une version ?

`latest` est un tag mutable qui change à chaque build. On ne sait pas quel code il contient, on ne peut pas le reproduire. Ce n'est pas une version, c'est un alias.

### Différence tag vs digest ?

Un tag est un alias lisible et réassignable (`v1.0.0`, `latest`). Un digest est l'empreinte SHA256 immuable du contenu de l'image. Le digest garantit qu'on utilise exactement la même image, le tag non.

### Pourquoi séparer staging/prod ?

Pour valider le comportement sur un environnement proche de la prod sans risquer d'impacter les utilisateurs réels. Si quelque chose casse en staging, la prod reste stable.

### Pourquoi une version vX.Y.Z ne doit jamais être reconstruite ?

Reconstruire peut produire une image différente (dépendances mises à jour, OS patché). La traçabilité serait rompue. Une version est un contrat immuable — si quelque chose change, on crée une nouvelle version.

### Citez les avantages d'une PR gate.

- Empêche de merger du code cassé sur `main`
- Force la revue avant intégration
- Donne un feedback rapide au développeur
- Protège la branche principale contre les erreurs humaines

### Qu'est-ce qui garantit la traçabilité ici ?

Le tag `<sha>` lie chaque image Docker exactement au commit qui l'a produite. Le tag de version lie l'image au tag Git. Les logs GitHub Actions conservent qui a déclenché quoi et quand.

---

## Release Process
