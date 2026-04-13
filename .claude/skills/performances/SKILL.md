---
name: performances-guidelines
description: >-
  Guidelines Performances Alsacreations. Utiliser quand on génère, modifie, relit
  ou audite une page web.
---

# Guidelines Performances

Suis impérativement les règles définies dans [performances.md](performances.md).

Points d'attention prioritaires :

1. Minimiser le poids des ressources texte et médias en appliquant la minification, la compression et l’optimisation avant mise en production.
2. Réduire le nombre de requêtes HTTP en regroupant les fichiers, en limitant les ressources externes et en favorisant le lazy-loading pour les ressources non critiques.
3. Utiliser les formats modernes et légers pour les images, vidéos, polices et autres assets : AVIF/WebP pour les images, WOFF2 pour les polices.
4. Employer les attributs de pré-chargement et de priorité (`async`, `defer`, `rel=preload`, `fetchpriority`) pour optimiser l’ordre de chargement des scripts, polices et images critiques.
5. Mettre en place une stratégie de cache efficace avec des en-têtes HTTP adaptés (`Cache-Control`, `Expires`) pour les ressources statiques et les contenus contrôlés.
6. Suivre les Core Web Vitals : LCP rapide (<2.5s), INP réactif (<200ms) et CLS faible (<0.1) pour garantir une expérience performante.
7. Préférer les mécanismes natifs du navigateur pour les optimisations (lazy-loading natif, preconnect, dns-prefetch) avant d’ajouter des scripts supplémentaires.
8. Limiter les shifts de mise en page en choisissant des modes CSS stables (Grid plutôt que Flexbox lorsque pertinent) et en définissant des dimensions pour les images et médias.
9. Mesurer et auditer régulièrement avec des outils fiables (PageSpeed Insights, WebPageTest, Lighthouse, GTmetrix) et définir un budget de performance clair.
10. Adapter la performance au contexte du projet en combinant cache front-end, cache back-end et compression serveur pour les sites dynamiques ou CMS.
