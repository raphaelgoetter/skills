# Instructions — Projet [Nom] — Alsacréations

## Identité et stack

- Agence : Alsacréations
- Guidelines de référence : <https://github.com/alsacreations/kiwipedia>
- Stack : HTML sémantique + CSS Vanilla moderne + JS natif (Vue 3 si mentionné explicitement)
- Pas de framework CSS sauf demande explicite

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
