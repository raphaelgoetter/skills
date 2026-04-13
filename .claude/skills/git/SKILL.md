---
name: git-guidelines
description: >-
  Guidelines GIT Alsacreations. Utiliser quand on génère, modifie, relit
  ou audite un dépôt Git.
---

# Guidelines GIT

Suis impérativement les règles définies dans [git.md](git.md).

Points d'attention prioritaires :

1. Respecter le format Conventional Commits pour chaque message de commit afin de maintenir une histoire de projet claire et standardisée.
2. Choisir le type de commit approprié (`feat`, `fix`, `refactor`, `style`, `test`, `chore`, `perf`, `docs`, `build`, `ci`) selon l’intention réelle du changement.
3. Nommer les branches de manière expressive et structurée : `feat/*`, `fix/*`, `develop`, `main`, en y incluant si possible une référence d’issue ou de tâche.
4. Utiliser `develop` pour les travaux en cours et `main` pour le code prêt à être publié en production.
5. Faire des `git pull` réguliers et communiquer avec l’équipe pour éviter les conflits lorsque plusieurs personnes travaillent sur les mêmes fichiers.
6. Résoudre les conflits manuellement avec soin : conserver la version correcte, supprimer les marqueurs Git, ajouter les fichiers résolus et committer.
7. Activer des bonnes pratiques Git locales utiles comme `rerere` pour réutiliser les résolutions de conflits récurrentes.
8. Garder les commits petits et cohérents : un commit doit représenter une seule intention ou correction significative.
9. Éviter de committer des fichiers générés ou des dépendances sans nécessité, et laisser les outils de build gérer les artefacts.
10. Documenter les conventions Git du projet et relire les messages de commit avant validation pour garantir qualité et traçabilité.
