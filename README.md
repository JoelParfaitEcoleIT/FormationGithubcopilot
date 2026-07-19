# Atelier pratique GitHub Copilot — TaskBoard (HTML/CSS uniquement)

Dossier autonome, basé sur trois sources officielles : [docs.github.com/copilot](https://docs.github.com/en/copilot), [code.visualstudio.com/docs/agent-customization/custom-instructions](https://code.visualstudio.com/docs/agent-customization/custom-instructions), et le dépôt communautaire [github.com/github/awesome-copilot](https://github.com/github/awesome-copilot).

**Aucun JavaScript dans cet atelier** — codebase et exemples sont volontairement limités à HTML et CSS, pour rester accessibles à un public de développeurs débutants, sans notion de programmation préalable.

## Contenu

1. **[Support_Formation_124_Slides.html](Support_Formation_124_Slides.html)** — le support de cours, **124 slides** (version interactive, navigable). Un bouton **« ⬇ Exporter en PDF »** en haut à droite ouvre directement la boîte d'impression du navigateur (choisir « Enregistrer au format PDF ») ; une **[version PDF déjà générée](Support_Formation_124_Slides.pdf)** est aussi fournie.
   Chaque notion est expliquée en paragraphes développés, en commençant par les fondamentaux (IA, types et niveaux d'IA, modèles, LLM, Arena.ai), puis toutes les commandes — **chacune avec un exemple prêt à copier-coller sur TaskBoard**, y compris les 9 variables `#` une par une — le fonctionnement détaillé des coûts, tout l'écosystème avancé étape par étape (Agent mode, Cloud agent, agents personnalisés et sous-agents via `handoffs`, skills, plugins, hooks, MCP avec Context7, workflows agentiques), et la personnalisation officielle (`copilot-instructions.md`, `*.instructions.md`, `AGENTS.md`, `CLAUDE.md`, prompt files). Une section dédiée distingue **écrire à Copilot (inline, dans le code)** et **écrire à Copilot Chat (conversationnel)**, avec des exemples développeur sur des fichiers réels du projet. Chaque slide technique cite sa source ; une question est posée à l'audience à chaque étape clé.

2. **[Exercice_50_Actions_Cours.md](Exercice_50_Actions_Cours.md)** — guide formateur, **50 actions** pas à pas pour maîtriser Copilot sur TaskBoard, chacune avec un repère/réponse attendue à partager en séance. Structuré en 12 phases (mise en place, variables `#`, participants `@`, commandes slash, raccourcis, modèles, Agent mode, Cloud agent, agents personnalisés/sous-agents, skills, plugins/hooks/MCP/workflows, instructions et bilan) + une grille de correction rapide.

3. **[Exercice_50_Actions_Participant.html](Exercice_50_Actions_Participant.html)** — la même trame de 50 actions, **à remplir directement dans le navigateur** (un champ réponse par action, sans les repères formateur), avec un bouton **« ⬇ Exporter en PDF »** pour que chaque participant génère et remette sa copie complétée en fin de formation.

4. **[Exercice_Pratique_10_Etapes_3_Niveaux.md](Exercice_Pratique_10_Etapes_3_Niveaux.md)** — exercice complémentaire plus court, 10 étapes en 3 pistes (🟢 Facile · 🟡 Intermédiaire · 🔴 Pro), pour une session plus courte ou une pratique en autonomie après la formation.

5. **[codebase_taskboard/](codebase_taskboard/)** — la codebase d'exercice, **12 fichiers HTML/CSS, aucun JavaScript**, fonctionnelle et vérifiée (aucune installation : ouvrez `index.html`). Un fichier CSS volontairement mal écrit (`css/legacy-styles.css`) sert de cible à l'exercice d'amélioration de code.

## Différence avec les autres versions du dossier de formation

Ce dossier est indépendant des versions précédentes (`Version_Facile_Debutant/`, notebooks Python `Ateliers/`). Il s'appuie sur une codebase **front-end HTML/CSS pure** — choix délibéré pour un public débutant — et va plus loin sur l'écosystème avancé de Copilot tout en restant accessible grâce aux exercices en plusieurs niveaux.
