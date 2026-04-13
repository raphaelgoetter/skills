---
name: javascript-guidelines
description: >-
  Guidelines JavaScript Alsacreations. Utiliser quand on génère, modifie, relit
  du JavaScript ou TypeScript.
---

# Guidelines JavaScript

Suis impérativement les règles définies dans [javascript.md](javascript.md).

Points d'attention prioritaires :

1. Valider le code JavaScript/TypeScript avec ESLint et suivre une convention de style cohérente (indentation 2 espaces, quotes, point-virgule selon configuration).
2. Préférer `const` et `let` plutôt que `var`, et maîtriser la portée des variables pour éviter les fuites dans le scope global.
3. Écrire un code progressif et dégradable : placer les scripts utiles en fin de document ou utiliser `defer` / `async` pour réduire la latence.
4. Encapsuler le code dans des closures ou modules pour isoler les variables et éviter les conflits entre scripts externes.
5. Utiliser le naming lowerCamelCase pour les variables, fonctions et objets, et garder les noms explicites et alignés sur le HTML quand le DOM est manipulé.
6. Ne jamais laisser de `console.log()` ou `eval()` dans le code de production, et documenter le code avec des commentaires clairs quand nécessaire.
7. Préférer les données statiques et les attributs HTML (`data-*`) pour les contenus traduisibles ou le paramétrage des composants plutôt que d’encoder ces valeurs directement en JavaScript.
8. Adopter des gestionnaires d’événements clairs, éviter les alias jQuery et utiliser des classes `js-*` pour séparer le comportement JavaScript du style CSS.
9. Respecter l’accessibilité : utiliser ARIA pour les composants dynamiques (`aria-hidden`, `aria-expanded`, `aria-live`) et garantir une navigation clavier cohérente.
10. Privilégier des solutions natives et simples, et n’utiliser des frameworks ou librairies externes qu’avec une version clairement identifiée et minifiée si nécessaire.
