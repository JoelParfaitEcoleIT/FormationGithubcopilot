# Exercice pratique — TaskBoard avec GitHub Copilot (HTML/CSS)

**10 étapes, 3 niveaux : 🟢 Facile · 🟡 Intermédiaire · 🔴 Pro**
Digital House Company — Joël Parfait Kuate — hello@dhcompany.pro

Ce guide vous fait pratiquer sur [`codebase_taskboard/`](codebase_taskboard/), un site **HTML et CSS uniquement — aucun JavaScript** — pensé pour un public débutant : vous n'avez besoin d'aucune connaissance de programmation pour suivre cet exercice, seulement des bases de HTML et CSS. Chaque étape propose 3 pistes — choisissez la vôtre, et changez de piste à tout moment.

---

## 0. Avant de commencer

### 0.1 Les 3 niveaux

| Niveau | Pour qui | Ce que vous faites |
|---|---|---|
| 🟢 **Facile** | Aucune expérience de Copilot | Vous recopiez le prompt fourni, tel quel |
| 🟡 **Intermédiaire** | À l'aise avec le HTML/CSS, moins avec Copilot | Vous adaptez le prompt à un autre élément du même fichier |
| 🔴 **Pro** | Déjà utilisateur de Copilot | Vous définissez votre propre périmètre, sans prompt tout prêt |

### 0.2 Rappels

> **🔒 Sécurité** — aucune donnée réelle. `codebase_taskboard/` est entièrement fictif.
> **💰 Sobriété** — ciblez un fichier précis, groupez vos questions, changez de session entre deux sujets.
> **👀 Vérification** — chaque proposition de Copilot est relue avant d'être acceptée.

### 0.3 Sources utilisées dans ce guide

- **GitHub Docs** — [docs.github.com/copilot](https://docs.github.com/en/copilot)
- **VS Code Docs, Custom instructions** — [code.visualstudio.com/docs/agent-customization/custom-instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions)
- **awesome-copilot** (dépôt communautaire officiel) — [github.com/github/awesome-copilot](https://github.com/github/awesome-copilot)

### 0.4 Démarrer

Ouvrez [`codebase_taskboard/index.html`](codebase_taskboard/index.html) dans un navigateur. Ouvrez le dossier `codebase_taskboard/` dans votre éditeur pour utiliser Copilot dessus.

```
codebase_taskboard/
  index.html                    Tableau des tâches + formulaire (statique)
  task-detail.html               Détail d'une tâche
  about.html                     Présentation du projet
  css/variables.css              Couleurs, espacements, arrondis
  css/base.css                   Remise à zéro et styles de base
  css/layout.css                 Structure des pages
  css/components.css             Cartes, badges, boutons, formulaire
  css/responsive.css             Adaptation aux petits écrans
  css/legacy-styles.css          Ancien fichier de styles à améliorer
  docs/architecture.md            Documentation existante
  docs/checklist-accessibilite.md Points à vérifier avant de livrer
```

**Aucun JavaScript dans ce projet.** Tout ce que vous ferez avec Copilot portera sur du HTML et du CSS — deux langages que l'on peut lire et comprendre sans expérience de programmation, ce qui rend cet exercice accessible à un vrai débutant.

---

## Étape 1 — Découvrir le projet

**Objectif : cartographier TaskBoard avant d'y toucher.**

- 🟢 Ouvrez `docs/architecture.md` et `README.md`. Notez les 3 pages HTML et les 6 fichiers CSS, et leur rôle en une ligne chacun.
- 🟡 Ouvrez Copilot Chat, tapez `@workspace Décris l'architecture de ce projet en 4 lignes.` Comparez avec vos notes.
- 🔴 Identifiez, sans les ouvrir en détail, le fichier CSS le plus « à risque » à modifier (probabilité de casser l'apparence d'une autre page) et justifiez en une phrase.

**✅ Checklist** : je sais où sont la structure (HTML), l'apparence (CSS), et le fichier à améliorer.

---

## Étape 2 — Cibler avec `#file` et `#selection`

**Objectif : pratiquer le ciblage précis plutôt que `#codebase`.**
**Source : GitHub Docs, « Chat cheat sheet » — docs.github.com/en/copilot/reference/chat-cheat-sheet.**

- 🟢 Recopiez : `#file:index.html` `/explain` `Explique la structure de cette page en langage simple.`
- 🟡 Sélectionnez le bloc `<section class="board">` dans `index.html`, puis : `#selection` `Explique ce que fait ce bloc et comment il est structuré.`
- 🔴 Posez la même question à `css/components.css` avec `#file` puis avec `#codebase`. Comparez précision et temps de réponse ; notez votre conclusion.

**✅ Checklist** : je sais quand utiliser `#file` plutôt que `#codebase`.

---

## Étape 3 — Créer les instructions de dépôt

**Objectif : personnaliser Copilot pour tout le projet TaskBoard.**
**Source : VS Code Docs, « Custom instructions » — code.visualstudio.com/docs/agent-customization/custom-instructions.**

- 🟢 Créez `codebase_taskboard/.github/copilot-instructions.md` avec ce contenu :

  ```markdown
  # Copilot instructions — TaskBoard
  ## Conventions
  - HTML5 sémantique, CSS pur (aucun framework, aucun JavaScript)
  - Nommage des classes CSS : kebab-case (ex. card-title, form-panel)
  - Toutes les couleurs et espacements passent par des variables CSS (css/variables.css)
  ## Contraintes
  - Ne jamais introduire de JavaScript dans ce projet
  - Ne jamais introduire de donnée réelle ou de secret
  ```

- 🟡 Créez en plus `codebase_taskboard/.github/instructions/legacy.instructions.md` :

  ```markdown
  ---
  applyTo: "css/legacy-styles.css"
  description: Conventions pour le CSS hérité
  ---
  Ce fichier est un ancien CSS, en attente de nettoyage. Toute proposition
  doit garder EXACTEMENT le même rendu visuel.
  ```

- 🔴 Ajoutez le champ optionnel `excludeAgent` à ce fichier, et testez le paramètre `chat.includeApplyingInstructions` dans votre éditeur. Documentez ce que chacun change.

**✅ Checklist** : une question neutre sur le projet respecte maintenant le style demandé (pas de JS proposé, variables CSS utilisées).

---

## Étape 4 — Améliorer un code existant

**Objectif : rendre `css/legacy-styles.css` propre, sans changer le rendu visuel.**

- 🟢 Recopiez :

  ```text
  #file:css/legacy-styles.css
  /explain
  Liste les problèmes de ce fichier CSS (répétitions, !important, valeurs
  non variabilisées), sans corriger.
  ```

  Puis :

  ```text
  Réécris ces règles en réutilisant les variables de css/variables.css
  (--priority-low, --priority-medium, --priority-high, --priority-critical,
  --radius-pill), sans aucun !important. Garde EXACTEMENT le même rendu.
  ```

- 🟡 Demandez en plus de fusionner les 4 classes `.old-badge-*` en une seule règle générique, sur le modèle de `.badge[data-priority="..."]` déjà présent dans `components.css`.
- 🔴 Comparez visuellement, dans le navigateur, le rendu avant/après en ouvrant `index.html` avant et après votre modification (capture d'écran ou description écrite des différences éventuelles).

**✅ Checklist** : le rendu visuel est identique ; plus aucun `!important` ni valeur de couleur non variabilisée.

**📦 Livrable** : la version améliorée de `legacy-styles.css`, et votre preuve de non-régression visuelle.

---

## Étape 5 — Vérifier l'accessibilité et la validité

**Objectif : remplacer les « tests » par une vérification adaptée au HTML/CSS — il n'y a pas de logique à tester ici, mais une qualité de balisage à contrôler.**

- 🟢 Recopiez :

  ```text
  #file:index.html
  Vérifie l'accessibilité de cette page : labels de formulaire, ordre des
  titres, attributs alt, contraste des badges. Liste les problèmes trouvés.
  ```

  Comparez la réponse à `docs/checklist-accessibilite.md`.

- 🟡 Avant de demander à Copilot, cochez vous-même la checklist d'accessibilité sur `task-detail.html`. Comparez ensuite avec ce que Copilot trouve.
- 🔴 Demandez explicitement : « Quels problèmes d'accessibilité n'as-tu peut-être pas détectés automatiquement ? » (contraste réel des couleurs, lecteur d'écran) et notez la réponse.

**✅ Checklist** : `docs/checklist-accessibilite.md` est entièrement cochée pour `index.html`.

**📦 Livrable** : la checklist complétée, et la liste des corrections effectuées.

---

## Étape 6 — Documenter et préparer une revue

**Objectif : préparer une explication claire pour un relecteur humain.**

- 🟢 Sélectionnez le bloc `.form-panel` dans `css/components.css`, puis : `#selection` `Ajoute un commentaire CSS qui explique le rôle de ce bloc.`
- 🟡 Rédigez une description de changement pour votre travail de l'Étape 4 :

  ```markdown
  ## Résumé
  ## Détail
  ## Risques
  ## Comment tester
  ```

- 🔴 Demandez à Copilot une checklist de revue orientée HTML/CSS pour TaskBoard, puis complétez-la avec 2 critères propres à votre équipe.

**✅ Checklist** : n'importe quel collègue pourrait comprendre votre changement sans relire tout le fichier.

---

## Étape 7 — Utiliser l'Agent mode

**Objectif : confier une tâche multi-fichiers, sous supervision.**
**Source : GitHub Blog, « The difference between coding agent and agent mode in GitHub Copilot ».**

- 🟢 Activez l'Agent mode. Demandez : « Ajoute une 4e colonne "Annulé" au tableau de `index.html`, avec le style correspondant dans `css/layout.css` (déjà prévu par un commentaire TODO). »
- 🟡 Observez la liste des fichiers modifiés avant validation. Validez ou refusez chaque changement séparément.
- 🔴 Étendez la demande : ajoutez aussi une nouvelle valeur de badge « annulée » dans `css/variables.css` et `css/components.css`. Interrompez volontairement l'agent en cours de tâche pour vérifier le contrôle humain.

**✅ Checklist** : rien n'a été appliqué sans votre validation explicite ; le rendu reste cohérent sur les 3 pages.

---

## Étape 8 — Créer un prompt file réutilisable

**Objectif : industrialiser une tâche récurrente d'équipe.**
**Source : VS Code Docs, « Prompt files » — code.visualstudio.com/docs/copilot/customization/prompt-files ; github.com/github/awesome-copilot.**

- 🟢 Créez `codebase_taskboard/.github/prompts/code-review.prompt.md` :

  ```markdown
  ---
  description: Revue de code standard TaskBoard (HTML/CSS)
  agent: ask
  tools: [read, search]
  ---
  Analyse le diff fourni. Vérifie : sémantique HTML, accessibilité,
  usage des variables CSS (pas de couleur ou d'espacement en dur),
  absence de JavaScript. Restitue une checklist avec un niveau de
  risque (faible / moyen / élevé).
  ```

- 🟡 Invoquez-le avec `/code-review` sur votre travail de l'Étape 4.
- 🔴 Créez un second prompt file `scaffold-page.prompt.md` pour générer le squelette d'une nouvelle page HTML respectant la structure des 3 pages existantes (en-tête, nav, main, footer, liens CSS).

**✅ Checklist** : `/code-review` fonctionne et produit une checklist exploitable.

---

## Étape 9 — Créer un agent personnalisé

**Objectif : définir un périmètre restreint pour Copilot.**
**Source : VS Code Docs, « Custom agents » — code.visualstudio.com/docs/copilot/customization/custom-agents ; github.com/github/awesome-copilot.**

- 🟢 Créez `codebase_taskboard/.github/agents/reviewer.agent.md` :

  ```markdown
  ---
  name: reviewer
  description: Analyse uniquement le HTML/CSS de TaskBoard, ne modifie jamais rien
  tools: [read, search]
  ---
  Tu es un agent de revue pour TaskBoard (HTML/CSS uniquement). Tu ne dois
  JAMAIS proposer de modification directe des fichiers, ni suggérer
  d'ajouter du JavaScript. Ta sortie est toujours structurée : constat,
  risque, recommandation.
  ```

- 🟡 Invoquez cet agent sur `css/legacy-styles.css` et vérifiez qu'il ne propose aucune modification de fichier.
- 🔴 Créez un second agent `planner.agent.md` qui ne produit qu'un plan, avec un champ `handoffs` qui transmet la main à `reviewer` pour validation. Testez le duo sur : « Je veux ajouter une page de statistiques au projet. »

**✅ Checklist** : l'agent `reviewer` respecte strictement son périmètre déclaré (aucune modification, aucune suggestion de JS).

---

## Étape 10 — Bonus Pro : MCP, hooks, workflow

*Réservée à la piste 🔴 Pro. En 🟢/🟡, lisez cette étape pour comprendre le principe.*

**Source : GitHub Docs, « Model Context Protocol (MCP) », « About GitHub agentic workflows », « About plugins » (consultés le 19/07/2026).**

- 🔴 Rédigez une note de gouvernance MCP en 4 lignes pour TaskBoard (toolsets autorisés, qui active, fréquence de revue).
- 🔴 Créez un `hooks.json` minimal qui rappelle de relire `docs/checklist-accessibilite.md` après toute modification d'un fichier HTML.
- 🔴 Rédigez (sans forcément l'exécuter) un mini-workflow agentique `.github/workflows/weekly-a11y-check.md` :

  ```markdown
  ---
  on: weekly
  permissions:
    contents: read
  engine: copilot
  ---
  Chaque semaine, relis les 3 pages HTML de TaskBoard et vérifie
  qu'elles respectent toujours docs/checklist-accessibilite.md.
  Signale toute régression.
  ```

- 🔴 Regroupez mentalement `reviewer.agent.md` (Étape 9), le prompt file (Étape 8) et ce workflow dans un plugin `taskboard-plugin/` avec un `plugin.json` minimal.

**✅ Checklist finale** : je peux expliquer la différence entre un agent, un skill, un hook, un plugin et un workflow agentique — même sans avoir écrit une ligne de JavaScript aujourd'hui.

---

## 📦 Livrable final de l'exercice

1. `legacy-styles.css` amélioré + preuve de non-régression visuelle (Étape 4).
2. Checklist d'accessibilité complétée pour `index.html` (Étape 5).
3. Commentaire CSS + description de changement (Étape 6).
4. Résultat de l'Agent mode : la colonne « Annulé » ajoutée (Étape 7).
5. `copilot-instructions.md`, prompt file, agent personnalisé (Étapes 3, 8, 9).
6. (Pro) Note de gouvernance MCP, `hooks.json`, workflow agentique (Étape 10).

---

*Guide préparé par Digital House Company — Joël Parfait Kuate · hello@dhcompany.pro.*
*Sources : docs.github.com/copilot, code.visualstudio.com/docs/agent-customization/custom-instructions, github.com/github/awesome-copilot — consultées le 19/07/2026.*
