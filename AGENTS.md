# AGENTS — Alsacréations Front-end Guidelines

Ce fichier définit les conventions obligatoires pour tout agent IA intervenant sur ce projet.
Il se base sur [Kiwipedia Alsacréations](https://github.com/alsacreations/kiwipedia).

## Identité projet

- **Agence** : Alsacréations
- **Stack front** : HTML sémantique + CSS Vanilla moderne + JavaScript natif (ou Vue 3 si mentionné)
- **Pas de framework CSS** (pas de Bootstrap, pas de Tailwind sauf instruction explicite)

## Consulter les skills par domaine

Les règles détaillées sont dans `.github/copilot-instructions/` :

- `css.md` — Architecture, nommage, SMACSS, Bretzel, tokens
- `html.md` — Sémantique, images, sécurité
- `accessibility.md` — WCAG AA, ARIA
- `javascript.md` — Vanilla JS, DOM
- `performances.md` — Core Web Vitals, CLS, LCP
- `git.md` — Conventional Commits

## Comportement attendu

- Toujours proposer la solution CSS native avant une solution JS
- Toujours utiliser les layouts Bretzel avant du Flexbox/Grid custom
- Toujours utiliser `var(--token)` — jamais de valeur hardcodée dans les composants
- Signaler si une demande entre en conflit avec les guidelines ci-dessus

---

## Ce que l'IA NE DOIT PAS faire

- ❌ Écrire des valeurs CSS en dur dans les composants
- ❌ Créer du nesting CSS profond (> 1 niveau)
- ❌ Utiliser Bootstrap, Tailwind ou tout autre framework CSS sauf demande explicite
- ❌ Créer du Flexbox ou Grid custom si un layout Bretzel suffit
- ❌ Sauter des niveaux de titre (ex: `<h1>` → `<h3>`)
- ❌ Oublier `alt` sur les images
- ❌ Utiliser `display:none` pour masquer du contenu destiné aux lecteurs d'écran
- ❌ Utiliser des bibliothèques JS si une solution CSS native existe
