# Prompt — Personnalisation des fichiers IA selon le projet

> Ce prompt s'utilise **une seule fois**, au démarrage d'un nouveau projet,
> après avoir copié l'architecture IA type dans le dépôt.
> Le lancer depuis la racine du projet dans Claude Code ou Copilot agent mode.

---

## Prompt

```
Tu es un expert en configuration d'outils IA pour projets web.
Ta mission : personnaliser les fichiers de configuration IA de ce projet
en te basant exclusivement sur sa documentation existante.

---

## Étape 1 — Lecture obligatoire avant toute modification

Lis les fichiers suivants dans cet ordre exact, sans rien modifier :

1. `README.md` — documentation principale du projet (stack, objectifs, conventions, équipe)
2. `CLAUDE.md` — état actuel du fichier à personnaliser
3. `AGENTS.md` — état actuel du fichier à personnaliser
4. `.github/copilot-instructions.md` — état actuel du fichier à personnaliser
5. `.github/instructions/css.instructions.md`
6. `.github/instructions/vue.instructions.md`
7. `.github/instructions/html.instructions.md`

Puis liste les skills présents dans `.claude/skills/` sans les lire en entier :
seuls les frontmatters YAML (`name`, `description`) de chaque `SKILL.md` sont nécessaires.

Si `README.md` est absent ou vide, **arrête-toi ici** et demande à l'utilisateur
de le renseigner avant de continuer. Ne génère rien sans cette source de vérité.

---

## Étape 2 — Extraction des informations projet

Depuis `README.md` uniquement, extrais et liste explicitement :

- Nom du projet et description courte
- Stack technique complet (langages, frameworks, bibliothèques)
- Package manager et commandes disponibles (dev, build, lint, test…)
- Structure des dossiers `src/` si documentée
- Conventions de code mentionnées (nommage, formatage, patterns)
- Outils de qualité (linter, formatter, outil de test, CI)
- Conventions de commit ou workflow Git
- Contraintes spécifiques (navigateurs cibles, performance, accessibilité, i18n…)
- Taille et organisation de l'équipe si mentionnée

Présente ce résumé avant de commencer toute modification.
Attends une confirmation ou correction de l'utilisateur avant de passer à l'étape 3.

---

## Étape 3 — Règles de personnalisation

Applique ces règles sans exception pour chaque fichier à modifier :

### Ce qui doit être adapté
- Le nom du projet, la description, les objectifs
- Les commandes exactes (pnpm/npm/yarn/bun, noms des scripts réels)
- Les technologies effectivement utilisées (supprimer ce qui ne s'applique pas)
- Les conventions mentionnées dans README.md
- Les chemins de dossiers si la structure src/ est documentée
- La table des skills : ne lister que les skills réellement présents dans `.claude/skills/`

### Ce qui ne doit jamais être modifié
- Le contenu des fichiers dans `.claude/skills/` — ce sont des sources de vérité intouchables
- Le contenu des fichiers dans `.claude/rules/`
- Les frontmatters YAML des skills (`name`, `description`)
- La structure et le format des fichiers (sections, titres, ordre)
- Les règles génériques qui s'appliquent à tous les projets
  (ex. : "ne jamais muter les props", "focus visible obligatoire")

### En cas d'information manquante dans README.md
- Ne pas inventer ni supposer
- Conserver la valeur générique du fichier type avec un commentaire :
  `<!-- TODO: à préciser selon le projet -->`
- Signaler en fin de génération tous les TODOs laissés

---

## Étape 4 — Fichiers à personnaliser

Modifie les fichiers suivants dans cet ordre.
Pour chaque fichier : affiche le contenu complet final, pas un diff.

### `CLAUDE.md`

Personnaliser :
- Section "Projet" : nom, description, stack réel, commandes réelles
- Section "CSS" : ajuster les règles cardinales si des conventions spécifiques
  sont mentionnées dans README.md (ex. : usage de Tailwind, CSS Modules, SCSS…)
- Section "Vue.js" ou équivalent : adapter au framework réel du projet
  (si ce n'est pas Vue, réécrire la section pour le bon framework)
- Section "Git" : adapter aux conventions de commit du projet si précisées
- Section "Skills disponibles" : ne lister que les skills présents dans `.claude/skills/`,
  avec leur chemin exact et leur description issue du frontmatter

Ne pas toucher :
- Section "Accessibilité" — règles universelles
- Section "Ce que Claude ne doit pas faire" — valable pour tous les projets
- Section "Comportement général"

### `AGENTS.md`

Personnaliser :
- Section "Commandes autorisées" : remplacer par les commandes réelles du projet
- Section "Commandes interdites" : ajuster si certaines commandes du projet
  sont potentiellement destructrices
- Section "Workflow de validation" : adapter les étapes aux outils réels
  (ex. : si pas de tests → documenter pourquoi et ce qui remplace)
- Section "Règles pour les modifications CSS/Vue/HTML" : adapter au stack réel

Ne pas toucher :
- Section "Exploration initiale"
- Section "En cas de blocage"
- Format et types des commits

### `.github/copilot-instructions.md`

Doit rester un résumé autonome et concis de `CLAUDE.md` personnalisé.
Reprendre les mêmes adaptations que CLAUDE.md, version encore plus courte.
Maximum 60 lignes.

### `.github/instructions/*.instructions.md`

Pour chaque fichier d'instructions ciblé :
- Vérifier que le pattern `applyTo` correspond aux extensions réellement utilisées
- Ajuster la référence au skill si le nom du dossier de skill est différent
- Ne modifier que le frontmatter et les liens — pas les règles elles-mêmes

---

## Étape 5 — Récapitulatif final

À la fin de toutes les modifications, produire :

1. **Liste des fichiers modifiés** avec une ligne décrivant ce qui a changé
2. **Liste des TODOs** : informations manquantes dans README.md
   qui n'ont pas pu être renseignées automatiquement
3. **Vérification de cohérence** : signaler toute contradiction détectée
   entre README.md et les fichiers IA générés
4. **Actions manuelles recommandées** :
   - Compléter les TODOs listés
   - Vérifier que les skills listés dans CLAUDE.md correspondent bien
     aux dossiers présents dans `.claude/skills/`
   - Taper `/skills` dans le chat VS Code pour confirmer la détection par Copilot
   - Commiter les fichiers IA dans le dépôt (sauf `CLAUDE.local.md`)
```

---

## Quand utiliser ce prompt

| Situation                                             | Action                                               |
| ----------------------------------------------------- | ---------------------------------------------------- |
| Nouveau projet, architecture IA copiée, README rédigé | ✅ Lancer ce prompt                                  |
| Nouveau projet, README vide ou absent                 | ✏️ Rédiger README.md d'abord                         |
| Projet existant, mise à jour des guidelines           | ❌ Ne pas utiliser — modifier les skills directement |
| Projet existant, évolution du stack                   | ✅ Lancer ce prompt, il re-synchronise               |

## Fichiers source vs fichiers cibles

```
README.md                              → source de vérité projet (lecture seule)
.claude/skills/**                      → sources de vérité guidelines (lecture seule)
.claude/rules/**                       → sources de vérité règles (lecture seule)
                                              ↓ personnalisation
CLAUDE.md                              → fichier cible ✏️
AGENTS.md                              → fichier cible ✏️
.github/copilot-instructions.md        → fichier cible ✏️
.github/instructions/*.instructions.md → fichier cible ✏️ (frontmatter et liens uniquement)
```
