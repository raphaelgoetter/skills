# Accessibilité

## Règles WCAG AA (minimum)

- Contraste texte : 4.5:1 minimum
- Tous les éléments interactifs navigables au clavier
- `alt` sur toutes les images porteuses d'information
- `<label>` associé à chaque champ de formulaire (via `for`/`id`)

## ARIA

- SVG décoratifs : `aria-hidden="true"`, pas de `<title>` ni `<desc>`
- Zones dynamiques : `role="status"` ou `aria-live="polite"`
- Landmarks ambigus : `aria-label` ou `aria-labelledby`
- Liens ambigus (ex: "Lire la suite") : `aria-label` avec contexte complet

## Interdit

- `display:none` ou `visibility:hidden` sur du contenu destiné aux AT
- `tabindex` positif (> 0)
- Attributs ARIA redondants avec la sémantique native (`role="button"` sur `<button>`)
