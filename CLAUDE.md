# CLAUDE.md

> Instructions permanentes pour Claude Code sur ce projet.
> Chaque règle ici s'applique à toutes les sessions, sans exception.
> Pour les guidelines complètes, voir les skills référencés en fin de section.

---

## Projet

- **Stack** : HTML/CSS vanilla, Vue.js 3 (Composition API), accessibilité RGAA/WCAG
- **Package manager** : pnpm (ne jamais utiliser npm ou yarn)
- **Commandes principales** :
  - `pnpm dev` — serveur de développement
  - `pnpm build` — build de production

---

## Comportement général

- Répondre en **français** sauf pour le code et les identifiants techniques
- Ne jamais modifier un fichier sans l'avoir lu en entier au préalable
- Toujours proposer une explication courte des choix effectués
- En cas de doute sur une intention, poser une seule question ciblée avant d'agir
- Privilégier la lisibilité et la maintenabilité à la concision

---

## CSS

**Règles cardinales (toujours actives) :**

- Préférer le CSS Vanilla natif et les custom properties, éviter les frameworks CSS sauf besoin projet.
- Structurer les styles via `app.css` et charger les fichiers dans l’ordre d’@layer : `config`, `base`, `components`, `utilities`.
- Isoler les composants avec `@scope` et utiliser `@layer` pour gérer la priorité des fichiers.
- Respecter l’ordre SMACSS des propriétés : positionnement → modèle de boîte → typographie → visuel → animation.
- Ne jamais coder de valeurs en dur pour les couleurs, espacements, typographies ou bordures : utiliser des variables CSS.
- Limiter le nesting à un seul niveau pour garder une spécificité faible et prévisible.

**Pour une tâche CSS spécifique :** utiliser le skill `/css-guidelines`
→ `.claude/skills/css/SKILL.md`

---

## HTML / Templates Vue

- Utiliser un document HTML5 valide, UTF-8, éléments et attributs en minuscules, avec des guillemets doubles.
- Déclarer la langue sur `<html>` et structurer le document avec des landmarks sémantiques (`<header>`, `<main>`, `<nav>`, `<aside>`, `<footer>`).
- Respecter une hiérarchie de titres logique avec une seule `<h1>` par page.
- Construire un `<head>` complet : `meta charset`, viewport responsive, titre pertinent, description, OpenGraph, canonical et favicon.
- Préférer les éléments sémantiques plutôt que des `<div>` ou `<span>` neutres.
- Optimiser les médias avec `width`/`height`, `loading="lazy"`, `decoding="async"` et des formats modernes.

---

## Accessibilité (priorité haute)

Ces règles ne sont pas négociables et s'appliquent à chaque modification :

- Respecter la sémantique HTML et les landmarks ARIA, y compris le titre, les rôles et les zones de contenu.
- Fournir un lien d’accès rapide au contenu principal et garantir une navigation clavier cohérente sans piège de tabulation.
- Associer chaque champ de formulaire à un `<label>` ou à une alternative ARIA, et regrouper les champs avec `<fieldset>` + `<legend>`.
- Préserver un focus visible et utiliser `:focus-visible` plutôt que `outline: none`.
- Utiliser des unités fluides (`rem`, `em`, `clamp()`), ne pas fixer les hauteurs de contenu et permettre le zoom jusqu’à 200%.
- Rendre les médias accessibles : `alt` pertinent, SVG accessibles, lecteurs audio/vidéo adaptés et masquer correctement les contenus pour les technologies d’assistance.

**Pour un audit ou une génération accessible :** utiliser le skill `/accessibilite`
→ `.claude/skills/accessibility/SKILL.md`

---

## Vue.js

- Composition API avec `<script setup>` systématiquement (pas d'Options API)
- Props typées via `defineProps<{...}>()` avec TypeScript ou JSDoc
- Un composant = un fichier `.vue`, nommé en PascalCase
- Les événements émis sont déclarés via `defineEmits`
- Pas de logique métier dans les templates : extraire dans des composables (`use*.js`)
- Les composables vivent dans `src/composables/`
- Pas de mutation directe des props

---

## JavaScript / TypeScript

- Valider le code avec ESLint et suivre une convention de style cohérente.
- Préférer `const` et `let` plutôt que `var`, et maîtriser la portée des variables.
- Écrire un code progressif et dégradable : placer les scripts utiles en fin de document ou utiliser `defer` / `async`.
- Encapsuler le code dans des closures ou des modules pour isoler les variables et éviter les conflits externes.
- Utiliser le naming lowerCamelCase et des noms explicites, surtout pour la manipulation du DOM.
- Ne jamais laisser de `console.log()` ou `eval()` dans le code de production.

---

## Git

- Respecter le format Conventional Commits : `type(scope): description`.
- Choisir le type de commit adapté à l’intention réelle du changement.
- Nommer les branches de façon structurée : `main`, `develop`, `feat/*`, `fix/*`, avec référence d’issue si possible.
- Utiliser `develop` pour les travaux en cours et `main` pour le code prêt pour la production.
- Faire des `git pull` réguliers et communiquer pour réduire les conflits.
- Résoudre les conflits manuellement puis ajouter et commit les fichiers résolus.
- Ne pas committer de fichiers générés, secrets ou `node_modules`.

---

## Écoconception

- Définir la méthodologie durable en amont : objectifs, cibles, indicateurs et revue régulière.
- Favoriser les technologies standards, open source et interopérables.
- Concevoir pour une large compatibilité matérielle et logicielle, y compris sur terminaux et navigateurs anciens.
- Déployer uniquement les composants utiles et supprimer les modules ou ressources non utilisés.
- Optimiser le poids des pages, le nombre de requêtes, le lazy-loading et la compression des assets.
- Préférer des formats légers adaptés aux images, vidéos, audio et documents, et mettre en cache les ressources contrôlées.

---

## Performances

- Minimiser le poids des ressources et compresser les contenus texte et médias.
- Réduire le nombre de requêtes HTTP en regroupant les fichiers et en favorisant le lazy-loading.
- Utiliser des formats modernes et légers : AVIF/WebP pour les images, WOFF2 pour les polices.
- Optimiser l’ordre de chargement avec `async`, `defer`, `rel=preload` et `fetchpriority`.
- Mettre en place une stratégie de cache HTTP efficace (`Cache-Control`, `Expires`).
- Mesurer les performances avec les Core Web Vitals et des audits réguliers.

---

## Ce que Claude ne doit pas faire

- Installer de nouvelles dépendances sans validation explicite
- Modifier `package.json`, `vite.config.*`, ou les fichiers de configuration sans demande
- Générer des migrations ou modifier la base de données de façon irréversible
- Supprimer des fichiers sans confirmation

---

## Skills disponibles

| Skill            | Déclenchement                               | Chemin                          |
| ---------------- | ------------------------------------------- | ------------------------------- |
| `/css`           | Écriture ou révision de CSS/SCSS            | `.claude/skills/css/`           |
| `/accessibility` | Audit, génération de composants accessibles | `.claude/skills/accessibility/` |
| `/html`          | Génération, révision ou audit HTML          | `.claude/skills/html/`          |
| `/javascript`    | Écriture ou révision de JS/TS               | `.claude/skills/javascript/`    |
| `/git`           | Règles de commit et gestion de branches     | `.claude/skills/git/`           |
| `/ecoconception` | Règles d'écoconception et bonnes pratiques  | `.claude/skills/ecoconception/` |
| `/performances`  | Règles de performance et bonnes pratiques   | `.claude/skills/performances/`  |
