# HTML

## Structure

- HTML valide W3C
- `<html lang="fr">` obligatoire si site français
- 1 seul `<h1>` par page, hiérarchie h1→h6 sans saut de niveau
- Éléments sémantiques : `<header>`, `<main>`, `<footer>`, `<nav>`, `<section>`, `<article>`, `<aside>`

## Images

- Toujours `width` + `height` (dimensions réelles) → évite le CLS
- `alt` descriptif ou `alt=""` si décorative
- Format bitmap : AVIF > WebP (JPG/PNG : legacy uniquement)
- `loading="lazy"` hors viewport, `fetchpriority="high"` sur l'image LCP

## Sécurité / bonnes pratiques

- `target="_blank"` → toujours `rel="noopener noreferrer"`
- Viewport : jamais `maximum-scale=1` ni `user-scalable=no`
- Contenu masqué visuellement → classe `.visually-hidden` (jamais `display:none` si lu par AT)
