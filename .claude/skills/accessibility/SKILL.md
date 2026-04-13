---
name: accessibility-guidelines
description: >-
  Guidelines Accessibilité Alsacreations. Utiliser quand on génère, modifie, relit
  ou audite une page web.
---

# Guidelines Accessibilité

Suis impérativement les règles définies dans [accessibility.md](accessibility.md).

Points d'attention prioritaires :

1. Respecter la sémantique HTML et les landmarks ARIA : `<html lang>`, `<main role="main">`, `<header>`, `<footer>`, `<nav>`, titres hiérarchisés et `<title>` pertinents.
2. Fournir un lien d'accès rapide (skip link) au contenu principal et garantir une navigation cohérente au clavier sans piège de tabulation.
3. Associer systématiquement chaque champ de formulaire à un `<label>` ou une alternative ARIA, utiliser `<fieldset>` + `<legend>` pour les groupes et signaler les champs obligatoires.
4. Préserver ou proposer un contour de focus visible sur tous les éléments interactifs, et utiliser `:focus-visible` plutôt que `outline: none`.
5. Travailler avec des unités fluides (`rem`, `em`, `clamp()`), ne pas fixer la hauteur des éléments de contenu et laisser le zoom fonctionner jusqu'à 200%.
6. Ne pas utiliser de contenu généré (`::before`, `::after`) pour véhiculer des informations importantes ou des icônes essentielles.
7. Masquer correctement le contenu destiné aux lecteurs d'écran avec une classe dédiée (`visually-hidden`) plutôt que `display: none`.
8. Donner des libellés explicites à tous les liens, indiquer les téléchargements et signaler les ouvertures dans une nouvelle fenêtre.
9. Rendre les médias accessibles : attribut `alt` pertinent pour les images, SVGs accessibles, lecteurs audio/vidéo adaptés et sous-titres lorsque nécessaire.
10. Vérifier les interactions dynamiques et l’usage d’ARIA sur les composants complexes : `aria-live`, modales, traps de focus et compatibilité avec les technologies d’assistance.
