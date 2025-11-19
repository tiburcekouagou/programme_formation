# Module 3 : L'Interactivité avec JavaScript

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Intégrer et exécuter du code JavaScript dans une page web.
- Maîtriser les concepts fondamentaux de la programmation : variables, conditions, boucles et fonctions.
- Manipuler le DOM (Document Object Model) pour modifier le contenu et le style d'une page en temps réel.
- Réagir aux actions de l'utilisateur (clics, saisie clavier, soumission de formulaire) en utilisant des écouteurs d'événements.
- Travailler avec des structures de données comme les tableaux et les objets.
- Communiquer avec des serveurs distants pour récupérer des données via des API (AJAX/Fetch).
- Écrire un code propre, organisé et facile à déboguer.

## 2. Prérequis

- Avoir complété les **Modules 1 (HTML)** et **2 (CSS)**.
- Une compréhension solide de la structure HTML et des sélecteurs CSS.
- Un éditeur de texte (VS Code) et un navigateur web.
- **Nouveau meilleur ami :** la console des outils de développement de votre navigateur (accessible avec `F12` ou `Cmd+Option+I`).

## 3. Résumé du Concept (Qu'est-ce que JavaScript ?)

Si HTML est le squelette et CSS l'apparence, **JavaScript (JS) est le système nerveux et le cerveau**. C'est un véritable **langage de programmation** qui s'exécute directement dans le navigateur de l'utilisateur.

Son rôle est de rendre la page *vivante*. Au lieu de simplement afficher du contenu, une page avec JavaScript peut réagir, changer et communiquer. C'est grâce à lui que vous pouvez : cliquer sur un bouton et voir une fenêtre apparaître, soumettre un formulaire sans recharger la page, voir un fil d'actualité se mettre à jour automatiquement, ou jouer à un jeu.

Vous n'allez plus seulement *décrire* une page, vous allez lui donner des *ordres* : "Quand l'utilisateur clique sur ce bouton, change la couleur de ce titre." ou "Va chercher la météo sur ce serveur et affiche-la ici."

## 4. Plan d’Apprentissage

*   **Chapitre 1 : Introduction et Fondamentaux**
    *   Lier un fichier JS
    *   Variables (`let`, `const`), types de données
    *   Utiliser `console.log()` pour déboguer
*   **Chapitre 2 : Logique et Fonctions**
    *   Opérateurs, conditions (`if/else`)
    *   Les fonctions : le cœur de la réutilisation
*   **Chapitre 3 : JavaScript rencontre HTML : Le DOM**
    *   Sélectionner des éléments (`querySelector`)
    *   Modifier le contenu (`.textContent`, `.innerHTML`) et les styles (`.style`)
*   **Chapitre 4 : La Gestion des Événements**
    *   Écouter les actions utilisateur (`addEventListener`)
    *   L'objet `event`
*   **Chapitre 5 : Tableaux et Boucles**
    *   Stocker des listes de données dans des tableaux (Arrays)
    *   Parcourir ces listes avec des boucles (`for`, `forEach`)
*   **Chapitre 6 : Aller plus loin : Les API avec Fetch**
    *   Introduction au JSON (le format de données du web)
    *   Faire des requêtes HTTP avec `fetch` pour obtenir des données externes

## 5. Leçons

### Leçon 1 : Introduction et Fondamentaux

On commence par écrire notre première ligne de JS. La console est notre laboratoire : elle nous permet d'afficher des valeurs et des messages pour comprendre ce que fait notre code. Les variables sont des "boîtes" nommées pour stocker des informations.

- **Exemple de code simple :**
  *Fichier `script.js`*
  ```javascript
  // Affiche un message dans la console du navigateur
  console.log("Hello, World!");

  // Déclare une variable qui peut changer
  let userAge = 30;
  // Déclare une constante qui ne peut pas changer
  const userName = "Alice";

  console.log(userName + " a " + userAge + " ans."); // Affiche "Alice a 30 ans."
  ```
- **Exemple de code appliqué à un cas réel (lier le script à notre CV) :**
  *Fichier `cv.html` (juste avant la fermeture de la balise `</body>`)*
  ```html
  <script src="script.js"></script>
  </body>
  ```
  *Fichier `script.js`*
  ```javascript
  const posteRecherche = "Développeur Web Full-Stack";
  console.log("La personne recherche le poste de : " + posteRecherche);
  ```

### Leçon 2 : Logique et Fonctions

Les conditions (`if/else`) permettent à notre code de prendre des décisions. Les fonctions sont des blocs de code réutilisables que l'on peut "appeler" pour exécuter une tâche spécifique. C'est la base de l'organisation en JS.

- **Exemple de code simple :**
  ```javascript
  function saluer(nom) {
    if (nom) {
      console.log("Bonjour, " + nom + " !");
    } else {
      console.log("Bonjour, illustre inconnu !");
    }
  }

  saluer("Bob"); // Affiche "Bonjour, Bob !"
  saluer();      // Affiche "Bonjour, illustre inconnu !"
  ```
- **Exemple de code appliqué (une fonction pour calculer l'âge) :**
  ```javascript
  function calculerAge(anneeDeNaissance) {
    const anneeActuelle = 2023;
    return anneeActuelle - anneeDeNaissance;
  }

  const age = calculerAge(1995);
  console.log("Cette personne a environ " + age + " ans."); // Affiche "Cette personne a environ 28 ans."
  ```

### Leçon 3 : JavaScript rencontre HTML : Le DOM

C'est ici que la magie opère ! JavaScript peut lire et modifier la structure HTML et les styles CSS de la page. On "sélectionne" un élément (comme en CSS) puis on le manipule.

- **Exemple de code simple :**
  ```html
  <h1 id="titre">Titre Initial</h1>
  ```
  ```javascript
  // 1. Sélectionner l'élément
  const monTitre = document.querySelector("#titre");
  
  // 2. Modifier son contenu
  monTitre.textContent = "Nouveau Titre !";

  // 3. Modifier son style
  monTitre.style.color = "red";
  ```
- **Exemple de code appliqué (personnaliser le titre de notre CV) :**
  ```html
  <!-- Dans cv.html -->
  <h1 id="main-title">Mon Nom</h1>
  ```
  ```javascript
  const nom = "Jeanne Doe";
  const titre = document.querySelector("#main-title");
  titre.textContent = `CV de ${nom}`; // Utilisation des "template literals" (plus modernes)
  ```

### Leçon 4 : La Gestion des Événements

Nous allons maintenant écouter ce que fait l'utilisateur. `addEventListener` nous permet d'attacher une fonction à un événement (comme un `click`) sur un élément HTML.

- **Exemple de code simple :**
  ```html
  <button id="mon-bouton">Cliquez-moi</button>
  ```
  ```javascript
  const bouton = document.querySelector("#mon-bouton");

  bouton.addEventListener("click", function() {
    alert("Vous avez cliqué !");
  });
  ```
- **Exemple de code appliqué (un bouton "mode sombre" pour notre CV) :**
  ```html
  <!-- Dans cv.html, par exemple dans le header -->
  <button id="dark-mode-toggle">Mode Sombre</button>
  ```
  ```javascript
  const toggleBtn = document.querySelector("#dark-mode-toggle");
  const body = document.querySelector("body");

  toggleBtn.addEventListener("click", function() {
    // Ajoute ou enlève la classe 'dark-mode' du body
    body.classList.toggle("dark-mode"); 
  });
  
  // Il faudrait ensuite définir les styles de .dark-mode dans le CSS.
  ```

### Leçon 5 : Tableaux et Boucles

Pour gérer des listes de données (expériences, compétences, articles...), on utilise des tableaux (Arrays). Pour agir sur chaque élément d'un tableau, on utilise des boucles.

- **Exemple de code simple :**
  ```javascript
  const fruits = ["Pomme", "Banane", "Fraise"];

  // La boucle forEach exécute une fonction pour chaque élément
  fruits.forEach(function(fruit) {
    console.log("J'aime la " + fruit);
  });
  ```
- **Exemple de code appliqué (afficher dynamiquement les compétences du CV) :**
  ```html
  <!-- Dans cv.html, la section compétences avec un <ul> vide -->
  <section>
    <h2>Compétences</h2>
    <ul id="skills-list"></ul>
  </section>
  ```
  ```javascript
  const competences = ["HTML5", "CSS3", "JavaScript", "Esprit d'équipe"];
  const liste = document.querySelector("#skills-list");

  competences.forEach(function(competence) {
    // 1. Créer un nouvel élément <li>
    const li = document.createElement("li");
    // 2. Lui donner du contenu
    li.textContent = competence;
    // 3. L'ajouter à la liste <ul>
    liste.appendChild(li);
  });
  ```

### Leçon 6 : Aller plus loin : Les API avec Fetch

Les applications modernes communiquent constamment avec des serveurs pour obtenir des données à jour. L'API `fetch` est l'outil standard en JavaScript pour faire ces requêtes réseau de manière asynchrone (sans bloquer la page).

- **Exemple de code simple (récupérer une blague aléatoire) :**
  ```javascript
  fetch("https://official-joke-api.appspot.com/random_joke")
    .then(response => response.json()) // Convertit la réponse en objet JSON
    .then(data => {
      console.log(data.setup);    // Affiche la question
      console.log(data.punchline); // Affiche la chute
    })
    .catch(error => console.error("Oups, une erreur :", error)); // Gère les erreurs
  ```
- **Exemple de code appliqué (afficher le nombre de dépôts publics sur votre profil GitHub) :**
  ```javascript
  const githubUsername = "facebook"; // Remplacez par un vrai pseudo
  const githubInfo = document.querySelector("#github-info"); // Un <p> à créer dans le HTML

  fetch(`https://api.github.com/users/${githubUsername}`)
    .then(response => response.json())
    .then(user => {
      githubInfo.textContent = `Ce profil GitHub a ${user.public_repos} dépôts publics.`;
    })
    .catch(error => {
      githubInfo.textContent = "Impossible de charger les données GitHub.";
      console.error(error);
    });
  ```

## 6. Exercices Pratiques

- **Niveau Débutant : Le Convertisseur de Devise**
  Créez une page avec un champ `<input>` et un bouton. Écrivez un script JS qui lit la valeur en euros dans l'input, la multiplie par un taux de change fixe (ex: 1.1 pour les dollars), et affiche le résultat dans un `<p>` quand on clique sur le bouton.

- **Niveau Intermédiaire : Le Générateur de Citations**
  Créez un tableau JS contenant 5 objets, chaque objet ayant une propriété `quote` et `author`. Créez une page avec un `<p>` pour la citation, un autre pour l'auteur, et un bouton "Nouvelle citation". À chaque clic, votre script doit choisir une citation au hasard dans le tableau et l'afficher sur la page.

- **Niveau Avancé : L'Accordéon (FAQ)**
  Créez une liste de questions/réponses en HTML. Par défaut, seules les questions sont visibles. En utilisant JavaScript, faites en sorte que lorsque l'on clique sur une question, la réponse correspondante apparaisse ou disparaisse (en ajoutant/retirant une classe CSS `.visible` par exemple).

## 7. Mini-projet Guidé : La To-Do List

C'est le projet classique pour apprendre le JS et la manipulation du DOM.

1.  **Étape 1 : Le HTML**
    Créez `index.html` avec un `<h1>`, un `<form>` contenant un `<input type="text">` et un `<button>`, et une liste non ordonnée `<ul>` vide.
    ```html
    <h1>Ma To-Do List</h1>
    <form id="todo-form">
      <input type="text" id="todo-input" placeholder="Ajouter une tâche...">
      <button type="submit">Ajouter</button>
    </form>
    <ul id="todo-list"></ul>
    ```

2.  **Étape 2 : La Sélection des Éléments**
    Dans `script.js`, utilisez `document.querySelector` pour récupérer le formulaire, l'input et la liste `<ul>` dans des variables.

3.  **Étape 3 : Écouter la Soumission du Formulaire**
    Ajoutez un `addEventListener` sur l'événement `submit` du formulaire. N'oubliez pas d'utiliser `event.preventDefault()` au début de la fonction pour empêcher la page de se recharger !

4.  **Étape 4 : Créer et Ajouter la Tâche**
    Dans la fonction de l'événement :
    a. Récupérez le texte de l'input (`input.value`).
    b. Si le texte n'est pas vide, créez un nouvel élément `<li>` (`document.createElement`).
    c. Attribuez le texte de l'input au `textContent` du `<li>`.
    d. Ajoutez ce `<li>` à la liste `<ul>` avec `list.appendChild(li)`.
    e. Videz le champ input (`input.value = ""`).

5.  **Étape 5 (Bonus) : Marquer comme Fait et Supprimer**
    Modifiez l'étape 4 pour qu'en plus du texte, le `<li>` contienne un bouton "Supprimer". Ajoutez deux `addEventListener` : un sur le `<li>` lui-même pour basculer une classe CSS `.completed` (qui raye le texte), et un sur le bouton "Supprimer" pour enlever le `<li>` du DOM (`li.remove()`).

## 8. Projet Final Non Guidé : Application Météo Simple

Créez une application d'une seule page qui affiche la météo d'une ville recherchée.

**Livrables :**
1.  Un dossier de projet contenant `index.html`, `style.css`, et `script.js`.
2.  Le design doit être simple, propre et responsive.

**Fonctionnalités requises :**
- Un champ de recherche pour taper le nom d'une ville et un bouton "Rechercher".
- Quand l'utilisateur recherche une ville, votre script doit :
  1.  Appeler une API météo (ex: **OpenWeatherMap** - vous devrez vous inscrire pour obtenir une clé API gratuite).
  2.  Afficher un message de chargement pendant que les données sont récupérées.
  3.  Une fois les données reçues, afficher les informations principales : nom de la ville, température actuelle, description du temps (ex: "Ensoleillé"), et une icône représentant le temps.
  4.  Gérer les erreurs : si la ville n'est pas trouvée ou si l'API ne répond pas, afficher un message d'erreur clair à l'utilisateur.

## 9. Critères d'Évaluation

- **Fonctionnalité :** L'application fonctionne-t-elle comme décrit ? Les cas d'erreur sont-ils gérés ?
- **Qualité du code JS :** Le code est-il lisible, bien organisé en fonctions ? Les noms de variables sont-ils clairs ?
- **Manipulation du DOM :** La mise à jour de la page est-elle efficace et sans bugs visuels ?
- **Asynchronisme :** L'appel `fetch` est-il correctement implémenté, avec gestion des `Promise` (`.then`/`.catch` ou `async/await`) ?
- **Séparation des préoccupations :** HTML, CSS et JS sont-ils bien dans leurs fichiers respectifs ?
- **Débogage :** La console est-elle propre en utilisation normale (pas d'erreurs, pas de `console.log` inutiles laissés dans le code final) ?

## 10. Ressources Complémentaires Fiables

- **MDN Web Docs :** La documentation de référence ultime pour tout JS.
  - [Un Premier Pas en JavaScript](https://developer.mozilla.org/fr/docs/Learn/JavaScript/First_steps)
- **JavaScript.info :** Un tutoriel en ligne moderne, extrêmement complet et clair, du débutant à l'expert.
  - [The Modern JavaScript Tutorial](https://javascript.info/)
- **freeCodeCamp :** Leur certification "JavaScript Algorithms and Data Structures" est une excellente suite d'exercices interactifs.
  - [JavaScript Algorithms and Data Structures](https://www.freecodecamp.org/learn/javascript-algorithms-and-data-structures/)
- **Public APIs :** Une liste gigantesque d'API publiques gratuites pour vous entraîner après le projet météo.
  - [GitHub - Public APIs](https://github.com/public-apis/public-apis)