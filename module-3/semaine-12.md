## Semaine 12 : State Management et API

### J1 : Le Problème de l'État Partagé et la Solution Pinia

**Objectif(s) du Jour :**
- Comprendre le problème du "prop drilling" dans une application à plusieurs niveaux.
- Découvrir le concept de gestionnaire d'état centralisé.
- Créer son premier "store" Pinia.
- Accéder à l'état (state) du store depuis n'importe quel composant.

**Notion Clé : Le Magasin Central**
Imaginez que vous construisiez une ville avec des Legos. Plusieurs maisons (composants) ont besoin d'une information commune, par exemple "Quelle heure est-il ?". Sans gestionnaire d'état, la mairie (le composant racine) doit passer l'heure à la maison 1, qui la passe à l'appartement A, qui la passe à la chambre... C'est le **prop drilling**. C'est fastidieux et fragile.
**Pinia**, c'est un **magasin central** au milieu de la ville. L'heure officielle y est affichée sur un grand panneau (le `state`). N'importe quelle maison (composant), peu importe où elle se trouve, peut simplement regarder vers le magasin central pour connaître l'heure. C'est simple, direct et efficace.

---

#### Leçon

##### 1. Le Problème : Le "Prop Drilling"

Quand un composant a besoin d'une donnée détenue par un grand-parent (ou plus haut), il faut la faire passer à travers tous les composants intermédiaires via des `props`, même s'ils n'en ont pas besoin. C'est lourd et difficile à maintenir.

##### 2. La Solution : Pinia

Pinia est le gestionnaire d'état officiel pour Vue 3. Il propose :
- Un **store** : un conteneur qui détient un `state` réactif, des `actions` pour le modifier, et des `getters` pour calculer des données dérivées.
- Chaque store est un module, ce qui rend le code organisé.

##### 3. Mettre en Place Pinia

- **Exemple de Code (Installation et création d'un store) :**
  ```html
  <!DOCTYPE html>
  <html>
  <head>
    <title>Mon App avec Pinia</title>
    <script src="https://unpkg.com/vue@3"></script>
    <!-- On importe Pinia -->
    <script src="https://unpkg.com/pinia"></script>
  </head>
  <body>
    <div id="app">
      <my-component></my-component>
      <other-component></other-component>
    </div>

    <script>
      const { createApp, defineComponent } = Vue;
      const { createPinia, defineStore } = Pinia;

      // 1. Définir un store
      const useCounterStore = defineStore('counter', {
        // L'état initial du store
        state: () => ({
          count: 0,
          name: 'Mon Compteur'
        })
      });

      // 2. Créer l'instance de Pinia
      const pinia = createPinia();
      const app = createApp({});

      // 3. Définir des composants qui utiliseront le store
      app.component('my-component', defineComponent({
        template: `<div>Compteur : {{ counterStore.count }}</div>`,
        setup() {
          const counterStore = useCounterStore();
          return { counterStore };
        }
      }));
      app.component('other-component', defineComponent({
        template: `<div>Nom du compteur : {{ counterStore.name }}</div>`,
        setup() {
          const counterStore = useCounterStore();
          return { counterStore };
        }
      }));

      // 4. Utiliser Pinia dans l'app et monter
      app.use(pinia);
      app.mount('#app');
    </script>
  </body>
  </html>
  ```

---

#### Mise en Pratique

1.  Créez un nouveau fichier `jour1.html`.
2.  Suivez l'exemple ci-dessus pour mettre en place Pinia.
3.  Créez un store `userStore` avec un `state` contenant un objet `user: { name: 'Alice', isLoggedIn: false }`.
4.  Créez un composant `<user-profile>` qui affiche "Bienvenue, `user.name` !" en lisant les données du store.
5.  Créez un autre composant `<navigation-bar>` qui affiche "Connexion" ou "Déconnexion" en fonction de la valeur de `user.isLoggedIn` dans le store.

#### Mini-Exercice du Jour

Dans la console de votre navigateur, essayez de modifier l'état directement : `userStore.user.isLoggedIn = true`. Vous devriez voir votre barre de navigation se mettre à jour instantanément.

#### Synthèse

Vous avez compris le "pourquoi" et le "comment" d'un état centralisé. N'importe quel composant peut maintenant lire l'état global. Mais comment le modifier de manière propre et sécurisée ? C'est le rôle des **actions**, que nous verrons demain.

---

### J2 : Modifier l'État Centralisé - Les Actions

**Objectif(s) du Jour :**
- Comprendre que les `actions` sont le moyen privilégié pour modifier l'état.
- Définir et utiliser des `actions` dans un store Pinia.
- Passer des arguments aux actions.

**Notion Clé : Le Manager du Magasin**
Dans notre magasin central, les clients (composants) ne vont pas ré-étiqueter les prix eux-mêmes. Ce serait le chaos. Pour modifier quelque chose, ils doivent s'adresser au **manager** du magasin (les `actions`). Ils lui donnent une instruction : "Augmente le stock de pommes de 10 unités" (`increment(10)`). Le manager est le seul habilité à effectuer la modification sur l'inventaire (le `state`). Cela garantit que toutes les modifications sont faites de manière contrôlée et prévisible.

---

#### Leçon

##### 1. Définir les Actions

Les `actions` sont des méthodes définies dans le store. Elles reçoivent l'accès à l'état via `this`.

```javascript
const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 0
  }),
  // Les actions sont des méthodes
  actions: {
    increment() {
      // 'this' fait référence à l'instance du store
      this.count++;
    },
    incrementBy(amount) {
      this.count += amount;
    }
  }
});
```

##### 2. Appeler les Actions depuis un Composant

On appelle une action comme n'importe quelle autre méthode de l'objet store.

- **Exemple de Code (Un compteur avec des actions) :**
  ```html
  <div id="app">
    <p>Compteur : {{ counterStore.count }}</p>
    <!-- On appelle les actions au clic -->
    <button @click="counterStore.increment()">+1</button>
    <button @click="counterStore.incrementBy(5)">+5</button>
  </div>

  <script>
    // ...
    app.component('my-app', defineComponent({
      template: `...`, // Template ci-dessus
      setup() {
        const counterStore = useCounterStore();
        return { counterStore };
      }
    }));
    // ...
  </script>
  ```

---

#### Mise en Pratique

1.  Reprenez le fichier `jour1.html` et renommez-le `jour2.html`.
2.  Dans votre `userStore`, ajoutez deux actions : `login()` qui passe `isLoggedIn` à `true`, et `logout()` qui le passe à `false`.
3.  Dans votre composant `<navigation-bar>`, ajoutez deux boutons. Le bouton "Connexion" doit appeler l'action `login`, et le bouton "Déconnexion" doit appeler l'action `logout`.
4.  Testez : cliquer sur les boutons doit changer l'état et mettre à jour l'affichage.

#### Mini-Exercice du Jour

Ajoutez une action `changeName(newName)` à votre `userStore`. Créez un petit formulaire dans un composant qui permet de changer le nom de l'utilisateur en appelant cette action.

#### Synthèse

Vous savez maintenant comment lire et modifier l'état de manière propre. Mais que faire si vous avez besoin d'une donnée calculée à partir de l'état, comme le nombre de tâches restantes dans une to-do list ? C'est le rôle des **getters**, que nous découvrirons demain.

---

### J3 : Données Dérivées et Performantes - Les Getters

**Objectif(s) du Jour :**
- Comprendre le rôle des `getters` en tant que propriétés calculées du store.
- Définir et utiliser des `getters` simples.
- Créer des `getters` qui acceptent des arguments.

**Notion Clé : Le Rapport d'Inventaire Automatique**
Dans notre magasin central, le manager ne recalcule pas la valeur totale du stock chaque fois qu'un client la demande. Il dispose d'un **rapport d'inventaire** (un `getter`) qui est calculé une seule fois. Ce rapport est mis en cache. Tant que l'inventaire (`state`) ne change pas, le manager donne toujours le même rapport. Si un article est ajouté, le rapport se met à jour automatiquement, mais une seule fois. C'est exactement comme les `computed properties`, mais au niveau du store.

---

#### Leçon

##### 1. Définir un Getter

Les `getters` sont définis dans la propriété `getters` du store. Ils reçoivent l'état (`state`) comme premier argument.

```javascript
const useCounterStore = defineStore('counter', {
  state: () => ({
    count: 5
  }),
  getters: {
    // Un getter simple, comme une computed property
    doubleCount: (state) => state.count * 2,
    // On peut aussi utiliser 'this'
    doubleCountPlusOne() {
      return this.doubleCount + 1;
    }
  }
});
```

##### 2. Utiliser un Getter

On accède à un getter comme à une propriété de l'état. Il est réactif.

- **Exemple de Code :**
  ```html
  <div id="app">
      <p>Compteur : {{ counterStore.count }}</p>
      <!-- On accède au getter comme une simple propriété -->
      <p>Double du compteur : {{ counterStore.doubleCount }}</p>
  </div>
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour3.html`.
2.  Créez un store `todoStore` avec un état contenant un tableau `todos` (avec des objets `{id, text, completed}`).
3.  Créez un `getter` nommé `completedTodos` qui retourne un tableau contenant uniquement les tâches terminées.
4.  Créez un autre `getter` nommé `uncompletedCount` qui retourne le nombre de tâches non terminées.
5.  Dans un composant, affichez le nombre de tâches non terminées et la liste des tâches terminées en utilisant ces getters.

#### Mini-Exercice du Jour

Créez un getter `getTodoById` qui retourne une fonction. Cette fonction prendra un `id` en argument et retournera la tâche correspondante dans le tableau. `(state) => (id) => state.todos.find(t => t.id === id)`. C'est une technique avancée pour créer des getters dynamiques.

#### Synthèse

Vous maîtrisez maintenant les trois piliers de Pinia : `state`, `actions`, et `getters`. Vous êtes prêt à utiliser cette architecture pour interagir avec le monde extérieur. Demain, nous allons connecter nos actions à une véritable API pour charger des données distantes.

---

### J4 : Connecter le Store au Monde - API et Axios

**Objectif(s) du Jour :**
- Découvrir Axios comme une alternative populaire à `fetch`.
- Placer la logique d'appel API à l'intérieur des `actions` d'un store Pinia.
- Gérer l'état de chargement (loading) pendant l'appel API.

**Notion Clé : Le Service des Commandes Extérieures**
Le manager de notre magasin (`action`) a parfois besoin de produits qui ne sont pas en stock. Il doit contacter un fournisseur extérieur (une **API**). Il passe la commande (la requête **Axios/fetch**). Pendant le temps de la livraison, il met une pancarte "Livraison en cours..." (un état `loading: true`). Lorsque les produits arrivent (la réponse de l'API), il les range sur les étagères (met à jour le `state`) et retire la pancarte (`loading: false`). Toute la logique de communication externe est gérée par le manager, pas par les clients.

---

#### Leçon

##### 1. Axios, une librairie pour les requêtes HTTP

Axios simplifie les requêtes HTTP. Il parse automatiquement le JSON et gère mieux les erreurs.
- **Installation :** On l'importe via un CDN pour nos exemples.
- **Utilisation :** `axios.get('https://api.example.com/data')` retourne une promesse.

##### 2. Actions Asynchrones

Les `actions` peuvent être des fonctions `async`. C'est l'endroit idéal pour effectuer des appels API.

- **Exemple de Code (Charger des utilisateurs) :**
  ```javascript
  const useUserStore = defineStore('users', {
    state: () => ({
      users: [],
      loading: false,
      error: null
    }),
    actions: {
      // Une action asynchrone
      async fetchUsers() {
        this.loading = true;
        this.error = null;
        try {
          // On fait l'appel API
          const response = await axios.get('https://jsonplaceholder.typicode.com/users');
          // On met à jour l'état avec les données reçues
          this.users = response.data;
        } catch (err) {
          // On gère les erreurs
          this.error = 'Erreur lors du chargement des utilisateurs.';
          console.error(err);
        } finally {
          // Quoi qu'il arrive, on arrête de charger
          this.loading = false;
        }
      }
    }
  });
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour4.html` et importez Vue, Pinia et Axios.
2.  Créez un `userStore` comme dans l'exemple ci-dessus.
3.  Créez un composant qui affiche "Chargement..." si `userStore.loading` est `true`.
4.  Une fois le chargement terminé, il doit afficher la liste des noms d'utilisateurs contenus dans `userStore.users`.
5.  Le composant doit avoir un bouton "Charger les utilisateurs" qui appelle l'action `fetchUsers`.

#### Mini-Exercice du Jour

Ajoutez la gestion d'erreur. Si `userStore.error` n'est pas `null`, affichez le message d'erreur à l'utilisateur. Pour tester, modifiez l'URL de l'API pour qu'elle soit incorrecte.

#### Synthèse

Vous avez connecté votre état local au monde extérieur. C'est l'architecture la plus courante et la plus robuste pour les applications Vue modernes : les composants déclenchent des actions, les actions communiquent avec l'API, et l'état est mis à jour, ce qui rend l'interface réactive. Vous êtes prêt pour le projet final !

---

### J5 : Projet de la Semaine - Frontend de Blog avec API

**Objectif(s) du Jour :**
- Intégrer toutes les notions de la semaine (Pinia, Axios) avec celles de la semaine précédente (Vue Router).
- Construire une application SPA complète et dynamique qui consomme une API REST.
- Mettre en place une architecture frontend professionnelle et scalable.

**Notion Clé : L'Exposition d'Art Complète**
Aujourd'hui, vous êtes le curateur d'une exposition d'art. Vous avez déjà le plan du musée (le **routeur** avec ses différentes salles). Vous avez le catalogue central de toutes les œuvres (le **store Pinia**). Votre mission est de remplir ce catalogue en commandant les œuvres à des artistes du monde entier (l'**API JSONPlaceholder**) et de vous assurer que chaque salle du musée affiche les bonnes œuvres.

---

#### PROJET DE LA SEMAINE : Frontend de Blog avec API

Votre mission est de construire une application de type blog qui récupère ses données depuis l'API publique [JSONPlaceholder](https://jsonplaceholder.typicode.com/).

**Structure et Fonctionnalités Obligatoires :**

1.  **Mise en Place :**
    - Un projet utilisant Vue 3, Vue Router, Pinia et Axios (vous pouvez tout importer via CDN dans un seul fichier `index.html`).

2.  **Store Pinia (`postStore`) :**
    - `state`:
      - `posts`: un tableau pour stocker la liste de tous les articles.
      - `currentPost`: un objet pour stocker l'article actuellement consulté.
      - `loading`: un booléen pour l'état de chargement.
    - `actions`:
      - `fetchAllPosts()`: une action `async` qui fait un `GET` sur `https://jsonplaceholder.typicode.com/posts` et remplit le tableau `posts`.
      - `fetchPostById(id)`: une action `async` qui fait un `GET` sur `https://jsonplaceholder.typicode.com/posts/{id}` et remplit `currentPost`.

3.  **Routage (Vue Router) :**
    - `/` (ou `/posts`): La page qui liste tous les articles du blog.
    - `/posts/:id`: La page de détail d'un article spécifique.

4.  **Composants & Logique :**
    - **`PostListPage.vue` (pour la route `/`) :**
      - Doit afficher un indicateur de chargement pendant que les données sont récupérées.
      - Une fois les données chargées, doit afficher une liste de titres d'articles.
      - Chaque titre doit être un `<router-link>` pointant vers la page de détail de l'article (ex: `/posts/1`).
      - L'action `fetchAllPosts` doit être appelée quand le composant est monté (dans le hook `onMounted` du `setup`).
    - **`PostDetailPage.vue` (pour la route `/posts/:id`) :**
      - Doit récupérer l'ID de l'URL grâce à `$route.params.id`.
      - Doit appeler l'action `fetchPostById(id)` avec cet ID.
      - Doit afficher un indicateur de chargement.
      - Une fois les données chargées, doit afficher le titre et le corps (`body`) de l'article contenu dans `currentPost`.

**Livrable :** Un unique fichier `index.html` (ou un projet plus structuré si vous utilisez un outil de build) déposé sur votre dépôt GitHub. L'application doit être entièrement fonctionnelle : charger la liste des articles, permettre de cliquer sur un titre, charger la page de détail correspondante et afficher son contenu.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez construit une application SPA complète, dynamique et bien architecturée. Vous avez non seulement terminé le module Vue.js, mais vous avez également assemblé toutes les pièces du puzzle du développement frontend moderne : composants, routage, gestion d'état centralisée et communication avec une API. Vous disposez maintenant d'une base extrêmement solide pour construire des applications web interactives et complexes.