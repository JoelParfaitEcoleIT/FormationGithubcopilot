# Checklist accessibilité et validité — TaskBoard

Sans JavaScript, il n'y a pas de tests automatisés classiques sur ce projet. À la place, on vérifie la **qualité du HTML et du CSS** eux-mêmes, avec l'aide de Copilot (voir Étape 5 du guide d'exercice).

- [ ] Chaque `<img>` (s'il y en a) a un attribut `alt` pertinent.
- [ ] Les titres sont dans l'ordre (`h1` puis `h2` puis `h3`, sans saut de niveau).
- [ ] Chaque champ de formulaire (`<input>`, `<select>`, `<textarea>`) a un `<label>` associé via `for`/`id`.
- [ ] Le contraste entre le texte et son fond est suffisant (notamment les badges de priorité).
- [ ] La navigation au clavier (Tab) permet d'atteindre tous les liens et boutons, avec un focus visible.
- [ ] Aucune couleur n'est le seul moyen de comprendre une information (les badges ont aussi un texte : « Haute », « Critique »...).
- [ ] Le HTML ne contient pas de balises non fermées ni d'attributs dupliqués.
