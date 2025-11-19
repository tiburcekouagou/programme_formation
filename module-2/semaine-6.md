## Semaine 6 : JavaScript dans le Navigateur - Le DOM

### J1 (Lundi) : Parler au Navigateur - Sélectionner des Éléments du DOM

**Objectif(s) du Jour :**
- Comprendre ce qu'est le DOM (Document Object Model).
- Utiliser l'objet global `document`.
- Sélectionner un élément unique avec `querySelector` et `getElementById`.
- Sélectionner plusieurs éléments avec `querySelectorAll`.
- Inspecter les éléments sélectionnés dans la console.

**Notion Clé : Le Plan de la Maison**
Imaginez votre page HTML comme une maison. Le **DOM** (Document Object Model) est le plan détaillé de cette maison, mais sous forme d'un objet JavaScript interactif. Chaque balise HTML (`<p>`, `<div>`, `<h1>`...) est une "pièce" sur ce plan. JavaScript peut lire ce plan pour savoir où se trouve chaque pièce, et plus important encore, il peut le **modifier** en temps réel : repeindre une pièce, ajouter des meubles, ou même détruire un mur. L'objet `document` est le point d'entrée, c'est la porte d'entrée de la maison.

---

#### Leçon

##### 1. L'Objet `document`
C'est un objet global, toujours disponible en JavaScript dans un navigateur. Il représente l'ensemble de votre page HTML. Tapez `console.log(document);` dans votre script pour le voir !

##### 2. Sélectionner un Élément Unique
- `document.querySelector(sélecteurCSS)` : La méthode la plus moderne et la plus polyvalente. Elle prend en argument n'importe quel sélecteur CSS (comme ceux que vous avez appris en Semaine 2) et renvoie le **premier** élément qui correspond.
- `document.getElementById(id)` : Une méthode plus ancienne mais très rapide, qui sélectionne l'élément unique ayant l'ID spécifié.

```html
<h1 id="main-title" class="title">Mon Titre</h1>
```
```javascript
// Méthode moderne (recommandée)
const monTitre = document.querySelector('#main-title');
// On peut aussi utiliser la classe, mais ça prendra le premier '.title' qu'il trouve
const titreParClasse = document.querySelector('.title'); 

// Méthode par ID
const monTitreParId = document.getElementById('main-title');

console.log(monTitre); // Affiche l'objet élément <h1> dans la console
```

##### 3. Sélectionner Plusieurs Éléments
- `document.querySelectorAll(sélecteurCSS)` : Similaire à `querySelector`, mais renvoie **tous** les éléments qui correspondent, sous forme d'une `NodeList` (qui ressemble beaucoup à un tableau).

```html
<ul>
  <li class="task">Tâche 1</li>
  <li class="task">Tâche 2</li>
  <li class="task">Tâche 3</li>
</ul>
```
```javascript
const toutesLesTaches = document.querySelectorAll('.task');

console.log(toutesLesTaches); // Affiche une NodeList avec les 3 <li>
console.log(toutesLesTaches.length); // Affiche 3
console.log(toutesLesTaches[1]); // Affiche le deuxième <li>
```

---

#### Mise en Pratique

1.  Créez un nouveau projet pour la semaine : un dossier avec `index.html`, `style.css` et `script.js`.
2.  Dans `index.html`, créez une structure de base pour une To-Do List : un `<h1>`, un `<form>` avec un `<input>` et un `<button>`, et une `<ul>` vide.
3.  Donnez des ID ou des classes pertinents à ces éléments (ex: `id="todo-form"`, `id="todo-input"`, `id="todo-list"`).
4.  Dans votre `script.js`, utilisez `querySelector` pour sélectionner le formulaire, l'input, le bouton et la liste `<ul>`.
5.  Stockez chaque élément sélectionné dans une constante (ex: `const form = ...`).
6.  Utilisez `console.log()` pour afficher chaque constante dans la console et vérifier que vos sélections ont bien fonctionné.

#### Mini-Exercice du Jour

Dans votre HTML, ajoutez trois paragraphes `<p>`. Donnez une classe `.highlight` à deux d'entre eux. En JavaScript, utilisez `querySelectorAll` pour sélectionner uniquement les paragraphes avec la classe `.highlight` et affichez la `NodeList` dans la console.

#### Synthèse

Vous avez établi le pont entre votre code JavaScript et votre page HTML. Vous savez maintenant "attraper" n'importe quel élément de votre page pour le manipuler. C'est la première étape indispensable de toute interaction. Demain, nous verrons quoi faire avec ces éléments une fois qu'on les a attrapés.

---

### J2 (Mardi) : Modifier le DOM - Contenu et Styles

**Objectif(s) du Jour :**
- Modifier le contenu textuel d'un élément avec `.textContent`.
- Modifier le contenu HTML d'un élément avec `.innerHTML`.
- Modifier les styles CSS d'un élément via la propriété `.style`.
- Ajouter, supprimer et vérifier la présence de classes CSS avec `.classList`.

**Notion Clé : Le Levier de Commande**
Maintenant que vous avez le "plan de la maison" (le DOM) et que vous savez sélectionner une "pièce" (un élément), vous pouvez utiliser les leviers de commande pour la modifier.
- `.textContent` est le levier "changer le texte affiché".
- `.innerHTML` est le levier "changer tout le contenu, y compris les balises HTML". (Plus puissant, mais à utiliser avec prudence).
- `.style` est un accès direct au panneau de contrôle des styles CSS de l'élément.
- `.classList` est le gestionnaire de classes, bien plus propre que de modifier le style directement.

---

#### Leçon

##### 1. Modifier le Contenu
- `.textContent` : Modifie uniquement le texte. C'est la méthode la plus sûre.
- `.innerHTML` : Interprète la chaîne de caractères comme du HTML. Utile, mais peut présenter des failles de sécurité si on y insère du contenu venant d'un utilisateur non fiable.

```javascript
const titre = document.querySelector('h1');
titre.textContent = "Ma Super To-Do List !"; // Modifie le texte
// titre.innerHTML = "<em>Ma Super</em> To-Do List !"; // Modifie le HTML
```

##### 2. Modifier les Styles directement
La propriété `.style` permet d'accéder aux styles "en ligne" de l'élément. Les propriétés CSS sont écrites en `camelCase` (ex: `background-color` devient `backgroundColor`).

```javascript
const titre = document.querySelector('h1');
titre.style.color = "blue";
titre.style.backgroundColor = "yellow";
```
**Inconvénient :** Cela mélange la logique de style dans le JS. C'est bien pour des changements dynamiques rapides, mais moins bien pour des états définis.

##### 3. Modifier les Styles via les Classes (La Bonne Pratique)
La meilleure façon de gérer les changements de style est de prédéfinir des classes dans votre CSS, et d'utiliser JavaScript pour les ajouter ou les enlever.
- `.classList.add('ma-classe')`
- `.classList.remove('ma-classe')`
- `.classList.toggle('ma-classe')` (ajoute la classe si elle n'y est pas, l'enlève si elle y est).

```css
/* Dans style.css */
.error-text {
  color: red;
  font-weight: bold;
}
```
```javascript
const message = document.querySelector('#error-message');
message.classList.add('error-text');
```

---

#### Mise en Pratique

1.  Dans votre projet To-Do List, utilisez `.textContent` pour changer le texte de votre `<h1>` via JavaScript.
2.  Créez un paragraphe `<p id="message-aide">` sous votre formulaire. Par défaut, il est vide. En JS, sélectionnez-le et changez son `.textContent` pour "Veuillez entrer une tâche à faire.".
3.  Dans votre CSS, créez une classe `.success` qui met le texte en vert.
4.  En JS, ajoutez cette classe `.success` à votre paragraphe de message d'aide en utilisant `.classList.add()`.

#### Mini-Exercice du Jour

Créez un `<div>` avec un `id="box"`. En CSS, donnez-lui une largeur, une hauteur et une couleur de fond. En JavaScript, sélectionnez cette boîte et modifiez ses styles pour lui donner une bordure rouge (`border`), un rayon de bordure (`borderRadius`) de 10px, et une ombre portée (`boxShadow`).

#### Synthèse

Vous pouvez maintenant modifier dynamiquement n'importe quel aspect visuel ou textuel de votre page. La combinaison de `.classList` (JS) et de classes pré-définies (CSS) est une technique professionnelle que vous utiliserez constamment. Demain, on passe à la vitesse supérieure : faire réagir la page aux actions de l'utilisateur.

---

### J3 (Mercredi) : Écouter l'Utilisateur - La Gestion des Événements

**Objectif(s) du Jour :**
- Comprendre le concept d'événement (click, submit, mouseover...).
- Utiliser `addEventListener()` pour déclencher une fonction en réponse à un événement.
- Comprendre le rôle de la fonction de callback dans la gestion d'événements.
- Empêcher le comportement par défaut d'un événement avec `event.preventDefault()`.

**Notion Clé : L'Interrupteur**
Un événement, c'est comme un interrupteur. La page web attend. L'utilisateur fait une action (l'**événement**, ex: appuyer sur l'interrupteur). Cette action déclenche un mécanisme (la **fonction de callback**) qui produit un résultat (la lumière s'allume). `addEventListener` est la méthode qui permet de "brancher" votre fonction au bon interrupteur.

---

#### Leçon

##### 1. `addEventListener()`
C'est la méthode principale pour écouter les événements. Elle prend (au minimum) deux arguments :
1.  Le **nom de l'événement** en chaîne de caractères (ex: `'click'`, `'submit'`).
2.  La **fonction de callback** à exécuter lorsque l'événement se produit.

```javascript
element.addEventListener('typeEvenement', function() {
  // Le code à exécuter
});
```

##### 2. L'Événement `click`
Le plus simple et le plus courant.

```html
<button id="mon-bouton">Clique-moi !</button>
```
```javascript
const bouton = document.querySelector('#mon-bouton');

bouton.addEventListener('click', function() {
  console.log("Le bouton a été cliqué !");
  alert("Clic !");
});
```

##### 3. L'Événement `submit` et `event.preventDefault()`
Quand on soumet un formulaire, le comportement par défaut du navigateur est de **recharger la page**. C'est un problème pour nos applications interactives. On veut gérer la soumission avec JavaScript sans rechargement.
La fonction de callback d'un `addEventListener` reçoit automatiquement un paramètre, souvent nommé `event` (ou `e`), qui est un objet décrivant l'événement. Cet objet a une méthode très utile : `.preventDefault()`.

```javascript
const form = document.querySelector('#todo-form');

form.addEventListener('submit', function(event) {
  // 1. On empêche le rechargement de la page
  event.preventDefault(); 
  
  // 2. On peut maintenant exécuter notre propre logique
  console.log("Le formulaire a été soumis sans recharger !");
});
```

---

#### Mise en Pratique

Dans votre projet To-Do List :
1.  Sélectionnez votre formulaire (`#todo-form`).
2.  Ajoutez un `addEventListener` pour l'événement `'submit'`.
3.  Dans la fonction de callback, commencez par appeler `event.preventDefault()`.
4.  Ensuite, sélectionnez la valeur actuelle de votre champ input (`input.value`) et affichez-la dans la console avec `console.log()`.
5.  Testez : tapez quelque chose dans le champ, appuyez sur "Entrée" ou cliquez sur le bouton. La page ne doit pas se recharger, et le texte que vous avez tapé doit apparaître dans la console.

#### Mini-Exercice du Jour

Créez un `<div>` carré et un bouton. Écrivez un script qui, à chaque clic sur le bouton, change la couleur de fond du `<div>` en une couleur aléatoire. (Indice : vous pouvez créer un tableau de couleurs et en choisir une au hasard à chaque clic).

#### Synthèse

Vos pages ne sont plus seulement dynamiques, elles sont devenues **interactives**. Vous savez maintenant écouter et réagir aux actions de l'utilisateur, ce qui est le cœur de toute application web. Demain, nous allons utiliser cette compétence pour la tâche la plus puissante : créer de nouveaux éléments HTML à la volée.

---

### J4 (Jeudi) : Créer et Supprimer des Éléments du DOM

**Objectif(s) du Jour :**
- Créer un nouvel élément HTML en mémoire avec `document.createElement()`.
- Ajouter cet élément à la page avec `.appendChild()`.
- Supprimer un élément existant avec `.remove()`.
- Assembler ces techniques pour ajouter dynamiquement du contenu.

**Notion Clé : La Construction à la Volée**
Jusqu'à présent, vous modifiiez des éléments qui existaient déjà dans votre fichier HTML. Le vrai pouvoir de JavaScript est de pouvoir construire de nouveaux éléments à partir de rien, comme un maçon qui ajoute des briques à un mur, puis de les placer où vous voulez dans la page. C'est ce qui permet de créer des listes qui grandissent, des commentaires qui apparaissent, etc.

---

#### Leçon

##### 1. Le Processus de Création
C'est toujours un processus en 3 étapes :
1.  **Créer :** On crée l'élément en mémoire. Il n'est visible nulle part.
2.  **Configurer :** On lui donne du contenu, des classes, des attributs...
3.  **Ajouter :** On l'attache à un élément parent déjà présent dans le DOM pour le rendre visible.

##### 2. Les Méthodes
- `document.createElement('nomDeLaBalise')` : Crée l'élément.
- `.appendChild(elementEnfant)` : Ajoute un élément enfant à la fin d'un élément parent.

- **Exemple de Code :**
  ```javascript
  // 1. Sélectionner le parent où on va ajouter l'élément
  const liste = document.querySelector('ul');
  
  // 2. Créer le nouvel élément en mémoire
  const nouvelItem = document.createElement('li');
  
  // 3. Le configurer
  nouvelItem.textContent = "Nouvelle Tâche";
  nouvelItem.classList.add('task');

  // 4. L'ajouter à la page
  liste.appendChild(nouvelItem);
  ```

##### 3. Supprimer un Élément
La méthode `.remove()` est très simple. On la lance sur l'élément que l'on veut supprimer.

```javascript
const elementASupprimer = document.querySelector('#element-genant');
elementASupprimer.remove();
```

---

#### Mise en Pratique

Dans le `addEventListener` de votre formulaire de To-Do List :
1.  Après avoir récupéré la valeur de l'input, vérifiez qu'elle n'est pas vide.
2.  Si elle n'est pas vide, utilisez `document.createElement('li')` pour créer un nouvel item de liste.
3.  Assignez la valeur de l'input au `.textContent` de ce nouvel item.
4.  Utilisez `.appendChild()` pour ajouter ce nouvel `<li>` à votre `<ul>` (`#todo-list`).
5.  (Bonus) Une fois la tâche ajoutée, videz le champ input en faisant `input.value = "";`.

#### Mini-Exercice du Jour

Créez un `<div>` vide avec un `id="container"` et un bouton. À chaque clic sur le bouton, créez un nouveau `div` avec la classe `.box`, donnez-lui une couleur de fond aléatoire et ajoutez-le au `div` container.

#### Synthèse

Vous possédez maintenant le cycle complet de la manipulation du DOM : Sélectionner, Modifier, Créer et Supprimer. Vous avez tous les outils nécessaires pour construire des applications web entièrement dynamiques. Demain, nous assemblons tout cela pour finaliser le projet de la semaine.

---

### J5 (Vendredi) : Projet de la Semaine - La To-Do List Interactive

**Objectif(s) du Jour :**
- Structurer un petit projet JS de manipulation du DOM.
- Gérer l'ajout, la suppression et le marquage de tâches.
- Comprendre la "délégation d'événements" pour gérer les clics sur des éléments qui n'existent pas encore.

**Notion Clé : Délégation d'Événements**
Problème : comment ajouter un `addEventListener` à un bouton "Supprimer" qui n'existe pas encore au chargement de la page ? Réponse : on ne le fait pas. On place **un seul** écouteur d'événement sur le conteneur parent (la liste `<ul>`). Quand un clic se produit à l'intérieur, l'événement "remonte" jusqu'au parent. On peut alors vérifier la cible (`event.target`) du clic. SI la cible est un bouton "Supprimer", ALORS on exécute la logique de suppression. C'est beaucoup plus performant et plus simple que d'ajouter un écouteur à chaque `<li>`.

---

#### PROJET DE LA SEMAINE : La To-Do List Interactive

**La Mission :**
Finaliser l'application To-Do List en y ajoutant les fonctionnalités de suppression et de marquage.

**Cahier des Charges / Étapes :**
1.  **Structure HTML/CSS :** Assurez-vous d'avoir une structure propre. Dans votre CSS, créez une classe `.completed` qui, par exemple, raye le texte (`text-decoration: line-through;`) et le met en gris.

2.  **Logique d'Ajout (Déjà faite hier) :**
    - Écoutez la soumission du formulaire.
    - Empêchez le rechargement.
    - Récupérez le texte de l'input.
    - Si le texte est valide, créez un `<li>`, mettez-y le texte, et ajoutez-le à la liste `<ul>`.
    - **Modification :** En plus du texte, ajoutez un bouton "Supprimer" à l'intérieur de chaque `<li>` que vous créez.
      ```javascript
      const deleteButton = document.createElement('button');
      deleteButton.textContent = "X";
      nouvelItem.appendChild(deleteButton);
      ```

3.  **Logique de Suppression et de Marquage (Délégation d'événements) :**
    - Ajoutez **un seul** `addEventListener('click', ...)` sur la liste parente (`<ul>`).
    - Dans la fonction de callback, utilisez `event.target` pour savoir sur quoi l'utilisateur a cliqué précisément.
    - **Pour marquer comme terminé :** Si `event.target` est un `<li>`, utilisez `.classList.toggle('completed')` sur cet élément.
    - **Pour supprimer :** Si `event.target` est un `<button>`, alors trouvez son parent `<li>` (ex: `event.target.parentElement`) et appelez `.remove()` sur ce parent.

**Livrable :**
Un dossier de projet avec `index.html`, `style.css` et `script.js` fonctionnels. Le tout doit être déposé sur votre dépôt GitHub.

**Bonus :**
- Utilisez le `localStorage` du navigateur pour sauvegarder les tâches, afin qu'elles ne disparaissent pas au rechargement de la page.
- Améliorez le design pour que l'application soit plus agréable à utiliser.

#### Synthèse Finale de la Semaine

**Incroyable !** Vous avez transformé une page statique en une véritable application web miniature. Vous maîtrisez désormais le cycle complet de l'interaction côté client : écouter l'utilisateur, lire ses intentions, et modifier la page en conséquence pour lui donner un retour instantané. La manipulation du DOM est la compétence la plus fondamentale du développement frontend, et vous venez de la maîtriser à travers un projet concret.

La semaine prochaine, nous aborderons la communication avec l'extérieur : comment utiliser JavaScript pour aller chercher des données sur des serveurs distants (des API) et les afficher dans nos applications. Vous pourrez ainsi créer une application météo, un catalogue de films, et bien plus encore.