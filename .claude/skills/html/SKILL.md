---
name: html-guidelines
description: >-
  Guidelines HTML Alsacreations. Utiliser quand on génère, modifie, relit
  ou audite une page web.
---

# Guidelines HTML

Suis impérativement les règles définies dans [html.md](html.md).

Points d'attention prioritaires :

1. Utiliser un document valide HTML5 avec `<!DOCTYPE html>`, encodage UTF-8, éléments et attributs en minuscules, et guillemets doubles pour les attributs.
2. Déclarer la langue de la page avec `lang` sur `<html>` et structurer le document par landmarks sémantiques (`<header>`, `<main>`, `<nav>`, `<aside>`, `<footer>`).
3. Respecter une hiérarchie logique des titres avec une seule balise `<h1>` par page, en évitant les sauts de niveau entre `<h2>`, `<h3>`, etc.
4. Construire un `<head>` complet avec `meta charset`, `viewport`, titre pertinent, description, OpenGraph, canonical et favicon modernes.
5. Préférer les éléments HTML sémantiques plutôt que des `<div>` ou `<span>` neutres pour améliorer accessibilité et SEO.
6. Optimiser les médias : ajouter `width` / `height` aux images, utiliser `loading="lazy"` et `decoding="async"`, et privilégier AVIF/WebP/SVG quand c’est possible.
7. Structurer les formulaires avec `<label>` associés, `autocomplete`, `inputmode`, `aria-describedby` pour l’aide et `rel="noopener"` pour les liens ouverts dans un nouvel onglet.
8. Privilégier des noms de classes et de fichiers en anglais avec des tirets, limiter l’usage des IDs et double-élaborer toujours par une classe CSS.
9. Favoriser les performances en plaçant les styles critiques en priorité dans le `<head>`, en validant le HTML et en réduisant le nombre de ressources bloquantes.
10. Intégrer les bonnes pratiques SEO : titres uniques, description concise, données structurées JSON-LD, balises OpenGraph et usage de `link rel="canonical"`.
