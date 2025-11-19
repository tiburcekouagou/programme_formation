## Semaine 7 : JavaScript Asynchrone et APIs

### J1 : Le Problème du Temps : L'Asynchrone et les Callbacks

**Objectif(s) du Jour :**
- Comprendre pourquoi le code synchrone est bloquant et problématique pour les tâches longues.
- Découvrir le concept de programmation asynchrone.
- Mettre en œuvre la première solution historique : les fonctions de rappel (callbacks).

**Notion Clé : La File d'Attente au Restaurant**
Imaginez un restaurant rapide.
- **Mode Synchrone (bloquant) :** Vous passez commande, et vous êtes obligé d'attendre au comptoir, sans bouger, que votre plateau soit prêt. Personne ne peut commander derrière vous. Tout est bloqué à cause de vous. C'est inefficace.
- **Mode Asynchrone (non-bloquant) :** Vous passez commande, on vous donne un bipeur, et vous allez vous asseoir. Le cuisinier prépare votre plat en arrière-plan. Quand c'est prêt, le bipeur sonne (**c'est le callback !**). Vous pouvez alors aller chercher votre plateau. Pendant ce temps, d'autres clients ont pu commander. L'interface utilisateur de votre navigateur fonctionne exactement comme ça : elle ne peut pas se permettre de "geler" en attendant qu'une image se télécharge ou qu'une donnée arrive.

---

#### Leçon

##### 1. Le Monde Synchrone

Par défaut, JavaScript exécute les instructions les unes après les autres, dans l'ordre.
```javascript
console.log("Instruction 1");
console.log("Instruction 2"); // Ne s'exécute que lorsque la 1 est finie
console.log("Instruction 3"); // Ne s'exécute que lorsque la 2 est finie
```
Si l'instruction 2 prend 10 secondes, toute l'application est gelée pendant 10 secondes.

##### 2. L'Asynchrone avec `setTimeout`

La fonction `setTimeout` est l'exemple le plus simple d'une fonction asynchrone. Elle prend deux arguments : une fonction à exécuter (le "callback") et un délai en millisecondes.

- **Exemple de Code (Non-bloquant) :**
  ```javascript
  console.log("Début du script");

  setTimeout(function() {
    // Cette fonction est le "callback"
    console.log("Ce message s'affiche après 2 secondes");
  }, 2000); // 2000 ms = 2 secondes

  console.log("Fin du script");

  // Ordre d'affichage dans la console :
  // 1. "Début du script"
  // 2. "Fin du script"
  // 3. (2 secondes plus tard) "Ce message s'affiche après 2 secondes"
  ```
  Le script ne s'arrête pas pour attendre ! Il lance le minuteur et continue son exécution.

##### 3. L'Enfer des Callbacks ("Callback Hell")

Que se passe-t-il si l'on doit enchaîner plusieurs opérations asynchrones ? On imbrique les callbacks les uns dans les autres, créant une "pyramide" illisible.

```javascript
// À ne pas faire ! C'est le "Callback Hell"
tacheAsynchrone1(function(resultat1) {
  tacheAsynchrone2(resultat1, function(resultat2) {
    tacheAsynchrone3(resultat2, function(resultat3) {
      console.log("C'est terminé !");
    });
  });
});
```

---

#### Mise en Pratique

1.  Créez un nouveau dossier pour cette semaine, et à l'intérieur, un fichier `jour1.html` avec une balise `<script src="jour1.js"></script>`.
2.  Dans `jour1.js`, reproduisez l'exemple de code avec `setTimeout`. Ouvrez la page dans le navigateur et observez la console pour bien comprendre l'ordre d'exécution.
3.  Simulez une séquence de tâches : Affichez "Étape 1" immédiatement. Puis, après 1 seconde, affichez "Étape 2". Enfin, 1 seconde *après* l'étape 2, affichez "Étape 3". Vous devrez imbriquer un `setTimeout` dans un autre.

#### Mini-Exercice du Jour

Créez une fonction `direBonjour(nom, callback)`. Cette fonction doit simuler une tâche de 1 seconde avec `setTimeout`, puis appeler le `callback` en lui passant la chaîne de caractères `"Bonjour, " + nom`. Appelez votre fonction `direBonjour` en lui fournissant un nom et une fonction de callback qui affiche le résultat dans la console.

#### Synthèse

Aujourd'hui, vous avez touché du doigt le cœur du JavaScript interactif : l'asynchrone. Vous avez compris le problème et expérimenté la première solution, les callbacks. Demain, nous découvrirons une solution bien plus propre et puissante pour éviter le "Callback Hell" : les Promesses.

---

### J2 : Tenir sa Parole - Les Promesses (Promises)

**Objectif(s) du Jour :**
- Comprendre ce qu'est une Promesse et à quoi elle sert.
- Savoir créer et "consommer" une Promesse.
- Gérer les cas de succès (`.then()`) et d'échec (`.catch()`).

**Notion Clé : Le Numéro de Suivi de Colis**
Quand vous commandez en ligne, vous ne recevez pas le produit instantanément. À la place, on vous donne un numéro de suivi : une **Promesse** de livraison.
- Cet objet "Promesse" a un état initial : **en attente** (`pending`).
- Si tout se passe bien, le colis arrive. La promesse est **tenue** (`fulfilled`). Vous pouvez alors *faire quelque chose* avec votre colis (l'utiliser, `.then()`).
- S'il y a un problème (colis perdu), la promesse est **rompue** (`rejected`). Vous devez gérer ce problème (contacter le service client, `.catch()`).
Une Promesse est un objet qui représente l'aboutissement (ou l'échec) futur d'une opération asynchrone.

---

#### Leçon

##### 1. La Structure d'une Promesse

On crée une promesse avec `new Promise()`. Elle prend une fonction en argument avec deux paramètres : `resolve` (pour dire "c'est un succès") et `reject` (pour dire "c'est un échec").

```javascript
const maPromesse = new Promise((resolve, reject) => {
  // Simule une opération qui prend du temps
  setTimeout(() => {
    const succes = true; // Changez à 'false' pour tester l'échec
    if (succes) {
      resolve("Opération réussie !"); // La promesse est tenue
    } else {
      reject("Erreur durant l'opération."); // La promesse est rompue
    }
  }, 2000);
});
```

##### 2. Consommer la Promesse

On utilise les méthodes `.then()` et `.catch()` pour réagir au résultat de la promesse.

```javascript
console.log("Je lance la promesse...");

maPromesse
  .then((messageDeSucces) => {
    // Ce bloc s'exécute si 'resolve' a été appelé
    console.log("SUCCÈS : " + messageDeSucces);
  })
  .catch((messageDErreur) => {
    // Ce bloc s'exécute si 'reject' a été appelé
    console.log("ÉCHEC : " + messageDErreur);
  });

console.log("...la promesse est lancée, le script continue.");
```

##### 3. L'Enchaînement (`.then().then()...`)

La grande force des promesses est de pouvoir enchaîner les opérations asynchrones de manière lisible, sans imbrication.

```javascript
operation1()
  .then(resultat1 => operation2(resultat1))
  .then(resultat2 => operation3(resultat2))
  .then(resultatFinal => console.log(resultatFinal))
  .catch(erreur => console.error("Une erreur est survenue:", erreur));
```

---

#### Mise en Pratique

1.  Créez un fichier `jour2.js` et le `jour2.html` correspondant.
2.  Reprenez le code du mini-exercice d'hier (`direBonjour`). Transformez-le ! Créez une nouvelle fonction `direBonjourPromise(nom)` qui ne prend plus de callback, mais qui **retourne une promesse**.
3.  Cette promesse devra être résolue après 1 seconde avec le message `"Bonjour, " + nom`.
4.  Appelez cette fonction et utilisez `.then()` pour afficher le message de succès dans la console.

#### Mini-Exercice du Jour

Créez une promesse qui simule le lancement d'un dé. Elle doit se résoudre avec un nombre aléatoire entre 1 et 6. Si le résultat est supérieur ou égal à 4, la promesse est tenue (`resolve`). Sinon, elle est rompue (`reject`). Consommez cette promesse et affichez "Gagné !" ou "Perdu !" en fonction du résultat.

#### Synthèse

Les promesses nettoient énormément le code asynchrone. Vous avez maintenant une méthode robuste pour gérer les opérations qui prennent du temps. Demain, nous allons découvrir la syntaxe la plus moderne et la plus agréable pour travailler avec les promesses : `async/await`.

---

### J3 : Rendre l'Asynchrone Lisible - `async/await`

**Objectif(s) du Jour :**
- Découvrir la syntaxe `async/await`.
- Comprendre qu'il s'agit d'une surcouche syntaxique aux Promesses.
- Apprendre à gérer les erreurs avec `try...catch` dans un contexte asynchrone.

**Notion Clé : Écrire une Recette de Cuisine**
Avec les promesses et `.then()`, c'est comme si vous disiez : "Lance la cuisson du gâteau, ET ENSUITE, une fois que c'est fait, prépare le glaçage".
Avec `async/await`, vous écrivez la recette comme vous la pensez :
1.  **Attends** que le gâteau soit cuit. (`await cuisson()`)
2.  Prépare le glaçage.

C'est la même logique, mais écrite de manière séquentielle et beaucoup plus naturelle à lire. `async/await` permet d'écrire du code asynchrone qui ressemble à du code synchrone.

---

#### Leçon

##### 1. La fonction `async`

Pour pouvoir utiliser `await`, il faut être à l'intérieur d'une fonction déclarée avec le mot-clé `async`. Une fonction `async` retourne **toujours** une promesse, implicitement.

```javascript
async function maFonctionAsynchrone() {
  // ... code avec await
  return "Valeur finale"; // Cette valeur sera la résolution de la promesse retournée
}
```

##### 2. Le mot-clé `await`

`await` met en pause l'exécution de la fonction `async` **uniquement**, jusqu'à ce que la promesse qu'il attend soit résolue. Il "déballe" ensuite la valeur de la promesse. `await` ne peut être utilisé que dans une fonction `async`.

```javascript
// En reprenant notre promesse d'hier : direBonjourPromise(nom)
async function saluer() {
  console.log("Début de la salutation...");
  const message = await direBonjourPromise("Alice"); // Met en pause ICI jusqu'à la résolution
  console.log(message); // S'exécute seulement après la résolution
  console.log("Fin de la salutation.");
}

saluer();
```

##### 3. Gestion des Erreurs avec `try...catch`

Comment gérer les échecs (`reject`) ? On entoure notre code "à risque" (celui avec `await`) d'un bloc `try...catch`, exactement comme en code synchrone.

```javascript
async function saluerEnTouteSecurite() {
  try {
    const message = await unePromesseQuiPeutEchouer();
    console.log("Succès :", message);
  } catch (erreur) {
    // Si la promesse est 'rejected', le code saute directement dans ce bloc 'catch'
    console.error("Échec :", erreur);
  }
}
```

---

#### Mise en Pratique

1.  Créez les fichiers `jour3.js` et `jour3.html`.
2.  Reprenez votre fonction `direBonjourPromise` du jour 2 (vous n'avez pas besoin de la modifier).
3.  Créez une nouvelle fonction `async` nommée `main`.
4.  À l'intérieur de `main`, utilisez `await` pour appeler `direBonjourPromise("Bob")` et stockez le résultat dans une variable.
5.  Affichez cette variable dans la console.
6.  Appelez la fonction `main()`. Comparez la lisibilité de ce code par rapport à la version avec `.then()`.

#### Mini-Exercice du Jour

Reprenez l'exercice du dé (jour 2). Réécrivez la logique de consommation de la promesse en utilisant `async/await` et un bloc `try...catch` pour afficher "Gagné !" en cas de succès et "Perdu !" en cas d'échec.

#### Synthèse

Vous maîtrisez maintenant la syntaxe la plus moderne et la plus utilisée pour gérer l'asynchronisme en JavaScript. `async/await` est votre meilleur ami pour écrire du code clair et maintenable. Demain, nous allons utiliser cette nouvelle super-compétence pour faire ce pour quoi elle a été conçue : communiquer avec le monde extérieur via des APIs.

---

### J4 : Parler au Monde - L'API `fetch()` et le JSON

**Objectif(s) du Jour :**
- Comprendre ce qu'est une API (Application Programming Interface).
- Utiliser l'API `fetch()` du navigateur pour envoyer des requêtes HTTP.
- Comprendre et manipuler le format de données JSON.

**Notion Clé : Commander au Menu de l'API**
Une **API**, c'est comme le menu d'un restaurant. Vous ne rentrez pas dans la cuisine (la base de données du serveur) pour vous servir. Vous consultez le menu (`la documentation de l'API`) qui vous dit ce que vous pouvez commander (`les "endpoints"`), comment le commander (`GET`, `POST`...) et ce que vous recevrez en retour (`le format des données`, souvent du JSON). `fetch()` est le serveur qui prend votre commande et vous la rapporte.

**JSON (JavaScript Object Notation)** est simplement du texte qui ressemble beaucoup à un objet JavaScript. C'est la langue universelle des APIs web.

---

#### Leçon

##### 1. L'API `fetch()`

`fetch()` est une fonction moderne, intégrée aux navigateurs, qui permet de faire des requêtes réseau. Elle est basée sur les Promesses.

```javascript
fetch('https://api.example.com/data') // 'fetch' retourne une promesse
  .then(response => {
    // La promesse se résout avec un objet 'Response'
    // Ce n'est PAS encore la donnée, juste la réponse HTTP
    console.log(response);
  })
  .catch(error => console.error("Erreur réseau:", error));
```

##### 2. Obtenir les Données : la méthode `.json()`

L'objet `Response` a une méthode `.json()` pour extraire le corps de la réponse et le transformer de texte JSON en un véritable objet/tableau JavaScript. Attention, `.json()`... **retourne aussi une promesse !**

- **Exemple avec `.then()` :**
  ```javascript
  fetch('https://jsonplaceholder.typicode.com/users/1')
    .then(response => response.json()) // Étape 1 : transformer la réponse en JSON
    .then(data => { // Étape 2 : travailler avec la donnée finale
      console.log(data);
      console.log("Nom de l'utilisateur :", data.name);
    })
    .catch(error => console.error("Erreur:", error));
  ```

##### 3. `fetch` avec `async/await` (la meilleure façon)

C'est là que la magie opère. La syntaxe devient limpide.

- **Exemple avec `async/await` :**
  ```javascript
  async function recupererUtilisateur() {
    try {
      const response = await fetch('https://jsonplaceholder.typicode.com/users/1');
      // On attend la réponse HTTP
      
      const data = await response.json(); 
      // On attend que les données JSON soient extraites et parsées

      console.log(data.name);
    } catch (error) {
      console.error("Impossible de récupérer l'utilisateur:", error);
    }
  }

  recupererUtilisateur();
  ```

---

#### Mise en Pratique

1.  Créez les fichiers `jour4.js` et `jour4.html`.
2.  Écrivez une fonction `async` nommée `fetchPosts`.
3.  Dans cette fonction, utilisez `fetch` et `await` pour récupérer la liste des "posts" depuis l'URL : `https://jsonplaceholder.typicode.com/posts`.
4.  Affichez le tableau de posts obtenu dans la console.
5.  Appelez votre fonction.

#### Mini-Exercice du Jour

Créez une fonction `async` `fetchTodoById(id)`. Cette fonction doit prendre un `id` en argument et récupérer la "todo" correspondante depuis `https://jsonplaceholder.typicode.com/todos/{id}`. Affichez le titre de la "todo" dans la console. Appelez-la avec un `id` de votre choix.

#### Synthèse

Vous savez maintenant comment faire communiquer votre application avec n'importe quel service sur internet. C'est une compétence absolument fondamentale. Vous avez toutes les briques pour le projet de la semaine : écouter l'utilisateur, interroger un service externe, et afficher le résultat. Demain, on assemble tout ça !

---

### J5 : Projet de la Semaine - L'Application Météo

**Objectif(s) du Jour :**
- Structurer une petite application complète : HTML, CSS et JS.
- Lier une action utilisateur (clic) à une requête API.
- Mettre à jour le DOM dynamiquement avec les données reçues.
- Consolider toutes les connaissances de la semaine dans un projet concret.

**Notion Clé : La Boucle d'Interaction Complète**
Aujourd'hui, nous fermons la boucle :
1.  **Utilisateur :** Saisit une ville et clique sur un bouton.
2.  **DOM & JS :** Un `addEventListener` capture le clic.
3.  **JS Asynchrone :** Notre code `async` prend la ville, construit l'URL de l'API et `await fetch()` les données météo.
4.  **API Externe :** Le service météo nous renvoie les données en JSON.
5.  **DOM & JS :** Notre code reçoit les données, extrait la température, la description, etc., et met à jour le contenu des balises HTML pour les afficher à l'utilisateur.

---

#### Leçon

##### 1. Structure du Projet

- **`index.html` :** Un formulaire simple avec un `<input type="text">` pour le nom de la ville et un `<button>`. Et des éléments vides avec des IDs pour afficher les résultats (ex: `<div id="temperature"></div>`, `<p id="description"></p>`).
- **`style.css` (optionnel) :** Un peu de style pour que ce ne soit pas trop moche.
- **`app.js` :** Le cerveau de l'application.

##### 2. La Logique dans `app.js`

```javascript
// 1. Sélectionner les éléments du DOM
const form = document.querySelector('form');
const input = document.querySelector('input');
const tempDisplay = document.querySelector('#temperature');
const descDisplay = document.querySelector('#description');
// ...etc

// 2. Ajouter l'écouteur d'événement
form.addEventListener('submit', (event) => {
  event.preventDefault(); // Empêche la page de se recharger
  const ville = input.value;
  getWeatherData(ville);
});

// 3. La fonction asynchrone qui fait le travail
async function getWeatherData(city) {
  // IMPORTANT: Il faudra une clé API !
  const apiKey = 'VOTRE_CLÉ_API_PERSONNELLE';
  const url = `https://api.openweathermap.org/data/2.5/weather?q=${city}&appid=${apiKey}&units=metric&lang=fr`;

  try {
    const response = await fetch(url);
    if (!response.ok) { // Gérer les erreurs HTTP (ex: ville non trouvée)
      throw new Error(`Erreur: ${response.status}`);
    }
    const data = await response.json();

    // 4. Mettre à jour le DOM
    tempDisplay.textContent = `${Math.round(data.main.temp)} °C`;
    descDisplay.textContent = data.weather[0].description;
    // ...etc
  } catch (error) {
    // Gérer les erreurs (réseau, ville invalide...)
    console.error(error);
    alert("Impossible de récupérer les données météo pour cette ville.");
  }
}
```

---

#### PROJET DE LA SEMAINE : Application Météo

Votre mission est de construire une application web fonctionnelle qui affiche la météo actuelle pour une ville donnée.

**Pré-requis :**
1.  Allez sur [OpenWeatherMap](https://openweathermap.org/) et créez un compte gratuit.
2.  Allez dans la section "API keys" de votre compte pour obtenir votre clé API personnelle. Il faut parfois attendre quelques minutes/heures pour qu'elle soit active.

**Contraintes Obligatoires :**
1.  **HTML :** Doit contenir un champ de saisie pour le nom de la ville et un bouton pour lancer la recherche. Doit aussi contenir des éléments HTML prêts à accueillir les résultats (température, description, nom de la ville, une icône météo).
2.  **JavaScript :**
    - Le code doit utiliser `async/await` et `fetch` pour interroger l'API d'OpenWeatherMap.
    - L'application ne doit pas se recharger lors de la soumission du formulaire.
    - La clé API ne doit **PAS être en dur dans le code partagé sur GitHub** (c'est une bonne pratique, mais pour ce projet, une alerte suffit. Pour aller plus loin, on utiliserait des variables d'environnement).
    - L'application doit gérer les erreurs (ex: si la ville n'existe pas) et afficher un message clair à l'utilisateur.
    - Les données affichées doivent être : le nom de la ville, la température (arrondie), la description du temps (ex: "ciel dégagé"), et l'icône correspondante (l'API fournit un code d'icône, vous pouvez construire l'URL de l'image comme ceci : `http://openweathermap.org/img/wn/CODE_ICONE@2x.png`).
3.  **Déploiement :** Le projet final doit être fonctionnel et déployé sur GitHub Pages ou Netlify.

**Livrable :** L'URL de votre dépôt GitHub contenant le projet, et l'URL de l'application déployée.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez traversé l'un des chapitres les plus complexes et les plus puissants du JavaScript moderne. Vous êtes passé de la simple manipulation du DOM à la création d'applications dynamiques qui communiquent avec le monde extérieur. Ce projet est un excellent ajout à votre portfolio. La semaine prochaine, nous allons apprendre à organiser nos applications de manière beaucoup plus structurée et puissante grâce à un framework : Vue.js.