# Architecture IA du projet

Documentation de la configuration des outils d'IA (Claude Code et GitHub Copilot dans VS Code)
pour assurer une cohérence entre les deux environnements sur ce projet.

---

## Architecture des fichiers

```bash
projet/
│
├── CLAUDE.md                          # Instructions permanentes pour Claude Code (et Copilot)
├── CLAUDE.local.md                    # Préférences personnelles — ne pas commiter (.gitignore)
├── AGENTS.md                          # Protocole pour les agents autonomes (Copilot agent, Claude Code)
│
├── .claude/                           # Configuration spécifique à Claude Code CLI
│   ├── rules/                         # Règles modulaires (évite un CLAUDE.md trop long)
│   │   ├── css.md                     # Règles CSS détaillées (référencées depuis CLAUDE.md)
│   │   └── vue.md                     # Règles Vue.js détaillées
│   ├── commands/                      # Slash commands personnalisés (/project:nom-commande)
│   │   └── audit-a11y.md              # Exemple : /project:audit-a11y
│   └── skills/                        # Skills partagés Claude Code + Copilot (auto-détectés)
│       ├── css-guidelines/
│       │   ├── SKILL.md               # Frontmatter + points prioritaires + référence au fichier
│       │   └── css-guidelines.md      # Guidelines CSS complètes (ex. kiwipedia)
│       ├── accessibilite/
│       │   ├── SKILL.md
│       │   └── accessibilite.md       # Critères RGAA/WCAG, patterns ARIA, exemples
│       └── composant-vue/
│           ├── SKILL.md
│           └── composant-template.vue # Template de composant Vue de référence
│
├── .github/                           # Configuration spécifique à GitHub Copilot / VS Code
│   ├── copilot-instructions.md        # Instructions toujours actives pour Copilot (résumé de CLAUDE.md)
│   ├── instructions/                  # Instructions ciblées par type de fichier
│   │   ├── css.instructions.md        # Appliqué automatiquement sur *.css, *.scss
│   │   ├── vue.instructions.md        # Appliqué automatiquement sur *.vue
│   │   └── html.instructions.md       # Appliqué automatiquement sur *.html
│   ├── agents/                        # Custom agents (personas spécialisés pour Copilot)
│   │   ├── reviewer.agent.md          # Agent de revue de code
│   │   └── planner.agent.md           # Agent de planification de tâches
│   ├── prompts/                       # Prompts réutilisables (invoqués manuellement)
│   │   ├── audit-css.prompt.md        # Audit CSS d'un fichier selon les guidelines
│   │   └── audit-a11y.prompt.md       # Audit accessibilité d'un composant
│   └── skills/                        # Skills Copilot-only (optionnel, si besoin de skills distincts)
│
└── .vscode/
    └── settings.json                  # Déclare chat.skillsLocations si skills hors chemins par défaut
```

---

## Rôle de chaque fichier

### `CLAUDE.md` — La constitution du projet

Chargé automatiquement au démarrage de chaque session Claude Code, et reconnu par Copilot comme instructions toujours actives. Contient les **règles non-négociables et concises** : stack, commandes pnpm, conventions CSS cardinales, règles d'accessibilité, conventions Vue et Git.

Principe clé : **court et précis**. Plus ce fichier est long, moins les règles sont suivies. Les détails sont délégués aux skills.

### `CLAUDE.local.md` — Préférences personnelles

Même format que `CLAUDE.md`, mais réservé aux préférences individuelles non partagées (chemin local, outils perso, style de réponse). À ajouter dans `.gitignore`.

### `AGENTS.md` — Protocole pour les agents autonomes

Actif uniquement quand un agent travaille de façon autonome (Copilot coding agent, Claude Code en mode agent). Décrit **comment agir** plutôt que comment écrire du code : quelles commandes lancer, dans quel ordre, comment valider avant de commiter, quoi faire en cas de blocage.

Ne duplique pas les règles de `CLAUDE.md` — les complète pour le contexte autonome.

### `.claude/rules/*.md` — Règles modulaires

Fragments de règles référencés depuis `CLAUDE.md` via `@rules/css.md`. Permet de garder le fichier principal court tout en conservant des règles détaillées accessibles. Chargés uniquement quand Claude les lit explicitement.

### `.claude/commands/*.md` — Slash commands personnalisés

Chaque fichier `nom.md` dans ce dossier crée une commande `/project:nom` dans Claude Code. Peut contenir des commandes shell (syntaxe `` !`commande` ``) dont la sortie est injectée dans le prompt. Exemple : `/project:audit-a11y` lance une analyse des fichiers Vue modifiés.

### `.claude/skills/` — Skills partagés ⭐

Dossier central pour les skills. **Reconnu automatiquement par Claude Code et par Copilot** sans configuration supplémentaire. Chaque skill est un sous-dossier contenant au minimum un `SKILL.md` avec frontmatter YAML, et optionnellement des fichiers de référence, templates ou scripts.

Les skills sont chargés **à la demande** selon la pertinence de la tâche — ils ne consomment pas de contexte en permanence.

### `.github/copilot-instructions.md` — Instructions Copilot toujours actives

Équivalent de `CLAUDE.md` pour Copilot. Peut simplement renvoyer vers `CLAUDE.md` via un lien Markdown pour éviter la duplication. Appliqué à toutes les requêtes chat dans VS Code.

### `.github/instructions/*.instructions.md` — Instructions ciblées par fichier

Injectées automatiquement par Copilot **uniquement quand il travaille sur des fichiers correspondant au pattern** défini dans le frontmatter `applyTo`. Idéal pour les règles CSS/Vue/HTML : elles n'encombrent pas le contexte quand on travaille sur du JavaScript ou de la config.

Exemple de frontmatter :

```yaml
---
applyTo: "**/*.css,**/*.scss"
---
```

### `.github/agents/*.agent.md` — Custom agents Copilot

Personas spécialisés sélectionnables manuellement dans le chat Copilot. Chaque agent a ses propres instructions, outils autorisés et éventuellement un modèle préféré. Exemples utiles : un agent "Reviewer" (lecture seule, pas de modification), un agent "Planner" (génère un plan sans écrire de code).

### `.github/prompts/*.prompt.md` — Prompts réutilisables

Invoqués manuellement via `/nom-du-prompt` dans le chat Copilot. Utiles pour les tâches récurrentes mais non automatiques : audit CSS d'un fichier spécifique, génération d'un composant accessible depuis un design, revue de PR selon les guidelines.

### `.vscode/settings.json` — Configuration VS Code

Nécessaire uniquement si des skills se trouvent hors des chemins détectés automatiquement. Exemple :

```json
{
  "chat.skillsLocations": [".claude/skills/**", "docs/skills/**"]
}
```

---

## Reconnaissance des skills : Claude Code vs Copilot

| Emplacement          | Claude Code      | Copilot VS Code  | Copilot agent cloud | Configuration requise                     |
| -------------------- | ---------------- | ---------------- | ------------------- | ----------------------------------------- |
| `.claude/skills/`    | ✅ Auto          | ✅ Auto          | ✅ Auto             | Aucune                                    |
| `.github/skills/`    | ❌               | ✅ Auto          | ✅ Auto             | Aucune                                    |
| `~/.claude/skills/`  | ✅ Auto (global) | ✅ Auto (global) | ❌                  | Aucune                                    |
| `~/.copilot/skills/` | ❌               | ✅ Auto (global) | ❌                  | Aucune                                    |
| `~/.agents/skills/`  | ❌               | ✅ Auto (global) | ✅                  | Aucune                                    |
| Autre chemin custom  | Via import `@`   | ❌               | ❌                  | `chat.skillsLocations` dans settings.json |

**Recommandation pour un projet mixte :** placer tous les skills dans `.claude/skills/` — c'est le seul chemin reconnu automatiquement par les deux outils sans aucune configuration.

---

## Chargement des instructions : ce qui est actif et quand

| Fichier / Dossier                        | Claude Code       | Copilot VS Code     | Moment de chargement                    |
| ---------------------------------------- | ----------------- | ------------------- | --------------------------------------- |
| `CLAUDE.md` (racine)                     | ✅                | ✅                  | Toujours, dès le démarrage              |
| `CLAUDE.local.md`                        | ✅                | ❌                  | Toujours (usage local uniquement)       |
| `AGENTS.md`                              | En mode agent     | En mode agent cloud | Agent autonome uniquement               |
| `.claude/rules/*.md`                     | Si référencé      | ❌                  | Sur demande explicite                   |
| `.claude/skills/`                        | Auto si pertinent | Auto si pertinent   | À la demande, selon la tâche            |
| `.github/copilot-instructions.md`        | ❌                | ✅                  | Toujours                                |
| `.github/instructions/*.instructions.md` | ❌                | ✅                  | Si fichier ouvert correspond au pattern |
| `.github/agents/*.agent.md`              | ❌                | ✅                  | Sélection manuelle dans le chat         |
| `.github/prompts/*.prompt.md`            | ❌                | ✅                  | Invocation manuelle `/nom`              |

---

## Principe de découpage : quoi mettre où

```
Une règle toujours nécessaire, courte             → CLAUDE.md / copilot-instructions.md
Une règle liée à un type de fichier spécifique    → .github/instructions/*.instructions.md
Des guidelines complètes (> 1 page)               → .claude/skills/ (SKILL.md + fichier dédié)
Une procédure répétable avec ressources            → .claude/skills/ (SKILL.md + scripts/templates)
Un audit ou une tâche déclenchée manuellement     → .github/prompts/*.prompt.md
Un protocole pour agent autonome                  → AGENTS.md
Un persona spécialisé pour le chat Copilot        → .github/agents/*.agent.md
```

---

## Structure d'un `SKILL.md`

```markdown
---
name: nom-du-skill # Nom en minuscules avec tirets (max 64 car.)
description: >- # Description précise : quand utiliser ce skill (max 1024 car.)
  Ce skill s'active quand on génère, modifie ou audite du CSS.
  Inclut les conventions BEM, custom properties, responsive et accessibilité.
---

# Titre du skill

Résumé des points prioritaires à appliquer en premier.

Pour les règles complètes, voir [guidelines.md](./guidelines.md).
```

Le frontmatter est ce que l'agent lit en premier (découverte). Le corps du `SKILL.md` est chargé si la tâche correspond. Les fichiers référencés (`guidelines.md`, templates…) ne sont chargés que s'ils sont explicitement mentionnés dans les instructions — c'est le **chargement progressif** qui préserve le contexte.

---

## Fichiers à ajouter dans `.gitignore`

```
CLAUDE.local.md
.claude/projects/
```

---

_Dernière mise à jour : avril 2026_
