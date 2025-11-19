# Module 4 : Construire des Applications Modernes avec Vue.js

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Comprendre le concept de **réactivité** et pourquoi il est au cœur des frameworks modernes.
- Initialiser et développer une application Vue.js en utilisant l'écosystème moderne (Vite, NPM).
- Construire des interfaces utilisateur complexes en les décomposant en **composants** réutilisables.
- Gérer la communication entre les composants (props et emits).
- Gérer l'état de l'application de manière centralisée avec **Pinia**.
- Créer une **Single Page Application (SPA)** avec un routage côté client grâce à **Vue Router**.
- Intégrer des données provenant d'API externes dans une application Vue.

## 2. Prérequis

- Avoir complété les **Modules 1 (HTML), 2 (CSS) et 3 (JavaScript)**.
- Maîtrise des concepts JS : variables, fonctions, objets, tableaux (et leurs méthodes comme `map`, `filter`), et la syntaxe ES6+ (`let/const`, fonctions fléchées).
- Compréhension de la programmation asynchrone (`async/await`, `Promise`, `fetch`).
- Avoir **Node.js** et **NPM** installés sur votre machine (cela nous permettra d'utiliser des outils de build modernes comme Vite).

## 3. Résumé du Concept (Qu'est-ce que Vue.js ?)

Imaginez que vous deviez manuellement mettre à jour chaque information sur un tableau de bord à chaque fois qu'une nouvelle donnée arrive. C'est ce que nous faisions avec le JavaScript "vanilla" : sélectionner un élément, puis changer son `textContent`. C'est fastidieux et source d'erreurs.

Vue.js est un **framework progressif** qui automatise ce processus. Son concept clé est la **réactivité**. Vous déclarez une variable (un "état") et vous la liez à votre HTML. Ensuite, dès que vous modifiez cette variable dans votre code JavaScript, Vue.js se charge de mettre à jour **automatiquement** et efficacement le HTML correspondant.

Vous ne donnez plus d'ordres impératifs ("change ce texte"), mais vous adoptez une approche **déclarative** ("voici à quoi doit ressembler mon HTML en fonction de cette donnée"). Vue.js s'occupe du "comment". Il permet de construire des applications complexes en les découpant en petits morceaux logiques et autonomes appelés **composants**.

## 4. Plan d’Apprentissage

*   **Chapitre 1 : Premier Pas avec Vue et Vite**
    *   Installer une application Vue avec Vite
    *   La structure d'un projet Vue (Single File Components)
    *   La réactivité : `ref` et la syntaxe des templates `{{ }}`
*   **Chapitre 2 : Les Directives Essentielles**
    *   Rendu conditionnel avec `v-if`, `v-else`
    *   Rendu de listes avec `v-for`
    *   Liaison d'attributs avec `v-bind` (ou `:`)
*   **Chapitre 3 : Événements et Formulaires**
    *   Gérer les événements utilisateur avec `v-on` (ou `@`)
    *   La liaison bidirectionnelle avec `v-model`
    *   Les `computed properties` pour des données dérivées
*   **Chapitre 4 : L'Architecture par Composants**
    *   Créer et utiliser un composant
    *   Passer des données d'un parent à un enfant avec les `props`
    *   Remonter des informations d'un enfant à un parent avec les `emits`
*   **Chapitre 5 : Gestion d'État avec Pinia**
    *   Le problème du "prop drilling"
    *   Créer un "store" pour centraliser l'état
    *   Accéder et modifier l'état depuis n'importe quel composant
*   **Chapitre 6 : Routage avec Vue Router**
    *   Mettre en place le routeur
    *   Définir des routes et naviguer entre les pages
    *   Gérer les paramètres dynamiques dans les routes (ex: `/users/:id`)

## 5. Leçons

### Leçon 1 : Premier Pas avec Vue et Vite

On quitte le simple fichier `.html`. Un projet Vue moderne s'initialise via la ligne de commande et utilise un outil (Vite) pour compiler notre code et offrir un serveur de développement ultra-rapide. On découvre les Fichiers Monocomposants (`.vue`) qui regroupent le HTML (`<template>`), le JS (`<script>`) et le CSS (`<style>`) d'un composant.

- **Exemple de code simple (dans `App.vue`) :**
  ```vue
  <script setup>
  import { ref } from 'vue';

  // 'ref' rend la variable réactive
  const message = ref('Bonjour Vue !');
  </script>

  <template>
    <h1>{{ message }}</h1>
  </template>
  ```
- **Exemple de code appliqué (un compteur simple) :**
  ```vue
  <script setup>
  import { ref } from 'vue';
  
  const compteur = ref(0);
  </script>

  <template>
    <!-- Le contenu de h1 se mettra à jour automatiquement ! -->
    <h1>Compteur : {{ compteur }}</h1>
  </template>
  ```

### Leçon 2 : Les Directives Essentielles

Les directives sont des attributs spéciaux préfixés par `v-` qui appliquent des comportements réactifs au DOM. Elles sont notre principal outil pour manipuler la structure de la page.

- **Exemple de code simple :**
  ```vue
  <script setup>
  import { ref } from 'vue';
  const visible = ref(true);
  const fruits = ref(['Pomme', 'Banane', 'Fraise']);
  </script>

  <template>
    <p v-if="visible">Ce texte est visible.</p>
    <ul>
      <li v-for="fruit in fruits" :key="fruit">{{ fruit }}</li>
    </ul>
  </template>
  ```
- **Exemple de code appliqué (refactoriser notre To-Do List) :**
  ```vue
  <script setup>
  import { ref } from 'vue';
  const taches = ref([
    { id: 1, text: 'Apprendre Vue', done: true },
    { id: 2, text: 'Construire un projet', done: false }
  ]);
  </script>

  <template>
    <ul>
      <!-- On boucle sur le tableau de tâches -->
      <li v-for="tache in taches" :key="tache.id">
        {{ tache.text }}
        <!-- On affiche 'Fait' seulement si tache.done est true -->
        <span v-if="tache.done"> - Fait</span>
      </li>
    </ul>
  </template>
  ```

### Leçon 3 : Événements et Formulaires

`@click` (raccourci de `v-on:click`) remplace `addEventListener`. `v-model` est une directive magique qui synchronise la valeur d'un champ de formulaire avec une variable, dans les deux sens.

- **Exemple de code simple :**
  ```vue
  <script setup>
  import { ref } from 'vue';
  const message = ref('');
  </script>

  <template>
    <!-- v-model met à jour la variable 'message' à chaque frappe -->
    <input v-model="message" placeholder="Écrivez quelque chose">
    <p>Vous avez écrit : {{ message }}</p>
  </template>
  ```
- **Exemple de code appliqué (le formulaire d'ajout de la To-Do List) :**
  ```vue
  <script setup>
  // ... (taches de la leçon précédente)
  import { ref } from 'vue';
  const nouvelleTache = ref('');

  function ajouterTache() {
    if (nouvelleTache.value.trim() === '') return;
    taches.value.push({ id: Date.now(), text: nouvelleTache.value, done: false });
    nouvelleTache.value = ''; // On vide le champ
  }
  </script>

  <template>
    <!-- On écoute l'événement 'submit' et on appelle la fonction 'ajouterTache' -->
    <form @submit.prevent="ajouterTache">
      <input v-model="nouvelleTache" placeholder="Ajouter une tâche">
      <button type="submit">Ajouter</button>
    </form>
    <!-- ... (liste des tâches) -->
  </template>
  ```

### Leçon 4 : L'Architecture par Composants

On arrête d'écrire tout notre code dans `App.vue`. On décompose l'interface en petits composants logiques et réutilisables, comme des briques de Lego.

- **Exemple de code simple :**

  *Fichier `BoutonSimple.vue`*
  ```vue
  <script setup>
  // On définit les 'props' que le composant peut recevoir
  defineProps({
    texte: String
  });
  </script>
  <template>
    <button>{{ texte }}</button>
  </template>
  ```

  *Fichier `App.vue`*
  ```vue
  <script setup>
  import BoutonSimple from './BoutonSimple.vue';
  </script>
  <template>
    <!-- On utilise le composant et on lui passe la prop 'texte' -->
    <BoutonSimple texte="Cliquez ici" />
    <BoutonSimple texte="Annuler" />
  </template>
  ```
- **Exemple de code appliqué (un composant pour une tâche de la To-Do List) :**

  *Fichier `TodoItem.vue`*
  ```vue
  <script setup>
  defineProps({
    tache: Object // On attend un objet 'tache' en prop
  });
  const emit = defineEmits(['supprimer']); // On déclare l'événement qu'on peut émettre
  </script>

  <template>
    <li>
      {{ tache.text }}
      <button @click="emit('supprimer', tache.id)">X</button>
    </li>
  </template>
  ```

  *Fichier `App.vue`*
  ```vue
  <!-- Dans le <template> -->
  <ul>
    <TodoItem 
      v-for="tache in taches" 
      :key="tache.id" 
      :tache="tache" 
      @supprimer="gererSuppression"
    />
  </ul>
  ```

### Leçon 5 : Gestion d'État avec Pinia

Quand l'application grandit, passer des `props` et des `emits` sur plusieurs niveaux devient un cauchemar. Pinia offre un "magasin" global où l'on peut stocker l'état (données, panier, utilisateur connecté...) et y accéder depuis n'importe quel composant.

- **Exemple de code simple :**

  *Fichier `stores/counter.js`*
  ```javascript
  import { defineStore } from 'pinia';
  
  export const useCounterStore = defineStore('counter', {
    state: () => ({ count: 0 }),
    actions: {
      increment() {
        this.count++;
      },
    },
  });
  ```

  *Fichier `MonComposant.vue`*
  ```vue
  <script setup>
  import { useCounterStore } from '@/stores/counter';
  const counterStore = useCounterStore();
  </script>

  <template>
    <!-- On accède directement à l'état du store -->
    <p>Compteur : {{ counterStore.count }}</p>
    <!-- On appelle une action du store -->
    <button @click="counterStore.increment()">Incrémenter</button>
  </template>
  ```
- **Exemple de code appliqué (gérer les tâches de la To-Do List avec Pinia) :**

  *Fichier `stores/todo.js`*
  ```javascript
  // ...
  export const useTodoStore = defineStore('todo', {
    state: () => ({
      taches: [{ id: 1, text: 'Utiliser Pinia', done: false }]
    }),
    actions: {
      ajouterTache(texte) {
        this.taches.push({ id: Date.now(), text: texte, done: false });
      }
    }
  });
  ```

### Leçon 6 : Routage avec Vue Router

Pour créer une application qui a plusieurs "pages" (`/`, `/a-propos`, `/contact`) sans recharger le navigateur à chaque fois, on utilise Vue Router. Il intercepte les changements d'URL et affiche le composant correspondant.

- **Exemple de code simple :**

  *Fichier `router/index.js`*
  ```javascript
  // ...
  const router = createRouter({
    history: createWebHistory(),
    routes: [
      { path: '/', component: HomePage },
      { path: '/about', component: AboutPage }
    ]
  });
  ```

  *Fichier `App.vue`*
  ```vue
  <template>
    <nav>
      <RouterLink to="/">Accueil</RouterLink>
      <RouterLink to="/about">À Propos</RouterLink>
    </nav>
    <!-- Vue Router affichera le composant de la page active ici -->
    <RouterView />
  </template>
  ```
- **Exemple de code appliqué (un blog avec liste d'articles et page de détail) :**

  *Fichier `router/index.js`*
  ```javascript
  // ...
  const routes = [
    { path: '/', component: ArticleListPage },
    // :id est un paramètre dynamique
    { path: '/article/:id', component: ArticleDetailPage }
  ];
  ```

## 6. Exercices Pratiques

- **Niveau Débutant : Onglets Interactifs**
  Créez une interface à onglets simple. Vous aurez 3 boutons ("Onglet 1", "Onglet 2", "Onglet 3") et une zone de contenu. En utilisant une variable d'état et `v-if`/`v-else-if`, affichez un contenu différent lorsque l'utilisateur clique sur chaque bouton.

- **Niveau Intermédiaire : Formulaire de Carte de Crédit**
  Créez un formulaire qui simule la saisie d'une carte de crédit. Utilisez `v-model` pour lier les champs (numéro de carte, nom, date d'expiration, CVV). Affichez une prévisualisation "live" de la carte avec les données saisies par l'utilisateur. Utilisez des `computed properties` pour formater le numéro de carte (ex: '4444 4444...').

- **Niveau Avancé : Composant de Notation par Étoiles**
  Créez un composant réutilisable `<StarRating />`. Il doit accepter une `prop` pour la note actuelle. Il doit afficher 5 étoiles. Quand l'utilisateur clique sur une étoile, le composant doit `emit` un événement avec la nouvelle note. Utilisez ce composant dans `App.vue` pour noter un produit.

## 7. Mini-projet Guidé : Un Panier d'Achat Simple

On va créer une mini-boutique qui liste des produits et permet de les ajouter à un panier.

1.  **Étape 1 : Le Composant Produit**
    Créez un composant `ProductCard.vue`. Il prendra un objet `product` en `prop` (contenant nom, prix, image) et l'affichera. Il aura aussi un bouton "Ajouter au panier" qui `emit` un événement `addToCart`.

2.  **Étape 2 : La Liste des Produits**
    Dans `App.vue`, créez un tableau de produits. Utilisez `v-for` pour afficher plusieurs instances de votre `ProductCard` et écoutez l'événement `@addToCart`.

3.  **Étape 3 : Le Store du Panier (Pinia)**
    Créez un store Pinia `cart.js`. Il aura un `state` (un tableau `items`), un `getter` (pour calculer le total du panier), et une `action` (`addProduct`) pour ajouter un produit au tableau `items`.

4.  **Étape 4 : Connecter les Composants au Store**
    Quand l'événement `@addToCart` est reçu dans `App.vue`, appelez l'action `addProduct` du store.

5.  **Étape 5 : Le Composant Panier**
    Créez un composant `ShoppingCart.vue`. Il importera le store `cart.js` et affichera la liste des produits du panier ainsi que le total calculé par le `getter`. Affichez ce composant dans `App.vue`.

## 8. Projet Final Non Guidé : Un Explorateur de Films

Créez une SPA (Single Page Application) qui permet aux utilisateurs de rechercher des films et de voir leurs détails.

**Livrables :**
1.  Un dépôt GitHub contenant votre projet Vue complet.
2.  L'application déployée en ligne (sur Netlify, Vercel ou GitHub Pages).

**Fonctionnalités requises :**
- **Architecture :** L'application doit utiliser `Vite`, les `Single File Components`, `Pinia` et `Vue Router`.
- **API :** Utilisez une API de films gratuite comme [The Movie Database (TMDb)](https://www.themoviedb.org/documentation/api) (inscription et clé API gratuites).
- **Pages (Routes) :**
  - Une page d'accueil (`/`) avec un champ de recherche.
  - Une page de résultats (`/search?query=...`) qui affiche les films correspondant à la recherche sous forme de grille de cartes.
  - Une page de détail de film (`/movie/:id`) qui affiche des informations complètes sur un film (poster, synopsis, note, acteurs...).
- **Gestion d'état (Pinia) :** Utilisez un store pour gérer les résultats de recherche, l'état de chargement, et éventuellement une liste de "favoris".
- **Expérience Utilisateur :**
  - Affichez un indicateur de chargement ("spinner") pendant les appels API.
  - Le design doit être responsive et agréable.
  - La gestion des erreurs (ex: film non trouvé, erreur API) doit être implémentée.

## 9. Critères d'Évaluation

- **Architecture Vue :** L'application est-elle bien découpée en composants logiques et réutilisables ? Les `props` et `emits` sont-ils utilisés correctement ?
- **Gestion de l'état :** Pinia est-il utilisé à bon escient pour l'état global ? L'état local est-il géré dans les composants quand c'est pertinent ?
- **Routage :** Les routes, y compris les routes dynamiques, fonctionnent-elles correctement ?
- **Interaction avec l'API :** Les appels `fetch` sont-ils bien gérés (états de chargement/erreur) et intégrés dans les actions Pinia ?
- **Qualité du code :** Le code est-il lisible, DRY (Don't Repeat Yourself) et suit-il les conventions de Vue ?
- **Fonctionnalité et UX :** L'application est-elle fonctionnelle, intuitive et sans bugs majeurs ?

## 10. Ressources Complémentaires Fiables

- **Documentation Officielle de Vue.js :** Incroyablement bien écrite, interactive et considérée comme l'une des meilleures documentations de l'écosystème JS. C'est votre ressource n°1.
  - [vuejs.org](https://vuejs.org/)
- **Documentation de Pinia :** La référence pour la gestion d'état.
  - [pinia.vuejs.org](https://pinia.vuejs.org/)
- **Documentation de Vue Router :** La référence pour le routage.
  - [router.vuejs.org](https://router.vuejs.org/)
- **Vue Mastery :** Des tutoriels vidéo de très haute qualité (certains gratuits, d'autres payants).
  - [vuemastery.com](https://www.vuemastery.com/)
- **Vue Land (Discord) :** Le serveur Discord officiel de Vue.js. Une communauté très active pour poser des questions.
  - Lien accessible depuis le site de Vue.js.