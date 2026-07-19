# Guide des commandes GitHub Copilot dans VS Code

Ce document regroupe les commandes et outils visibles dans les captures d’écran, ainsi que les outils de navigateur présentés précédemment.

> Remarque : la liste disponible dépend de la version de VS Code, de GitHub Copilot Chat, du mode utilisé — Ask, Agent, Plan ou Autopilot —, des extensions installées, des plugins, des serveurs MCP et des personnalisations du projet. Certains noms peuvent donc ne pas apparaître dans toutes les installations.

## 1. Comprendre les préfixes

| Préfixe | Signification | Exemple |
|---|---|---|
| `/` | Lance une commande rapide ou un prompt réutilisable dans le chat. | `/fix Corrige cette fonction` |
| `@` | Désigne un participant, un agent ou un groupe d’outils. | `@terminal explique cette erreur` |
| `#` | Ajoute explicitement un outil, une ressource ou un contexte au prompt. | `Analyse ce bug avec #browser` |

Dans l’interface montrée sur les captures, les outils apparaissent avec `@`. Dans la documentation récente de VS Code, ils sont aussi souvent référencés avec la syntaxe `#tool:` ou `#browser` dans les fichiers de prompt et d’agent.

---

# 2. Commandes générales du chat

| Commande | Définition | Exemple d’utilisation |
|---|---|---|
| `/compact` | Résume et compacte l’historique de la conversation afin de libérer de l’espace dans la fenêtre de contexte du modèle. Le chat continue avec un résumé de ce qui précède. | `/compact` |
| `/clear` | Démarre une nouvelle conversation et archive ou ferme la conversation actuelle selon la version de VS Code. | `/clear` |
| `/fork` | Crée une nouvelle conversation à partir de la conversation actuelle. La nouvelle branche conserve le contexte précédent, mais peut ensuite évoluer indépendamment. | `/fork` puis : `Explore maintenant une solution en Python` |
| `/rename` | Renomme la conversation actuelle pour la retrouver plus facilement dans l’historique. | `/rename Audit du formulaire de connexion` |
| `/debug` | Ouvre la vue de débogage du chat pour examiner les appels d’outils, les messages système, les erreurs et les journaux de l’agent. | `/debug` |
| `/troubleshoot` | Demande à Copilot d’analyser les journaux de l’agent afin d’expliquer un comportement inattendu, un outil non chargé ou une personnalisation ignorée. | `/troubleshoot Pourquoi le fichier SKILL.md n’a-t-il pas été chargé ?` |

---

# 3. Comprendre, corriger et générer du code

| Commande | Définition | Exemple d’utilisation |
|---|---|---|
| `/explain` | Explique un fichier, une sélection de code, une erreur ou un concept technique. | Sélectionner une fonction, puis écrire : `/explain Explique chaque étape simplement` |
| `/fix` | Analyse le code ou les erreurs détectées et propose une correction. En mode Agent, Copilot peut appliquer directement les modifications après approbation. | `/fix Corrige cette erreur TypeError sans modifier l’API publique` |
| `/tests` | Génère des tests pour la fonction, la classe, le fichier ou la sélection active. | Sélectionner `calculateTotal()`, puis écrire : `/tests Génère les cas nominaux, limites et erreurs` |
| `/setupTests` | Analyse le projet et aide à installer ou configurer un framework de test adapté. | `/setupTests Configure Vitest pour ce projet TypeScript` |
| `/new` | Crée ou prépare la structure d’un nouveau fichier, composant, module ou workspace à partir d’une description en langage naturel. | `/new Crée une API Node.js avec Express, TypeScript et une route /health` |
| `/newNotebook` | Génère un notebook Jupyter adapté au besoin décrit. | `/newNotebook Crée un notebook d’analyse exploratoire du fichier ventes.csv` |
| `/plan` | Lance un travail de recherche et produit un plan d’implémentation structuré avant de modifier le code. | `/plan Ajouter une authentification à double facteur à cette application` |
| `/search` | Transforme une demande en recherche dans la vue Search de VS Code. | `/search Trouve tous les appels à localStorage dans le projet` |
| `/get-search-view-results` | Récupère les résultats actuellement visibles dans la vue Search afin que Copilot puisse les analyser. | Lancer une recherche dans VS Code, puis : `/get-search-view-results Résume les fichiers concernés` |
| `/startDebugging` | Génère ou met à jour la configuration de débogage, généralement `launch.json`, puis aide à lancer la session de débogage. | `/startDebugging Configure le débogage de cette application Node.js` |

---

# 4. Initialisation et personnalisation de Copilot

| Commande | Définition | Exemple d’utilisation |
|---|---|---|
| `/init` | Analyse le projet et génère ou met à jour les instructions générales du workspace, par exemple `.github/copilot-instructions.md` ou `AGENTS.md`. | `/init` |
| `/instructions` | Ouvre l’interface permettant de consulter et configurer les instructions permanentes appliquées à Copilot. | `/instructions` |
| `/create-instruction` | Génère avec l’IA un fichier d’instructions ciblé, généralement `*.instructions.md`. | `/create-instruction Crée des règles pour tous les fichiers TypeScript du dossier src` |
| `/create-instructions` | Variante affichée dans certaines versions ou personnalisations. Elle sert également à créer un fichier d’instructions. | `/create-instructions Impose ESLint, Prettier et les imports nommés` |
| `/prompts` | Ouvre la gestion des fichiers de prompt réutilisables, généralement stockés dans `.github/prompts`. | `/prompts` |
| `/create-prompt` | Crée un fichier `*.prompt.md` réutilisable, qui apparaîtra ensuite comme une commande `/nom-du-prompt`. | `/create-prompt Crée un prompt de revue de sécurité d’une API REST` |
| `/skills` | Ouvre la configuration des Agent Skills. Une skill regroupe des instructions, scripts, modèles et ressources pour un workflow spécialisé. | `/skills` |
| `/create-skill` | Crée une nouvelle skill avec un fichier principal `SKILL.md` et, si nécessaire, des ressources supplémentaires. | `/create-skill Crée une skill qui audite un formulaire web et rédige un rapport QA` |
| `/agents` | Ouvre la gestion des agents personnalisés définis dans des fichiers `*.agent.md`. | `/agents` |
| `/create-agent` | Crée un agent spécialisé avec son rôle, ses instructions, son modèle et ses outils autorisés. | `/create-agent Crée un agent QA qui ne modifie jamais le code et produit uniquement des anomalies` |
| `/hooks` | Ouvre la configuration des hooks, c’est-à-dire des scripts exécutés automatiquement à certains moments du cycle de l’agent. | `/hooks` |
| `/create-hook` | Génère un fichier de hook permettant d’automatiser ou de bloquer certaines actions. | `/create-hook Exécute ESLint après chaque modification de fichier JavaScript` |
| `/models` | Ouvre le sélecteur de modèles afin de choisir le modèle utilisé par le chat ou l’agent. | `/models` puis sélectionner le modèle souhaité |
| `/plugins` | Ouvre la gestion des plugins disponibles pour l’agent. Un plugin peut fournir des agents, skills, instructions, prompts, hooks ou outils supplémentaires. | `/plugins` |
| `/tools` | Ouvre la liste des outils disponibles pour le chat ou l’agent et permet de les activer ou désactiver. | `/tools` puis activer les outils Browser et Terminal |

---

# 5. Permissions et autonomie de l’agent

Ces commandes modifient le niveau d’approbation des actions exécutées par Copilot. Elles doivent être utilisées avec prudence, surtout dans un projet contenant des données réelles, des clés, des commandes système ou des opérations de déploiement.

| Commande | Définition | Exemple d’utilisation |
|---|---|---|
| `/autoApprove` | Active l’approbation automatique ou le mode de contournement des validations pour les appels d’outils, selon la version et la politique de l’organisation. | `/autoApprove` puis demander : `Lance les tests et corrige les erreurs` |
| `/disableAutoApprove` | Désactive l’approbation automatique et rétablit le comportement normal de confirmation. | `/disableAutoApprove` |
| `/yolo` | Alias historique ou alternatif pour autoriser l’agent à contourner les approbations. Son effet peut être similaire à `/autoApprove`. | `/yolo` |
| `/disableYolo` | Désactive le mode `/yolo` et rétablit les permissions par défaut. | `/disableYolo` |
| `/autopilot` | Active le mode Autopilot. L’agent peut poursuivre plus longtemps son workflow, utiliser des outils, corriger et retester avec moins d’interruptions. | `/autopilot` puis : `Implémente la fonctionnalité, exécute les tests et corrige jusqu’à réussite` |
| `/exitAutopilot` | Quitte le mode Autopilot et rétablit le niveau de permissions par défaut. | `/exitAutopilot` |

## Différence pratique

- **Default approvals** : Copilot demande une validation pour certaines actions.
- **Bypass approvals / autoApprove / yolo** : Copilot exécute les outils sans demander chaque confirmation.
- **Autopilot** : Copilot travaille de manière plus continue et autonome sur une tâche complète.

---

# 6. Participants et combinaisons visibles

| Participant ou combinaison | Définition | Exemple |
|---|---|---|
| `@terminal` | Participant spécialisé dans le terminal, les commandes shell et leurs résultats. | `@terminal explique pourquoi npm run build échoue` |
| `@terminal /explain` | Demande au participant Terminal d’expliquer une commande, sa sortie ou une erreur. | `@terminal /explain npm ERR! code ERESOLVE` |
| `@vscode` | Participant spécialisé dans les fonctions, paramètres, commandes et API de VS Code. | `@vscode Comment activer le retour automatique à la ligne ?` |
| `@vscode /search` | Utilise le participant VS Code pour préparer ou piloter une recherche dans le workspace. | `@vscode /search Trouve les fichiers qui utilisent axios` |
| `@agent` | Groupe d’outils permettant de déléguer une tâche à un agent ou à un sous-agent dans un contexte séparé. | `Utilise @agent pour déléguer la revue de sécurité à un agent spécialisé` |
| `@askQuestions` | Permet à l’agent d’afficher des questions structurées : texte libre, choix unique ou choix multiples. | `Utilise @askQuestions pour me demander le framework, la base de données et la méthode d’authentification` |

---

# 7. Outils Browser visibles dans les captures

Les outils Browser permettent à l’agent de piloter un navigateur intégré afin de tester une application web comme le ferait un utilisateur. Copilot peut ouvrir une page, cliquer, remplir un formulaire, consulter la console, observer les requêtes réseau et vérifier le résultat.

## 7.1 Outils généraux et navigation

| Outil | Définition | Exemple de demande à Copilot |
|---|---|---|
| `@browser` | Groupe regroupant les outils de navigation et d’interaction avec le navigateur intégré. | `Utilise @browser pour tester le formulaire de connexion sur http://localhost:3000` |
| `@browser_navigate` | Ouvre une URL dans l’onglet actif. | `Ouvre http://localhost:3000/login` |
| `@browser_navigate_back` | Revient à la page précédente dans l’historique de navigation. | `Retourne à la page précédente et vérifie que les filtres sont conservés` |
| `@browser_close` | Ferme la page, l’onglet ou la session de navigateur utilisée par l’agent. | `Ferme l’onglet de test après la vérification` |
| `@browser_tabs` | Liste, crée, sélectionne ou ferme les onglets selon les actions supportées par la version installée. | `Liste les onglets puis active celui qui contient l’application locale` |
| `@browser_resize` | Modifie la taille de la fenêtre ou du viewport afin de tester un affichage responsive. | `Redimensionne la page en 390 × 844 et vérifie la version mobile` |
| `@browser_snapshot` | Produit une représentation structurée de la page : textes, boutons, champs, liens et rôles accessibles. | `Prends un snapshot et identifie tous les champs obligatoires` |
| `@browser_find` | Recherche un texte ou un élément dans la page active. | `Trouve le bouton intitulé Enregistrer` |

## 7.2 Clics, mouvements et interactions

| Outil | Définition | Exemple de demande à Copilot |
|---|---|---|
| `@browser_click` | Clique sur un élément identifié dans la page. | `Clique sur le bouton Se connecter` |
| `@browser_hover` | Place le pointeur sur un élément pour afficher un menu, une infobulle ou un état de survol. | `Survole l’icône utilisateur et vérifie que le menu apparaît` |
| `@browser_drag` | Démarre ou exécute une opération de glisser-déposer à partir d’un élément. | `Fais glisser la carte Tâche 1 vers la colonne Terminé` |
| `@browser_drop` | Dépose l’élément déplacé sur une cible. | `Dépose le fichier dans la zone Importer` |
| `@browser_press_key` | Simule l’appui sur une touche du clavier. | `Appuie sur Enter pour soumettre le formulaire` |
| `@browser_select_option` | Sélectionne une option dans une liste déroulante HTML. | `Choisis Belgique dans le champ Pays` |
| `@browser_handle_dialog` | Accepte, refuse ou complète une boîte de dialogue JavaScript de type `alert`, `confirm` ou `prompt`. | `Accepte la fenêtre de confirmation de suppression` |

## 7.3 Formulaires et fichiers

| Outil | Définition | Exemple de demande à Copilot |
|---|---|---|
| `@browser_fill_form` | Remplit plusieurs champs d’un formulaire en une seule opération. | `Remplis Nom avec Dupont, Email avec test@example.com et Pays avec Belgique` |
| `@browser_file_upload` | Sélectionne un fichier local pour un champ de téléversement. | `Téléverse fixtures/avatar-test.png dans le champ Photo` |

## 7.4 Diagnostic et observation technique

| Outil | Définition | Exemple de demande à Copilot |
|---|---|---|
| `@browser_console_messages` | Récupère les messages de la console : erreurs JavaScript, avertissements et logs. | `Affiche les erreurs de console apparues après l’envoi du formulaire` |
| `@browser_network_requests` | Liste les requêtes réseau exécutées par la page : API, scripts, images, CSS et autres ressources. | `Liste les requêtes réseau et repère celles qui retournent 400 ou 500` |
| `@browser_network_request` | Consulte le détail d’une requête réseau précise : URL, méthode, statut, en-têtes et parfois corps de requête ou réponse. | `Ouvre le détail de la requête POST /api/login` |
| `@browser_evaluate` | Exécute une expression JavaScript dans le contexte de la page pour lire ou manipuler l’état du navigateur. | `Évalue document.title et retourne le titre de la page` |
| `@browser_run_code_unsafe` | Exécute un bloc de code de navigateur plus libre et plus puissant. Il est qualifié d’unsafe car il peut contourner les interactions normales et modifier l’état de la page. | `Exécute un script qui récupère les valeurs de tous les champs visibles` |

---

# 8. Outils Browser mentionnés dans la liste précédente

Ces outils peuvent apparaître avec Playwright, un serveur MCP Browser ou une autre version des outils de navigateur. Leur présence exacte dépend de la configuration installée.

| Outil | Définition | Exemple de demande à Copilot |
|---|---|---|
| `@browser_generate_locator` | Génère un sélecteur Playwright stable pour retrouver un élément dans un test automatisé. | `Génère le locator Playwright du bouton Créer un compte` |
| `@browser_keyboard` | Exécute une séquence d’actions clavier plus avancée qu’un simple appui de touche. | `Utilise le clavier pour faire Tab, Tab, Enter` |
| `@browser_mouse_click` | Clique à une position précise de l’écran lorsque l’élément ne peut pas être identifié proprement. | `Clique aux coordonnées x=420, y=310` |
| `@browser_mouse_drag` | Effectue un glisser-déposer fondé sur des coordonnées. | `Fais glisser de x=200,y=300 vers x=700,y=300` |
| `@browser_mouse_move` | Déplace le curseur vers une position précise. | `Déplace la souris vers le graphique à x=600,y=250` |
| `@browser_mousewheel` | Fait défiler la page avec la molette. | `Fais défiler de 700 pixels vers le bas` |
| `@browser_open` | Ouvre le navigateur intégré ou une nouvelle page de navigation. | `Ouvre le navigateur sur http://localhost:5173` |
| `@browser_screenshot` | Prend une capture d’écran de la page ou d’une zone visible. | `Prends une capture de la page après l’erreur` |
| `@browser_type` | Saisit un texte dans un champ ciblé. | `Saisis test@example.com dans le champ Email` |
| `@browser_verify_element_visible` | Vérifie qu’un élément attendu est visible. | `Vérifie que le bouton Confirmer est visible` |
| `@browser_verify_list_visible` | Vérifie qu’une liste ou que ses éléments sont affichés. | `Vérifie que les trois produits apparaissent dans la liste` |
| `@browser_verify_text_visible` | Vérifie qu’un texte attendu est visible sur la page. | `Vérifie que le message Identifiants incorrects est affiché` |
| `@browser_verify_value` | Vérifie la valeur actuelle d’un champ ou d’un composant. | `Vérifie que le champ Pays contient Belgique` |

---

# 9. Commandes personnalisées ou tronquées visibles dans les captures

Les deux commandes suivantes semblent provenir d’un prompt, d’une skill, d’un plugin ou d’une personnalisation installée dans le workspace. Leur nom complet est tronqué dans la capture.

| Commande visible | Interprétation probable | Exemple |
|---|---|---|
| `/source-command-ll…` | Commande personnalisée destinée à aider à créer ou maintenir une instruction, une personnalité ou un contexte persistant. Il faut survoler la commande ou ouvrir `/prompts` ou `/skills` pour lire son nom complet et son fichier source. | `/source-command-ll… Crée une personnalité persistante de reviewer sécurité` |
| `/project-setup-info…` | Commande ou prompt de configuration de projet. Elle semble fournir des étapes de démarrage complètes pour créer ou configurer un projet. | `/project-setup-info… Configure une application React avec TypeScript et Vitest` |

La fonction intégrée correspondante peut également apparaître comme outil `vscode/getProjectSetupInfo` selon la version de VS Code.

---

# 10. Exemples de scénarios complets

## Exemple A — Comprendre et corriger une erreur

```text
/explain Explique l’erreur actuellement sélectionnée, sa cause et son impact.
```

Puis :

```text
/fix Corrige le problème sans modifier la signature publique de la fonction.
```

Enfin :

```text
/tests Ajoute les tests de non-régression correspondants.
```

## Exemple B — Préparer une nouvelle fonctionnalité

```text
/plan Ajouter un système de réinitialisation de mot de passe avec un lien valable 15 minutes.
```

Après validation du plan :

```text
Implémente le plan, exécute les tests et corrige les erreurs restantes.
```

## Exemple C — Tester une application web

```text
Utilise les outils Browser pour ouvrir http://localhost:3000/login.
Vérifie que les champs Email et Mot de passe sont visibles.
Soumets le formulaire vide et vérifie les messages obligatoires.
Saisis ensuite un mauvais mot de passe.
Vérifie la réponse réseau de POST /api/login, les erreurs de console et le message affiché à l’utilisateur.
Prends une capture d’écran du résultat final.
```

L’agent peut alors enchaîner des outils tels que :

```text
@browser_navigate
@browser_snapshot
@browser_fill_form
@browser_click
@browser_console_messages
@browser_network_requests
@browser_network_request
@browser_screenshot
```

## Exemple D — Créer un agent spécialisé

```text
/create-agent Crée un agent nommé QA-Analyste.
Il doit analyser les exigences, détecter les ambiguïtés, produire des scénarios de test,
ne jamais modifier le code et utiliser le navigateur uniquement pour vérifier le comportement observé.
```

## Exemple E — Créer une skill réutilisable

```text
/create-skill Crée une skill d’audit de formulaire web comprenant :
- contrôle des champs obligatoires ;
- tests de valeurs valides, invalides et limites ;
- contrôle des messages d’erreur ;
- vérification des requêtes réseau ;
- production d’un rapport Markdown.
```

---

# 11. Recommandations de sécurité

1. Utiliser `/plan` avant une modification importante ou multi-fichiers.
2. Garder les approbations par défaut pour les projets de production.
3. Éviter `/yolo`, `/autoApprove` et `/autopilot` lorsque le projet peut supprimer des données, exécuter des migrations ou publier en production.
4. Vérifier les commandes terminal proposées par l’agent avant exécution.
5. Ne jamais fournir de mot de passe, jeton d’API ou clé privée dans le chat.
6. Utiliser des comptes et données de test pour les scénarios Browser.
7. Préférer `@browser_click`, les locators et les snapshots aux clics par coordonnées, qui sont moins stables.
8. Utiliser `@browser_run_code_unsafe` uniquement lorsqu’une interaction normale est insuffisante et que le script est compris.

---

# 12. Sources officielles utiles

- [AI features in VS Code — Cheat Sheet](https://code.visualstudio.com/docs/agents/reference/ai-features-cheat-sheet)
- [Customize agent behavior in VS Code](https://code.visualstudio.com/docs/agent-customization/overview)
- [Use prompt files in VS Code](https://code.visualstudio.com/docs/agent-customization/prompt-files)
- [Use Agent Skills in VS Code](https://code.visualstudio.com/docs/agent-customization/agent-skills)
- [Custom agents in VS Code](https://code.visualstudio.com/docs/agent-customization/custom-agents)
- [Agent hooks in VS Code](https://code.visualstudio.com/docs/agent-customization/hooks)

