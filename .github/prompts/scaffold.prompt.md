# Prompt — Scaffolding de l'architecture IA du projet

> Copier-coller ce prompt dans Claude Code (terminal) ou Copilot en mode agent.
> Adapter les variables de la section "Contexte projet" avant d'envoyer.

---

## Prompt

````
Tu es un expert en configuration d'outils IA pour projets web.
Ta mission : générer l'architecture complète de fichiers de configuration
pour Claude Code et GitHub Copilot sur ce projet.

---

## Contexte projet

- Nom du projet : [MON_PROJET]
- Stack technique : HTML/CSS vanilla, Vue.js 3 (Composition API), accessibilité RGAA/WCAG
- Package manager : pnpm
- Commandes principales :
  - `pnpm dev` — serveur de développement
  - `pnpm build` — build de production
  - `pnpm lint` — lint JS/CSS
  - `pnpm lint:fix` — correction automatique
  - `pnpm test:run` — tests en mode CI
- Linter CSS : Stylelint
- Guidelines de référence :
  - CSS : https://github.com/alsacreations/kiwipedia/blob/main/guidelines/css.md
  - HTML : https://github.com/alsacreations/kiwipedia/blob/main/guidelines/html.md
  - Accessibilité : référentiel RGAA + WCAG 2.1 AA
- Langue de travail : français (sauf code et identifiants techniques)
- Conventions de commit : Conventional Commits (feat, fix, style, refactor, a11y, docs, chore)

---

## Fichiers à générer

Génère l'intégralité des fichiers suivants avec leur contenu complet et opérationnel.
Ne génère pas de placeholders vides : chaque fichier doit être immédiatement utilisable.

### 1. `CLAUDE.md` (racine du projet)

Instructions permanentes pour Claude Code et Copilot.
Doit contenir :
- Description du projet et stack
- Commandes pnpm disponibles
- Règles CSS cardinales (unités, custom properties, ordre des propriétés, BEM, mobile-first)
- Règles HTML/Vue (sémantique, Composition API, script setup, props typées, composables)
- Règles d'accessibilité non-négociables (focus, contraste, labels, ARIA)
- Conventions Git (Conventional Commits, type `a11y` inclus)
- Ce que Claude ne doit jamais faire (liste explicite)
- Table des skills disponibles avec chemin et déclenchement

Contrainte : concis et précis. Déléguer les détails aux skills. Max ~100 lignes.

### 2. `CLAUDE.local.md` (racine du projet)

Template de fichier de préférences personnelles (à gitignorer).
Doit contenir des sections commentées avec exemples :
- Style de réponse préféré
- Outils locaux spécifiques
- Chemins locaux éventuels
- Note rappelant que ce fichier ne doit pas être commité

### 3. `AGENTS.md` (racine du projet)

Protocole pour les agents autonomes.
Doit contenir :
- Étapes d'exploration initiale obligatoires
- Liste des commandes autorisées / interdites sans validation
- Workflow de validation séquencé avant commit : lint → build → tests → vérif a11y
- Règles spécifiques pour les commits sur fichiers CSS, Vue, HTML
- Format des commits avec tableau des types et exemples
- Ce que l'agent ne doit jamais faire
- Procédure en cas de blocage

### 4. `.claude/rules/css.md`

Règles CSS détaillées, référençable depuis CLAUDE.md via `@rules/css.md`.
Doit contenir :
- Ordre complet des propriétés CSS
- Conventions de nommage BEM complètes avec exemples
- Liste des custom properties standard du projet (`--color-*`, `--spacing-*`, `--font-*`)
- Règles responsive (breakpoints, mobile-first)
- Cas particuliers (z-index scale, transitions, animations)

### 5. `.claude/rules/vue.md`

Règles Vue.js détaillées.
Doit contenir :
- Structure type d'un composant Vue 3 (ordre des blocs, script setup, template, style scoped)
- Conventions de nommage (composants PascalCase, composables useXxx, events kebab-case)
- Patterns interdits (Options API, mutation de props, logique dans le template)
- Structure des dossiers src/ (components/, composables/, views/, assets/)

### 6. `.claude/commands/audit-a11y.md`

Slash command `/project:audit-a11y` pour Claude Code.
Doit : lister les fichiers Vue et HTML récemment modifiés via `!git diff --name-only HEAD~1`,
puis déclencher une analyse accessibilité sur chacun selon les critères RGAA prioritaires.

### 7. `.claude/commands/audit-css.md`

Slash command `/project:audit-css`.
Doit : lister les fichiers CSS/SCSS/Vue modifiés, vérifier la conformité aux guidelines
(custom properties, unités, BEM, ordre des propriétés).

### 8. `.claude/skills/css-guidelines/SKILL.md`

Frontmatter YAML + instructions du skill CSS.
- `name` : `css-guidelines`
- `description` : précise et exploitable par le modèle pour l'auto-détection
- Corps : points prioritaires numérotés + référence à `./css-guidelines.md`

### 9. `.claude/skills/css-guidelines/css-guidelines.md`

Contenu complet des guidelines CSS Alsacreations.
Récupérer et adapter le contenu de :
https://github.com/alsacreations/kiwipedia/blob/main/guidelines/css.md
Structurer en sections exploitables par un LLM (pas de mise en forme décorative).

### 10. `.claude/skills/accessibilite/SKILL.md`

Frontmatter YAML + instructions du skill accessibilité.
- `name` : `accessibilite`
- `description` : couvre audit, génération de composants accessibles, vérification RGAA/WCAG
- Corps : critères prioritaires WCAG 2.1 AA, patterns ARIA courants, checklist de vérification

### 11. `.claude/skills/composant-vue/SKILL.md`

Frontmatter YAML + instructions du skill de génération de composants Vue.
- `name` : `composant-vue`
- Corps : procédure de création (props → emits → template → style scoped → tests)
  + référence à `./composant-template.vue`

### 12. `.claude/skills/composant-vue/composant-template.vue`

Template Vue 3 de référence avec Composition API, script setup, props typées,
emits déclarés, slot nommé, style scoped, commentaires explicatifs sur chaque section.
Doit être accessible par défaut (rôle ARIA, focus visible, label).

### 13. `.github/copilot-instructions.md`

Instructions Copilot toujours actives.
Peut être un résumé autonome ou renvoyer vers CLAUDE.md.
Doit couvrir les mêmes sections que CLAUDE.md mais de façon encore plus concise.

### 14. `.github/instructions/css.instructions.md`

```yaml
---
applyTo: "**/*.css,**/*.scss,**/*.module.css"
---
````

Suivi des règles CSS cardinales + lien vers le skill css-guidelines.

### 15. `.github/instructions/vue.instructions.md`

```yaml
---
applyTo: "**/*.vue"
---
```

Suivi des règles Vue + accessibilité obligatoire dans les composants + lien vers les skills.

### 16. `.github/instructions/html.instructions.md`

```yaml
---
applyTo: "**/*.html"
---
```

Règles sémantique HTML, accessibilité, structure de document.

### 17. `.github/agents/reviewer.agent.md`

Custom agent Copilot "Reviewer".

- Lecture seule (pas de modification de fichiers)
- Vérifie : qualité du code, conformité aux guidelines CSS/Vue, accessibilité, conventions Git
- Modèle suggéré : Claude Sonnet ou Opus
- Structure sa réponse en sections : Accessibilité / CSS / Vue / Autres

### 18. `.github/agents/planner.agent.md`

Custom agent Copilot "Planner".

- Génère un plan d'implémentation détaillé sans écrire de code
- Vérifie la faisabilité accessibilité avant de planifier
- Sections : Vue d'ensemble / Composants à créer / Points d'attention a11y / Étapes ordonnées

### 19. `.github/prompts/audit-css.prompt.md`

Prompt réutilisable pour auditer un fichier CSS selon les guidelines Alsacreations.
Doit demander à l'utilisateur de préciser le fichier cible via `${input:fichier}`.

### 20. `.github/prompts/audit-a11y.prompt.md`

Prompt réutilisable pour auditer l'accessibilité d'un composant Vue ou d'une page HTML.
Vérifie : structure sémantique, focus, contraste, labels, ARIA, navigation clavier.

### 21. `.vscode/settings.json`

Configuration VS Code minimale :

- `chat.skillsLocations` pointant vers `.claude/skills/**`
- Activation de `chat.useCustomizationsInParentRepositories`
- Désactivation des suggestions inline si souhaité (section commentée)

### 22. `.gitignore` (entrées à ajouter)

Ajouter uniquement les entrées relatives à cette architecture :

- `CLAUDE.local.md`
- `.claude/projects/`

---

## Contraintes de génération

- Chaque fichier doit être **complet et immédiatement utilisable**, sans placeholder du type `[À COMPLÉTER]`
- Les fichiers SKILL.md doivent avoir un frontmatter YAML valide avec `name` et `description`
- Les fichiers `.instructions.md` doivent avoir un frontmatter avec `applyTo`
- Les fichiers `.agent.md` doivent avoir un frontmatter avec `name`, `description` et `tools`
- Aucune duplication : si une règle est dans un skill, elle n'est pas répétée en entier dans CLAUDE.md
- Respecter la hiérarchie : CLAUDE.md reste court, les détails vivent dans les skills et rules
- Générer les fichiers dans l'ordre listé, en annonçant chaque fichier avant son contenu

---

## Livrable attendu

À la fin de la génération :

1. Confirmer la liste des fichiers créés
2. Signaler tout fichier qui nécessite une action manuelle complémentaire
   (ex. : récupération de contenu externe, adaptation à l'environnement local)
3. Indiquer la commande pour vérifier que les skills sont bien détectés par Copilot :
   taper `/skills` dans le chat VS Code

```

---

## Notes d'utilisation

**Dans Claude Code (terminal) :**
Lancer depuis la racine du projet. Claude Code créera les fichiers directement
dans l'arborescence du projet. Vérifier ensuite avec `ls -la .claude/ .github/`.

**Dans Copilot agent mode (VS Code) :**
Ouvrir le chat, passer en mode Agent, coller le prompt.
Copilot proposera les créations de fichiers sous forme de diffs à valider un par un.

**Adapter avant d'envoyer :**
- Remplacer `[MON_PROJET]` par le nom réel
- Ajuster les commandes pnpm si les scripts ont des noms différents
- Ajouter ou retirer des guidelines selon les technologies du projet
- Retirer les fichiers déjà existants de la liste "Fichiers à générer"
```
