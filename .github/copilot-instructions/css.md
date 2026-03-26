# CSS

## Architecture (obligatoire)

- 3 niveaux : Primitives (`--color-pink-300`) → Tokens sémantiques (`--primary`) → Composants (`.card { color: var(--primary); }`)
- Jamais de valeur hardcodée dans les composants — toujours `var(--token-name)`
- Layouts Bretzel (`data-layout="stack|cluster|autogrid|duo|repel|reel|switcher"`) AVANT tout Flexbox/Grid custom

## `@scope()`

- Restreindre les composants dans un `@scope()` pour éviter les conflits de styles

```css
/* ✅ @scope + classes simples */
@scope (.card) {
  /* Cible .title uniquement s'il appartient à la structure de la carte */
  .title {
    font-size: var(--text-l);
    color: var(--primary);
  }
}
```

## Syntaxe

- Nommage des classes simple : `.card`, `.title`, `.content`, `.media`, `.header`, `.footer`, `.desc`
- Ordre SMACSS : position → box-model → typo → décoration → animation
- Nesting natif CSS recommandé, profondeur max 1 niveau
- Thématisation : `color-scheme: light dark` sur `:root` + tokens de couleurs (`--surface`, `--on-surface`, etc.) pour les valeurs

## Interdit

- Valeurs en dur dans les composants
- Bootstrap, Tailwind (sauf demande explicite)
- Nesting > 1 niveau
