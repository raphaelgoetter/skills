---
name: css-guidelines
description: >-
  Guidelines CSS Alsacreations. Utiliser quand on génère, modifie, relit
  ou audite du CSS. Inclut conventions de nommage, architecture, syntaxe, custom properties, responsive, accessibilité.
---

# Guidelines CSS

Suis impérativement les règles définies dans [css.md](css.md).

Points d'attention prioritaires :

1. Prioriser le CSS Vanilla natif et les custom properties, et éviter les frameworks CSS sauf si le projet le nécessite explicitement.
2. Structurer les styles avec des fichiers clairs et un point d'entrée unique (`app.css`), en important les fichiers par ordre de `@layer` : `config`, `base`, `components`, `utilities`.
3. Utiliser `@scope` pour isoler les styles des composants et `@layer` pour gérer la priorité des fichiers, sans mélanger les deux concepts.
4. Favoriser les classes génériques (`.title`, `.media`, `.header`, `.footer`, `.content`, `.desc`) isolés dans des `@scope`.
5. Respecter l’ordre SMACSS des propriétés dans les règles CSS : positionnement, modèle de boîte, typographie, décoration, animations, puis autres.
6. Limiter le nesting à un seul niveau si possible et éviter les sélecteurs trop profonds qui augmentent inutilement la spécificité.
7. Ne jamais coder de valeurs en dur pour les couleurs, espacements, typographies ou bordures : utiliser des variables CSS (`--color-*`, `--spacing-*`, `--text-*`, etc.).
8. Organiser le design system en primitives, tokens et composants : primitives dans `theme.css`, tokens sémantiques pour les rôles et styles de composants réutilisables.
9. Privilégier les styles utilitaires des Layouts "Bretzel" pour la plupart des dispositions "simples" et responsive. N'utiliser Grid Layout ou Flexbox que pour des affichages complexes ou spécifiques.
10. Privilégier le responsive moderne et fluide : custom media queries, `clamp()` pour les tailles de texte et les espacements, mobile-first.
