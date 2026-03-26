# Performances

## CSS

- Grid Layout > Flexbox (moins sensible aux Layout Shifts)
- `flex: 1; min-width: 0` plutôt que `flex-grow: 1`
- `grid-template-columns: minmax(0, 1fr)` plutôt que `1fr`

## Images

- `loading="lazy"` sur toutes les images hors viewport initial
- `fetchpriority="high"` sur l'image LCP
- `width` + `height` sur toutes les images (évite le CLS)
- Format AVIF en priorité

## Chargement

- Scripts non critiques : `defer` ou `async`
- Fonts : `font-display: swap`
- `rel="preload"` pour ressources critiques au-dessus de la ligne de flottaison
