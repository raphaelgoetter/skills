# JavaScript

## Principes

- Vanilla JS en priorité — pas de bibliothèque si solution CSS native possible
- ES modules (`import`/`export`) — pas de CommonJS
- `const` par défaut, `let` si nécessaire, jamais `var`
- Sélecteurs : `querySelector`/`querySelectorAll` — pas de jQuery

## DOM

- Hooks JS : classes `.js-*` uniquement (jamais cibler une classe CSS fonctionnelle)
- Délégation d'événements plutôt que listeners multiples
- `addEventListener` avec `{ passive: true }` pour les events de scroll/touch

## Interdit

- `innerHTML` avec données utilisateur (XSS)
- `eval()`
- Modification directe de `style.*` → passer par CSS Custom Properties ou classes
