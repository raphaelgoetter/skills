# AGENTS.md

> Instructions pour les agents autonomes (Copilot coding agent, Claude Code en mode agent).
> Ce fichier décrit comment l'agent doit **explorer, construire, tester et valider** ses modifications
> avant de les soumettre. Il complète `CLAUDE.md` sans le remplacer.

---

## Exploration initiale

Avant toute modification, l'agent doit :

1. Lire `CLAUDE.md` pour les règles permanentes du projet
2. Lire `package.json` pour connaître les scripts disponibles
3. Identifier les fichiers concernés par la tâche avant d'en modifier un seul
4. Ne pas supposer la structure du projet — la vérifier avec les outils disponibles

---

## Commandes autorisées

L'agent peut exécuter les commandes suivantes sans validation humaine :

```bash
pnpm install          # installation des dépendances
pnpm dev              # serveur de développement (lecture seule, ne pas laisser tourner)
pnpm build            # build de production
pnpm lint             # lint JS/CSS
pnpm lint:fix         # correction automatique des erreurs de lint
pnpm test             # tests unitaires
pnpm test:run         # tests en mode CI (sans watch)
```

**Commandes interdites sans validation explicite :**

```bash
pnpm add *            # installation de nouvelle dépendance
pnpm remove *         # suppression de dépendance
git push              # push vers le dépôt distant
rm -rf *              # suppression de fichiers ou dossiers
```

---

## Workflow de validation avant commit

L'agent **doit** exécuter ces étapes dans l'ordre avant de proposer ou créer un commit :

### 1. Lint

```bash
pnpm lint
```

- Si des erreurs sont détectées : tenter `pnpm lint:fix`, puis corriger manuellement ce qui reste
- Ne pas commiter si des erreurs de lint subsistent

### 2. Build

```bash
pnpm build
```

- Le build doit se terminer sans erreur ni warning bloquant
- En cas d'erreur TypeScript ou de module manquant : corriger avant de continuer

### 3. Tests

```bash
pnpm test:run
```

- Tous les tests existants doivent passer
- Si un test échoue à cause d'une modification intentionnelle : mettre à jour le test et le documenter dans le message de commit

### 4. Vérification accessibilité (si fichiers HTML/Vue modifiés)

Pour tout fichier `.vue` ou `.html` modifié, vérifier manuellement :

- Présence des attributs `alt` sur les images
- Labels associés à chaque champ de formulaire
- Focus visible sur les éléments interactifs
- Hiérarchie des titres non interrompue

Consulter le skill `/accessibilite` pour les critères complets.

---

## Règles pour les modifications CSS

Pour tout fichier `.css`, `.scss` ou style dans un `.vue` :

- Vérifier qu'aucune valeur de couleur n'est hardcodée (utiliser les custom properties)
- Vérifier que les unités respectent les conventions (`rem`, `px`, `%`, `fr`)
- Lancer `pnpm lint` après toute modification CSS

Consulter le skill `/css-guidelines` pour les règles complètes.

---

## Règles pour les composants Vue

Pour tout nouveau composant ou modification de composant existant :

- Vérifier que `<script setup>` est utilisé (pas d'Options API)
- Vérifier que les props sont typées via `defineProps`
- Vérifier que les événements émis sont déclarés via `defineEmits`
- S'assurer qu'aucune logique métier ne se trouve dans le template

Consulter le skill `/composant-vue` pour les patterns standards.

---

## Format des commits

Messages en anglais, format Conventional Commits strict :

```
type(scope): description courte en impératif

Corps optionnel : explication du pourquoi, pas du quoi.
```

**Types autorisés :**

| Type       | Usage                                               |
| ---------- | --------------------------------------------------- |
| `feat`     | Nouvelle fonctionnalité                             |
| `fix`      | Correction de bug                                   |
| `style`    | Modifications CSS/visuelles sans impact fonctionnel |
| `refactor` | Réécriture sans changement de comportement          |
| `a11y`     | Amélioration d'accessibilité                        |
| `docs`     | Documentation uniquement                            |
| `test`     | Ajout ou correction de tests                        |
| `chore`    | Maintenance, dépendances, config                    |

**Exemples corrects :**

```
feat(nav): add skip-to-content link for keyboard navigation
fix(button): restore focus outline removed by reset
a11y(modal): trap focus inside dialog on open
style(card): replace hardcoded color with --color-surface
```

---

## Ce que l'agent ne doit jamais faire

- Modifier `vite.config.*`, `tsconfig.*`, `.eslintrc.*` sans demande explicite
- Modifier `package.json` (scripts, dépendances, version)
- Supprimer des fichiers ou des dossiers
- Effectuer un `git push` ou créer une Pull Request sans validation
- Contourner un test qui échoue en le supprimant ou en le désactivant (`skip`, `todo`)
- Ajouter des `console.log` ou commentaires `TODO` dans le code livré
- Générer du code inaccessible (éléments interactifs non focusables, contrastes insuffisants)

---

## En cas de blocage

Si l'agent ne peut pas compléter la tâche proprement (build cassé, test impossible à corriger,
ambiguïté sur l'intention), il doit :

1. Arrêter sans commiter
2. Décrire précisément le blocage
3. Lister les options possibles avec leurs compromis
4. Attendre une décision humaine
