# Guide des commandes GitHub Copilot CLI

Ce document présente GitHub Copilot CLI, son installation, sa configuration et ses principales commandes, avec une définition en français et des exemples d’utilisation.

> Important : GitHub Copilot CLI évolue rapidement. Les commandes disponibles dépendent de la version installée, du compte GitHub, des politiques de l’organisation, des plugins, des serveurs MCP et de l’activation du mode expérimental. Dans le terminal, utilisez toujours `/help` pour afficher la liste exacte disponible dans votre installation.

# 1. Installer GitHub Copilot CLI

## 1.1 Prérequis

Avant l’installation, vérifiez les éléments suivants :

- un compte GitHub donnant accès à GitHub Copilot ;
- l’autorisation d’utiliser Copilot CLI si le compte est géré par une organisation ou une entreprise ;
- sous Windows, PowerShell 6 ou une version plus récente ;
- pour l’installation avec npm, Node.js 22 ou une version plus récente ;
- Git installé si vous souhaitez travailler sur des dépôts locaux et utiliser les fonctions Git ou GitHub.

Vérifier les versions disponibles :

```powershell
node --version
npm --version
git --version
$PSVersionTable.PSVersion
```

Sous macOS ou Linux :

```bash
node --version
npm --version
git --version
```

## 1.2 Choisir une méthode d’installation

Une seule méthode est nécessaire.

### Méthode A — Windows avec WinGet

Cette méthode est recommandée sur un poste Windows récent.

```powershell
winget install GitHub.Copilot
```

Installer la version de prépublication :

```powershell
winget install GitHub.Copilot.Prerelease
```

### Méthode B — Installation multiplateforme avec npm

Cette méthode fonctionne sous Windows, macOS et Linux avec Node.js 22 ou une version plus récente.

```bash
npm install -g @github/copilot
```

Si le fichier `~/.npmrc` contient `ignore-scripts=true` :

```bash
npm_config_ignore_scripts=false npm install -g @github/copilot
```

Installer la version de prépublication :

```bash
npm install -g @github/copilot@prerelease
```

### Méthode C — macOS ou Linux avec Homebrew

```bash
brew install --cask copilot-cli
```

Installer la version de prépublication :

```bash
brew install --cask copilot-cli@prerelease
```

### Méthode D — macOS ou Linux avec le script officiel

Avec `curl` :

```bash
curl -fsSL https://gh.io/copilot-install | bash
```

Avec `wget` :

```bash
wget -qO- https://gh.io/copilot-install | bash
```

Pour installer dans un dossier personnalisé :

```bash
curl -fsSL https://gh.io/copilot-install | PREFIX="$HOME/.local" bash
```

Assurez-vous ensuite que le dossier contenant l’exécutable appartient à la variable `PATH`.

## 1.3 Vérifier l’installation

Fermez puis rouvrez le terminal si la commande n’est pas immédiatement reconnue.

```bash
copilot --version
```

Afficher l’aide générale :

```bash
copilot help
```

Résultat attendu : la version installée s’affiche et la commande `copilot` est disponible.

## 1.4 Mettre à jour GitHub Copilot CLI

Utilisez la méthode correspondant à l’installation initiale.

### WinGet

```powershell
winget upgrade GitHub.Copilot
```

### npm

```bash
npm install -g @github/copilot@latest
```

### Homebrew

```bash
brew upgrade --cask copilot-cli
```

Depuis une session Copilot CLI, la commande suivante peut également être disponible :

```text
/update
```

Vérifiez ensuite la version :

```bash
copilot --version
```

---

# 2. Configurer GitHub Copilot CLI

## 2.1 Démarrer dans le bon projet

Placez-vous dans le dépôt concerné avant de lancer la CLI.

Sous Windows :

```powershell
cd C:\projets\mon-application
copilot
```

Sous macOS ou Linux :

```bash
cd ~/projets/mon-application
copilot
```

Vous pouvez aussi préciser le dossier au lancement :

```bash
copilot -C ./mon-application
```

## 2.2 Authentifier le compte GitHub

Pour un usage interactif, OAuth est la méthode recommandée.

Depuis le terminal :

```bash
copilot login
```

Ou depuis une session interactive :

```text
/login
```

Copilot affiche un code à usage unique et ouvre une page GitHub dans le navigateur. Saisissez le code, autorisez l’application, puis revenez dans le terminal.

Vérifier le compte actif :

```text
/user show
```

Lister ou changer de compte :

```text
/user list
/user switch
```

### Authentification pour un script, un serveur ou un pipeline CI/CD

Copilot CLI accepte les variables suivantes, dans cet ordre de priorité :

1. `COPILOT_GITHUB_TOKEN` ;
2. `GH_TOKEN` ;
3. `GITHUB_TOKEN`.

Exemple sous Bash :

```bash
export COPILOT_GITHUB_TOKEN="VOTRE_JETON"
copilot -p "Analyse le projet et résume les risques techniques"
```

Exemple sous PowerShell :

```powershell
$env:COPILOT_GITHUB_TOKEN = "VOTRE_JETON"
copilot -p "Analyse le projet et résume les risques techniques"
```

Utilisez un jeton à granularité fine appartenant au compte personnel, avec la permission de compte **Copilot Requests**. N’inscrivez jamais un jeton réel dans un dépôt, un fichier partagé ou un exemple de documentation.

Si GitHub CLI est déjà installé et authentifié, Copilot CLI peut utiliser son jeton en solution de repli :

```bash
gh auth status
copilot
```

## 2.3 Valider la confiance accordée au dossier

Au premier démarrage dans un dossier, Copilot demande si vous faites confiance au répertoire courant et à ses sous-dossiers.

Choisissez :

- la session actuelle uniquement pour un dépôt inconnu, temporaire ou téléchargé ;
- cette session et les prochaines uniquement pour un dossier que vous contrôlez durablement.

Les dossiers approuvés de façon permanente sont gérés dans :

```text
~/.copilot/config.json
```

Sous Windows, le chemin équivalent est généralement :

```text
$HOME\.copilot\config.json
```

La variable d’environnement `COPILOT_HOME` permet de déplacer le répertoire de configuration.

## 2.4 Initialiser les instructions du dépôt

Dans le dépôt :

```text
/init
```

Ou directement depuis le terminal :

```bash
copilot init
```

Cette opération analyse le projet et crée ou met à jour :

```text
.github/copilot-instructions.md
```

Après l’initialisation, vérifiez que le fichier précise au minimum :

- l’architecture du projet ;
- les commandes d’installation, de build, de test et de lint ;
- les conventions de code ;
- les fichiers qui ne doivent pas être modifiés ;
- les règles de sécurité et de confidentialité ;
- les critères à respecter avant de considérer une tâche comme terminée.

Exemple :

```markdown
# Instructions du dépôt

- Utiliser TypeScript en mode strict.
- Exécuter `npm run lint`, `npm test` et `npm run build` avant de terminer.
- Ne jamais modifier une migration déjà déployée.
- Ne jamais ajouter de secret, de jeton ou de mot de passe dans le dépôt.
- Demander une validation avant toute commande de déploiement ou tout `git push`.
```

## 2.5 Configurer les paramètres

Ouvrir l’éditeur interactif des paramètres :

```text
/settings
```

Afficher une valeur précise :

```text
/settings show model
```

Modifier un paramètre utilisateur :

```text
/settings model auto
```

Configurer un paramètre partagé au niveau du dépôt :

```text
/settings --repo model auto
```

Configurer un remplacement local non partagé :

```text
/settings --local model auto
```

Les principales portées sont :

| Portée | Fichier | Usage |
|---|---|---|
| Utilisateur | `~/.copilot/settings.json` | Valeurs par défaut pour tous les projets de la machine. |
| Dépôt | `.github/copilot/settings.json` | Configuration partagée et versionnée avec le projet. |
| Locale | `.github/copilot/settings.local.json` | Préférences personnelles propres au dépôt ; à ajouter dans `.gitignore`. |

Ordre de priorité simplifié : paramètres utilisateur, paramètres du dépôt, paramètres locaux, variables d’environnement, puis options de lancement.

## 2.6 Choisir le modèle

Dans la session :

```text
/model
```

Sélectionnez `auto` lorsque vous souhaitez laisser Copilot choisir le modèle adapté. Sélectionnez manuellement un modèle lorsqu’un besoin précis l’exige, par exemple une grande fenêtre de contexte ou un comportement particulier sur le code.

Au lancement :

```bash
copilot --model auto
```

Le choix exact des modèles dépend du plan, des politiques de l’organisation et de la version de Copilot CLI.

## 2.7 Configurer les permissions de manière prudente

Par défaut, Copilot demande une validation avant certaines actions. Pour une première utilisation, conservez ce fonctionnement.

Autoriser uniquement les tests npm pendant une session :

```bash
copilot --allow-tool='shell(npm test)'
```

Autoriser les modifications de fichiers, mais interdire `git push` :

```bash
copilot --allow-tool='write' --deny-tool='shell(git push)'
```

Autoriser presque tout sauf les commandes dangereuses :

```bash
copilot --allow-all-tools \
  --deny-tool='shell(rm)' \
  --deny-tool='shell(git push)'
```

N’utilisez `--allow-all`, `/allow-all` ou `/yolo` que dans un environnement isolé, versionné et sans secret de production.

## 2.8 Contrôler les chemins et les URL

Par défaut, Copilot accède au dossier de travail, à ses sous-dossiers et au dossier temporaire du système. Ajoutez explicitement un autre dossier uniquement lorsqu’il est nécessaire :

```bash
copilot --add-dir ../bibliotheque-partagee
```

Dans la session :

```text
/add-dir ../bibliotheque-partagee
/list-dirs
```

Les accès web externes peuvent nécessiter une validation. Évitez d’autoriser globalement des domaines ou URL lorsque seule une ressource précise est nécessaire.

## 2.9 Vérifier la configuration

Lancez cette séquence de contrôle :

```text
/version
/user show
/env
/instructions
/settings show model
```

Puis testez une demande en lecture seule :

```text
Donne-moi une vue d’ensemble de ce dépôt. Identifie les points d’entrée,
les commandes de test et les principaux dossiers. Ne modifie aucun fichier.
```

Enfin, utilisez le mode Plan pour une tâche plus structurée :

```text
/plan ajouter une validation du formulaire de connexion avec tests unitaires,
sans modifier le code pour le moment
```

## 2.10 Configuration minimale recommandée

Pour un premier projet, la configuration suivante est suffisante :

1. installer la version stable ;
2. exécuter `copilot --version` ;
3. lancer `copilot login` ;
4. ouvrir le dépôt avec `copilot -C CHEMIN_DU_DEPOT` ;
5. n’accorder la confiance permanente qu’aux dépôts maîtrisés ;
6. exécuter `/init` ;
7. conserver les validations manuelles des outils ;
8. exécuter `/plan` avant les changements importants ;
9. vérifier `/diff`, les tests et `/review` avant de créer une pull request.

---

# 3. Comprendre GitHub Copilot CLI

GitHub Copilot CLI est un agent conversationnel utilisable directement dans le terminal. Il peut notamment :

- analyser et modifier un dépôt Git ;
- lancer des commandes shell, des tests et des outils de qualité ;
- préparer ou gérer des pull requests ;
- déléguer des tâches à des agents ou sous-agents ;
- utiliser des skills, des plugins et des serveurs MCP ;
- conserver, reprendre, partager ou compacter des sessions ;
- travailler en mode standard, Plan ou Autopilot.

Pour ouvrir l’interface interactive :

```bash
copilot
```

Pour afficher l’aide générale depuis le terminal :

```bash
copilot help
```

Pour afficher les commandes dans une session interactive :

```text
/help
```

---

# 4. Initialisation et personnalisation

| Commande | Définition | Exemple |
|---|---|---|
| `/init` | Analyse le dépôt et initialise les instructions Copilot propres au projet. La commande peut créer ou mettre à jour `.github/copilot-instructions.md`. | `/init` |
| `/agent` | Affiche les agents personnalisés disponibles et permet d’en sélectionner un pour la suite de la session. | `/agent` puis sélectionner `security-auditor` |
| `/skills` | Gère les Agent Skills, c’est-à-dire des workflows spécialisés stockés autour d’un fichier `SKILL.md`. | `/skills list` |
| `/mcp` | Gère les serveurs MCP qui donnent à Copilot des outils supplémentaires : bases de données, navigateurs, API, services internes, etc. | `/mcp list` |
| `/plugin` | Gère les plugins Copilot CLI et les catalogues de plugins. La disponibilité dépend de la version installée. | `/plugin` puis rechercher un plugin de test |
| `/instructions` | Affiche les fichiers d’instructions chargés et permet d’activer ou désactiver certaines instructions. | `/instructions` |
| `/env` | Affiche les éléments chargés dans l’environnement : instructions, MCP, skills, agents, hooks, plugins, LSP et extensions. | `/env` |
| `/settings` | Ouvre ou modifie les paramètres de Copilot CLI. Les options peuvent être personnelles ou propres au dépôt. | `/settings` |

### Exemple : initialiser correctement un projet

```text
/init
```

Puis demander :

```text
Analyse le projet et vérifie que les instructions mentionnent les commandes de build,
de test, de lint, l’architecture principale et les conventions TypeScript.
```

---

# 5. Agents et sous-agents

| Commande | Définition | Exemple |
|---|---|---|
| `/model` | Sélectionne le modèle d’IA utilisé par Copilot CLI. Le choix `auto` laisse Copilot sélectionner automatiquement un modèle adapté. | `/model` puis choisir `auto` |
| `/delegate` | Envoie une tâche au Copilot coding agent distant. Copilot travaille sur GitHub et peut créer une pull request. | `/delegate complète les tests d’intégration de l’API et corrige les échecs` |
| `/fleet` | Décompose une tâche complexe en plusieurs sous-tâches exécutées en parallèle par des sous-agents. | `/fleet implémente l’authentification, les tests et la documentation` |
| `/autopilot` | Active ou désactive le mode Autopilot dans les versions qui exposent cette commande. L’agent poursuit le travail avec moins d’interruptions jusqu’à la fin de la tâche. | `/autopilot` |
| `/tasks` | Affiche et gère les tâches actives, notamment les sous-agents et commandes shell lancées en arrière-plan. | `/tasks` |
| `/subagents` | Configure les modèles utilisés par défaut ou par type de sous-agent. | `/subagents` |
| `/agents` | Alias ou variante de `/subagents` dans certaines versions ; peut aussi ouvrir la configuration des agents secondaires. | `/agents` |
| `/rubber-duck` | Demande un second avis à un agent de type « rubber duck » sur un plan, du code ou des tests. | `/rubber-duck vérifie si mon plan de migration oublie des risques` |

## Quand utiliser chaque mode ?

- Utilisez **`/delegate`** pour envoyer un travail dans un dépôt GitHub et obtenir une pull request.
- Utilisez **`/fleet`** lorsque plusieurs parties indépendantes peuvent être traitées en parallèle.
- Utilisez **Autopilot** lorsque la mission est claire et que l’agent doit coder, tester et corriger jusqu’à atteindre l’objectif.
- Utilisez **Plan** lorsque vous voulez d’abord une analyse sans modification du code.

### Exemple de délégation

```text
/delegate ajoute des tests pour tous les endpoints de paiement,
corrige les cas limites détectés et crée une pull request vers develop
```

### Exemple d’exécution parallèle

```text
/fleet réalise les tâches suivantes :
1. créer les endpoints utilisateurs ;
2. ajouter les tests unitaires ;
3. préparer la migration SQL ;
4. mettre à jour la documentation OpenAPI.
```

---

# 6. Travail sur le code et GitHub

| Commande | Définition | Exemple |
|---|---|---|
| `/ide` | Connecte la session CLI à un workspace d’IDE, notamment VS Code. | `/ide` |
| `/diff` | Affiche et permet de revoir les changements présents dans le répertoire courant. | `/diff` |
| `/pr` | Affiche l’état de la pull request liée à la branche actuelle. | `/pr` |
| `/pr view web` | Ouvre la pull request actuelle dans le navigateur. | `/pr view web` |
| `/pr create` | Crée une pull request ou met à jour celle qui existe déjà pour la branche actuelle. | `/pr create ajoute les notes de migration dans la description` |
| `/pr fix feedback` | Analyse les commentaires de revue et applique les corrections demandées. | `/pr fix feedback` |
| `/pr fix conflicts` | Synchronise la branche avec la branche de base et aide à résoudre les conflits. | `/pr fix conflicts` |
| `/pr fix ci` | Analyse les jobs CI en échec, corrige les causes identifiées et recontrôle les résultats. | `/pr fix ci concentre-toi sur les tests d’intégration` |
| `/pr fix` | Exécute successivement les corrections de feedback, de conflits et de CI. | `/pr fix` |
| `/pr auto` | Automatise le cycle complet de la pull request jusqu’à obtenir une situation stable : création, feedback, conflits et CI. | `/pr auto inclure un résumé des changements de sécurité` |
| `/review` | Lance l’agent de revue de code sur les changements courants. | `/review recherche les bugs, régressions et problèmes de performance` |
| `/security-review` | Analyse les changements indexés et non indexés afin de rechercher des vulnérabilités. Cette commande peut dépendre de la version ou d’un agent installé. | `/security-review vérifie les injections SQL, XSS et secrets exposés` |
| `/lsp` | Gère la configuration des serveurs de langage utilisés pour comprendre le code. | `/lsp` |
| `/terminal-setup` | Configure le terminal pour prendre correctement en charge la saisie multiligne avec `Shift+Enter`. | `/terminal-setup` |
| `/worktree` | Crée un nouveau Git worktree isolé et bascule dedans. Commande expérimentale. | `/worktree feature-authentication` |
| `/move` | Déplace les changements non commités dans un nouveau worktree et bascule dessus. Commande expérimentale. | `/move corriger le système de paiement` |

### Exemple : revue complète avant une pull request

```text
/diff
```

```text
/review compare les changements à main.
Recherche les bugs, les régressions, les erreurs de typage et les tests manquants.
```

```text
/security-review vérifie les entrées utilisateur, les autorisations,
les secrets, les dépendances et les appels réseau.
```

```text
/pr create ajoute une section Tests effectués et une section Risques connus
```

---

# 7. Permissions et accès

Ces commandes contrôlent ce que Copilot CLI peut lire, modifier ou exécuter. Elles doivent être utilisées avec prudence.

| Commande | Définition | Exemple |
|---|---|---|
| `/allow-all` | Autorise tous les outils, chemins et URL sans demander une validation individuelle. | `/allow-all on` |
| `/yolo` | Alias de permission élevée dans certaines versions. Son effet est proche de `/allow-all`. | `/yolo on` |
| `/add-dir` | Ajoute un dossier à la liste des emplacements accessibles par Copilot. | `/add-dir ../shared-library` |
| `/list-dirs` | Affiche tous les dossiers actuellement autorisés. | `/list-dirs` |
| `/cwd` | Affiche le répertoire de travail courant ou change de répertoire. | `/cwd ./backend` |
| `/cd` | Alias courant de `/cwd` pour changer de dossier. | `/cd packages/api` |
| `/reset-allowed-tools` | Réinitialise la liste des outils qui ont été autorisés. | `/reset-allowed-tools` |
| `/sandbox` | Active, désactive ou configure l’isolation système pour limiter l’accès aux fichiers et au réseau. Selon la version, cette fonction peut être expérimentale. | `/sandbox enable` |

## Recommandation de sécurité

Évitez `/allow-all` et `/yolo` dans un dépôt contenant :

- des secrets ou fichiers `.env` réels ;
- des données de production ;
- des commandes de déploiement ;
- des accès cloud ou bases de données ;
- des scripts capables de supprimer ou écraser des fichiers.

Préférez une autorisation ciblée :

```bash
copilot --allow-tool='shell(npm test)' --allow-tool='write'
```

Ou interdisez explicitement une commande sensible :

```bash
copilot --allow-all-tools --deny-tool='shell(rm)' --deny-tool='shell(git push)'
```

---

# 8. Gestion des sessions

| Commande | Définition | Exemple |
|---|---|---|
| `/resume` | Ouvre le sélecteur de sessions et permet de reprendre une session précédente. Un identifiant peut être fourni. | `/resume` |
| `/continue` | Alias permettant de reprendre une session, selon la version utilisée. | `/continue` |
| `/rename` | Renomme la session actuelle ou génère automatiquement un nom à partir de la conversation. | `/rename Migration API paiement` |
| `/session` | Affiche et gère les sessions lorsque cette commande est proposée par la version installée. | `/session` |
| `/context` | Affiche la consommation de la fenêtre de contexte et sa visualisation. | `/context` |
| `/usage` | Affiche les métriques de la session : modèles utilisés, tokens et statistiques. | `/usage` |
| `/compact` | Résume l’historique afin de réduire l’utilisation de la fenêtre de contexte. | `/compact concentre le résumé sur le module d’authentification` |
| `/share` | Partage ou exporte une session ou un rapport de recherche en Markdown, HTML, gist ou lien GitHub. | `/share file session ./rapport-session.md` |
| `/export` | Alias ou variante de `/share` pour exporter le contenu de la session. | `/export html session ./rapport.html` |
| `/remote` | Active ou désactive le contrôle distant depuis GitHub web ou l’application mobile, lorsque le compte y a accès. | `/remote` |
| `/copy` | Copie la dernière réponse de Copilot dans le presse-papiers. | `/copy` |
| `/rewind` | Revient au tour précédent et annule les modifications de fichiers suivies par l’outil. | `/rewind` |
| `/undo` | Alias de `/rewind`. | `/undo` |
| `/fork` | Crée une nouvelle session à partir de la session actuelle. Commande expérimentale. | `/fork version-sans-framework` |

### Exemple : compacter une longue session

```text
/compact conserve uniquement :
- les décisions techniques validées ;
- les fichiers modifiés ;
- les tests encore en échec ;
- les prochaines actions.
```

### Exemple : exporter le résultat

```text
/share file session ./documentation/session-copilot.md
```

---

# 9. Aide, diagnostic et interface

| Commande | Définition | Exemple |
|---|---|---|
| `/help` | Affiche l’aide des commandes interactives. | `/help` |
| `/changelog` | Affiche l’historique des versions de Copilot CLI. Le mot `summarize` demande un résumé généré par l’IA. | `/changelog summarize last 5` |
| `/release-notes` | Alias ou variante de `/changelog`. | `/release-notes summarize` |
| `/feedback` | Envoie un retour sur Copilot CLI. | `/feedback` |
| `/bug` | Alias permettant de signaler un problème dans certaines versions. | `/bug` |
| `/diagnose` | Analyse les journaux de la session et cherche la cause d’un comportement anormal. | `/diagnose pourquoi le serveur MCP ne se connecte pas` |
| `/theme` | Affiche ou modifie le thème visuel du terminal. | `/theme high-contrast` |
| `/statusline` | Configure les informations affichées dans la ligne de statut. | `/statusline` |
| `/footer` | Alias de configuration de la ligne d’état dans certaines versions. | `/footer` |
| `/update` | Met à jour Copilot CLI vers la dernière version disponible. | `/update` |
| `/upgrade` | Alias de `/update`. | `/upgrade` |
| `/version` | Affiche la version installée et vérifie les mises à jour. | `/version` |
| `/experimental` | Active, désactive ou affiche l’état des fonctionnalités expérimentales. | `/experimental on` |
| `/memory` | Affiche l’état de la mémoire ou permet de l’activer et la désactiver entre les sessions, si la fonction est disponible. | `/memory` |
| `/app` | Ouvre l’application GitHub Copilot ou affiche son lien d’installation. | `/app` |
| `/clikit` | Prévisualise certains composants internes de l’interface CLI. Principalement utile au diagnostic ou au développement. | `/clikit` |
| `/tuikit` | Prévisualise des composants et éléments du design system de l’interface terminal. | `/tuikit colors` |

---

# 10. Questions, recherche et planification

| Commande | Définition | Exemple |
|---|---|---|
| `/ask` | Pose une question rapide sans l’ajouter à l’historique principal de la conversation. | `/ask quelle est la différence entre rebase et merge ?` |
| `/plan` | Crée un plan d’implémentation avant de modifier le code. Le mode Plan doit rester principalement en lecture seule. | `/plan migrer cette API Express vers Fastify sans interruption de service` |
| `/refine` | Réécrit une demande imprécise sous forme de prompt plus clair et plus structuré. | Écrire un brouillon, puis lancer `/refine` |
| `/research` | Lance une recherche approfondie à partir du dépôt, de GitHub et de sources web disponibles. | `/research compare trois solutions d’authentification adaptées à ce projet` |
| `/search` | Recherche dans la chronologie de la conversation. Fonction souvent expérimentale. | `/search migration SQL` |
| `/find` | Alias de recherche dans la conversation dans certaines versions. | `/find erreur 401` |
| `/chronicle` | Analyse l’historique des sessions et produit des synthèses, conseils ou propositions d’amélioration. | `/chronicle standup` |

## Exemples `/chronicle`

```text
/chronicle standup
```

Produit une synthèse exploitable pour une réunion quotidienne.

```text
/chronicle tips
```

Propose des conseils à partir de votre manière d’utiliser Copilot CLI.

```text
/chronicle improve
```

Analyse les sessions afin d’identifier des améliorations de workflow ou de configuration.

---

# 11. Contrôle de la machine et de la session

| Commande | Définition | Exemple |
|---|---|---|
| `/keep-alive` | Empêche la machine de se mettre en veille pendant la session, pendant le travail de l’agent ou durant une période déterminée. | `/keep-alive 2h` |
| `/caffeinate` | Alias de `/keep-alive` dans certaines versions. | `/caffeinate busy` |
| `/limits` | Affiche ou modifie les limites de consommation appliquées à une réponse ou à une session. | `/limits` |
| `/limits set max-ai-credits 10` | Définit une limite souple de crédits IA par réponse. | `/limits set max-ai-credits 10` |
| `/limits unset all` | Supprime les limites configurées. | `/limits unset all` |
| `/restart` | Redémarre Copilot CLI en conservant la session actuelle. | `/restart` |
| `/clear` | Abandonne la conversation actuelle et démarre une nouvelle conversation. | `/clear` |
| `/new` | Alias permettant de commencer une nouvelle conversation. | `/new analyse maintenant le dossier backend` |
| `/reset` | Autre alias possible de création d’une nouvelle conversation. | `/reset` |
| `/exit` | Ferme Copilot CLI. | `/exit` |
| `/quit` | Alias de `/exit`. | `/quit` |

---

# 12. Compte GitHub et authentification

| Commande | Définition | Exemple |
|---|---|---|
| `/login` | Connecte l’utilisateur à GitHub Copilot. | `/login` |
| `/logout` | Déconnecte la session OAuth actuelle. La présence de cette commande dépend de la version. | `/logout` |
| `/user` | Affiche, liste ou change l’utilisateur GitHub actif. | `/user list` |
| `/user show` | Affiche le compte actuellement utilisé. | `/user show` |
| `/user switch` | Permet de basculer vers un autre compte configuré. | `/user switch` |

---

# 13. Commandes expérimentales et programmées

Certaines commandes nécessitent :

```text
/experimental on
```

ou le lancement de la CLI avec :

```bash
copilot --experimental
```

| Commande | Définition | Exemple |
|---|---|---|
| `/after` | Programme une instruction unique à exécuter plus tard dans la session. | `/after 30m rappelle-moi de vérifier les tests` |
| `/every` | Programme une instruction récurrente dans la session. | `/every 1h exécute les tests et résume les échecs` |
| `/fork` | Crée une nouvelle session dérivée de la session actuelle. | `/fork solution-alternative` |
| `/worktree` | Crée un worktree isolé à partir de `HEAD`. | `/worktree feature-checkout` |
| `/move` | Déplace les changements non commités dans un nouveau worktree. | `/move corriger la validation des formulaires` |
| `/search` | Recherche dans la chronologie de la conversation. | `/search décision architecture` |

> Les tâches programmées avec `/after` et `/every` sont liées à la session CLI. Elles ne remplacent pas nécessairement un ordonnanceur système comme cron ou GitHub Actions.

---

# 14. Entrée vocale

| Commande | Définition | Exemple |
|---|---|---|
| `/voice on` | Active le mode vocal lorsque cette fonction est disponible. | `/voice on` |
| `/voice off` | Désactive le mode vocal. | `/voice off` |
| `/voice models` | Affiche les modèles vocaux disponibles. | `/voice models` |
| `/voice devices` | Affiche ou sélectionne le microphone utilisé. | `/voice devices` |

---

# 15. Emplacements des instructions lus par Copilot CLI

Copilot CLI peut charger des instructions depuis plusieurs emplacements.

| Emplacement | Portée | Utilité |
|---|---|---|
| `CLAUDE.md` | Racine Git et répertoire courant | Réutilise des instructions de projet compatibles avec les conventions Claude. |
| `GEMINI.md` | Racine Git et répertoire courant | Réutilise des instructions de projet compatibles avec les conventions Gemini. |
| `AGENTS.md` | Racine Git et répertoire courant | Définit des règles générales pour les agents travaillant dans le dépôt. |
| `.github/copilot-instructions.md` | Dépôt | Fichier principal d’instructions GitHub Copilot du projet. |
| `.github/instructions/**/*.instructions.md` | Dépôt | Instructions spécialisées, généralement ciblées sur certains fichiers ou dossiers. |
| `$HOME/.copilot/copilot-instructions.md` | Utilisateur | Instructions personnelles chargées dans plusieurs projets. |
| `$HOME/.copilot/instructions/**/*.instructions.md` | Utilisateur | Bibliothèque personnelle d’instructions spécialisées. |
| `COPILOT_CUSTOM_INSTRUCTIONS_DIRS` | Variable d’environnement | Ajoute d’autres dossiers personnalisés contenant des instructions. |

## Exemple de `.github/copilot-instructions.md`

```markdown
# Instructions du projet

- Utiliser TypeScript en mode strict.
- Ne jamais modifier les migrations déjà déployées.
- Exécuter `npm run lint`, `npm test` et `npm run build` avant de terminer.
- Utiliser des tests Vitest avec la structure Arrange, Act, Assert.
- Ne jamais écrire de secret dans le code ou les logs.
```

## Exemple d’instruction spécialisée

Fichier :

```text
.github/instructions/tests.instructions.md
```

Contenu :

```markdown
---
applyTo: "**/*.test.ts"
---

- Couvrir les cas nominaux, erreurs et limites.
- Ne pas utiliser de délai artificiel dans les tests.
- Préférer les mocks explicites aux mocks globaux.
```

---

# 16. Raccourcis utiles dans l’interface interactive

| Raccourci | Fonction | Exemple |
|---|---|---|
| `@ fichier` | Ajoute le contenu d’un fichier au contexte. | `@ src/auth.ts explique cette classe` |
| `# numéro` | Ajoute une issue ou une pull request GitHub au contexte. | `#42 prépare un plan de correction` |
| `! commande` | Exécute directement une commande shell sans passer par l’agent. | `! git status` |
| `Shift+Enter` | Insère une nouvelle ligne dans le prompt. | Rédiger une mission en plusieurs lignes |
| `Shift+Tab` | Bascule entre les modes standard, Plan et Autopilot. | Passer en mode Plan avant une migration |
| `Ctrl+X` puis `/` | Lance une commande slash sans perdre le prompt déjà saisi. | Changer de modèle au milieu d’une demande |
| `Ctrl+X` puis `e` | Ouvre le prompt dans l’éditeur externe défini par `$EDITOR`. | Modifier un long prompt dans VS Code |
| `Ctrl+X` puis `b` | Envoie une tâche ou une commande en arrière-plan. | Continuer à utiliser la session pendant les tests |

---

# 17. Options courantes au lancement de la CLI

Les commandes slash sont utilisées **dans** l’interface interactive. Les options suivantes sont utilisées **au lancement**, dans le terminal.

| Option | Définition | Exemple |
|---|---|---|
| `copilot` | Lance l’interface interactive. | `copilot` |
| `copilot help` | Affiche l’aide générale. | `copilot help` |
| `-p`, `--prompt` | Exécute directement une demande sans entrer dans une longue session interactive. | `copilot -p "Explique ce projet"` |
| `--model` | Sélectionne le modèle à utiliser. | `copilot --model auto` |
| `--agent` | Sélectionne un agent personnalisé. | `copilot --agent security-auditor` |
| `--attachment` | Ajoute un fichier au prompt initial. | `copilot --attachment ./schema.png` |
| `-C` | Change de répertoire avant de démarrer. | `copilot -C ./backend` |
| `--continue` | Reprend la session récente. | `copilot --continue` |
| `--resume` | Reprend une session déterminée. | `copilot --resume <SESSION-ID>` |
| `--autopilot` | Lance la session avec la continuation Autopilot activée. | `copilot --autopilot` |
| `--allow-all` | Autorise tous les outils, chemins et URL. | `copilot --allow-all` |
| `--allow-tool` | Autorise seulement certains outils sans confirmation. | `copilot --allow-tool='shell(npm test)'` |
| `--deny-tool` | Interdit explicitement un outil ou une commande. | `copilot --deny-tool='shell(git push)'` |
| `--available-tools` | Limite les outils disponibles pour le modèle. | `copilot --available-tools='bash,read_file,write_file'` |
| `--sandbox` | Active l’isolation système pour la session. | `copilot --sandbox` |
| `--share` | Exporte la session programmée vers un fichier Markdown. | `copilot -p "Analyse le projet" --share=rapport.md` |
| `-w`, `--worktree` | Démarre la session dans un Git worktree isolé. | `copilot --worktree=feature-auth` |
| `-v`, `--version` | Affiche la version installée. | `copilot --version` |

---

# 18. Scénarios complets

## Scénario A — Comprendre un dépôt inconnu

```text
/init
```

```text
/plan analyse l’architecture du projet, les points d’entrée,
les dépendances, les commandes de build et les risques techniques.
Ne modifie aucun fichier.
```

```text
/share file session ./documentation/analyse-projet.md
```

## Scénario B — Corriger une fonctionnalité et créer une PR

```text
/plan corriger le calcul de TVA et ajouter les tests de non-régression
```

Après validation du plan :

```text
Implémente le plan, exécute les tests et le lint,
puis corrige les erreurs jusqu’à obtenir un résultat stable.
```

```text
/review concentre-toi sur les erreurs de calcul et les cas limites
```

```text
/pr create ajoute les résultats de tests dans la description
```

## Scénario C — Audit de sécurité

```text
/security-review analyse les changements actuels.
Recherche les injections, les failles d’autorisation,
les secrets exposés, les dépendances vulnérables et les logs sensibles.
Classe les résultats par criticité.
```

Puis :

```text
/review transforme chaque problème confirmé en action corrective précise
```

## Scénario D — Travail parallèle

```text
/plan ajouter un module de gestion des utilisateurs avec API, interface et tests
```

```text
/fleet exécute le plan en séparant :
- API et base de données ;
- interface utilisateur ;
- tests ;
- documentation.
```

```text
/tasks
```

## Scénario E — Reprendre une session interrompue

```text
/resume
```

```text
/context
```

```text
/compact conserve les décisions, les modifications et les tests encore en échec
```

---

# 19. Bonnes pratiques

1. Lancez `/init` au début d’un nouveau dépôt ou lorsque les instructions sont absentes.
2. Utilisez `/plan` avant une migration, une refonte ou une modification risquée.
3. Examinez `/diff` avant de valider les modifications.
4. Lancez `/review` et les tests avant `/pr create`.
5. Réservez `/fleet` aux tâches réellement parallélisables.
6. N’activez `/allow-all`, `/yolo` ou Autopilot que dans un environnement contrôlé.
7. Utilisez `/compact` lorsque la session devient longue ou perd en précision.
8. Utilisez `/env` pour comprendre pourquoi une instruction, une skill ou un MCP n’est pas chargé.
9. Utilisez `/diagnose` lorsque l’agent adopte un comportement inattendu.
10. Vérifiez régulièrement `/version`, `/update` et `/changelog`.

---

# 20. Sources officielles

- Installation : https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/install-copilot-cli
- Authentification : https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/authenticate-copilot-cli
- Configuration : https://docs.github.com/en/copilot/how-tos/copilot-cli/set-up-copilot-cli/configure-copilot-cli
- Démarrage rapide : https://docs.github.com/en/copilot/how-tos/copilot-cli/cli-getting-started
- Référence des commandes : https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-command-reference
- Répertoire et fichiers de configuration : https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference
- Utiliser GitHub Copilot CLI : https://docs.github.com/en/copilot/how-tos/copilot-cli
- Bonnes pratiques : https://docs.github.com/en/copilot/how-tos/copilot-cli/cli-best-practices
- Gestion des pull requests : https://docs.github.com/en/copilot/how-tos/copilot-cli/use-copilot-cli/manage-pull-requests

