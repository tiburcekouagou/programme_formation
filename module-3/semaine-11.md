## Semaine 11 : Le Routage avec Vue Router

### J1 : Naviguer sans Recharger : SPA et Vue Router

**Objectif(s) du Jour :**
- Comprendre ce qu'est une SPA (Single-Page Application) et ses avantages.
- Découvrir le rôle de Vue Router en tant que routeur côté client.
- Installer Vue Router et le configurer dans une application Vue.
- Créer ses premières routes et les composants de page associés.

**Notion Clé : Le Guide Touristique de la Ville**
Jusqu'à présent, pour "visiter" une nouvelle page de votre site, vous deviez prendre un avion, quitter la ville et atterrir dans une nouvelle (rechargement complet de la page). C'est lent et l'expérience est saccadée.
Une **SPA**, c'est comme visiter une grande ville où tous les lieux d'intérêt sont déjà là. **Vue Router** est votre guide touristique personnel. Quand vous voulez aller à la "Place de l'Accueil" (`/`) ou au "Musée À Propos" (`/about`), le guide ne vous fait pas quitter la ville. Il vous montre simplement le bon chemin et change votre vue, instantanément, sans temps de chargement. L'URL dans la barre d'adresse change pour que vous sachiez où vous êtes, mais vous n'avez jamais quitté l'application.

---

#### Leçon

##### 1. Qu'est-ce qu'une SPA (Single-Page Application) ?

Une SPA est une application web qui charge une seule page HTML, puis met à jour dynamiquement son contenu au fur et à mesure que l'utilisateur interagit avec elle, au lieu de charger de nouvelles pages entières depuis le serveur.

##### 2. Mise en Place de Vue Router

Vue Router est la librairie officielle de routage pour Vue.js. On l'ajoute à notre projet.

- **Exemple de Code (Installation et Configuration) :**
  ```html
  <!DOCTYPE html>
  <html>
  <head>
    <title>Mon App avec Vue Router</title>
    <!-- 1. Importer Vue et Vue Router -->
    <script src="https://unpkg.com/vue@3"></script>
    <script src="https://unpkg.com/vue-router@4"></script>
  </head>
  <body>
    <div id="app">
      <!-- 4. Les composants de page seront rendus ici -->
      <router-view></router-view>
    </div>

    <script>
      const { createApp } = Vue;
      const { createRouter, createWebHashHistory } = VueRouter;

      // a. Définir les composants pour chaque "page"
      const HomePage = { template: '<div>Page d\'accueil</div>' };
      const AboutPage = { template: '<div>Page À Propos</div>' };

      // b. Définir les routes (le mapping URL -> Composant)
      const routes = [
        { path: '/', component: HomePage },
        { path: '/about', component: AboutPage },
      ];

      // c. Créer l'instance du routeur
      const router = createRouter({
        history: createWebHashHistory(), // Gère l'historique de navigation
        routes, // Raccourci pour 'routes: routes'
      });

      // 2. Créer l'application Vue
      const app = createApp({});
      // 3. Dire à l'application Vue d'utiliser le routeur
      app.use(router);
      app.mount('#app');
    </script>
  </body>
  </html>
  ```
- **`<router-view>` :** C'est le conteneur où Vue Router affichera le composant correspondant à l'URL actuelle.

---

#### Mise en Pratique

1.  Créez un nouveau fichier `jour1.html`.
2.  Suivez l'exemple ci-dessus pour mettre en place Vue Router.
3.  Créez trois composants de page simples : `HomePage`, `AboutPage`, et `ContactPage`.
4.  Définissez les routes correspondantes (`/`, `/about`, `/contact`).
5.  Testez en changeant manuellement l'URL dans votre navigateur (ex: `file:///.../jour1.html#/` puis `file:///.../jour1.html#/about`). Vous devriez voir le contenu changer sans que la page ne se recharge.

#### Mini-Exercice du Jour

Ajoutez une route `/404` avec un composant `NotFoundPage` qui affiche "404 - Page non trouvée". Essayez d'accéder à une URL qui n'existe pas, comme `#/produits`. Pour l'instant, rien ne se passe. Nous verrons demain comment gérer les routes inexistantes.

#### Synthèse

Vous avez construit le squelette d'une application multi-vues. Vous comprenez maintenant comment Vue Router intercepte les changements d'URL pour afficher différents composants. Demain, nous allons rendre cette navigation cliquable pour l'utilisateur avec le composant `<router-link>`.

---

### J2 : Navigation Utilisateur - `<router-link>`

**Objectif(s) du Jour :**
- Créer des liens de navigation cliquables avec `<router-link>`.
- Comprendre pourquoi on utilise `<router-link>` au lieu d'une balise `<a>` classique.
- Mettre en évidence le lien actif pour améliorer l'expérience utilisateur.

**Notion Clé : Le Portillon de Métro Intelligent**
- Une balise `<a href="/about">` classique, c'est comme **sortir de la station de métro** pour reprendre un taxi. Vous quittez l'application, ce qui provoque un rechargement complet de la page. C'est ce qu'on veut éviter.
- Le composant `<router-link to="/about">`, c'est le **portillon de correspondance** à l'intérieur de la station. Il dit au système de routage "amène-moi à la station 'About' sans me faire sortir". C'est une navigation interne, rapide et fluide. De plus, ce portillon est intelligent : il sait sur quel quai vous êtes et peut allumer une lumière pour vous indiquer "Vous êtes ici" (la classe active).

---

#### Leçon

##### 1. Le Composant `<router-link>`

C'est le composant fourni par Vue Router pour créer des liens de navigation.
- **Syntaxe :** `<router-link to="/chemin">Texte du lien</router-link>`
- Il sera rendu par défaut comme une balise `<a>` dans le DOM, mais avec le bon comportement de routage côté client.

##### 2. Mettre en Évidence le Lien Actif

Quand vous êtes sur la page `/about`, il est courant de vouloir que le lien "À Propos" dans la barre de navigation ait un style différent. Vue Router gère cela automatiquement.
- Il ajoute par défaut une classe CSS `router-link-active` au `<router-link>` qui correspond à la route actuelle.
- Il vous suffit de styliser cette classe en CSS.

- **Exemple de Code (Une barre de navigation) :**
  ```html
  <div id="app">
    <header>
      <nav>
        <router-link to="/">Accueil</router-link>
        <router-link to="/about">À Propos</router-link>
        <router-link to="/contact">Contact</router-link>
      </nav>
    </header>

    <!-- Zone d'affichage des pages -->
    <main>
      <router-view></router-view>
    </main>
  </div>

  <style>
    /* On cible la classe que Vue Router ajoute automatiquement */
    .router-link-active {
      color: red;
      font-weight: bold;
    }
  </style>

  <script>
    // ... (configuration du routeur comme hier)
  </script>
  ```

---

#### Mise en Pratique

1.  Reprenez le fichier `jour1.html` et renommez-le `jour2.html`.
2.  Juste au-dessus de la balise `<router-view>`, ajoutez une barre de navigation contenant des `<router-link>` pour chacune de vos routes (`/`, `/about`, `/contact`).
3.  Ajoutez le style CSS pour la classe `.router-link-active`.
4.  Testez dans votre navigateur : vous pouvez maintenant naviguer entre vos pages en cliquant sur les liens, sans aucun rechargement, et le lien actif est bien mis en évidence.

#### Mini-Exercice du Jour

Créez un composant réutilisable `<app-navigation>` qui contient la barre de navigation avec les `<router-link>`. Utilisez ce composant dans votre application principale pour garder votre template `app` propre.

#### Synthèse

Votre application est maintenant pleinement navigable pour l'utilisateur. La distinction entre `<router-link>` (navigation interne) et `<a>` (navigation externe) est fondamentale. Demain, nous allons aborder un cas très courant : comment créer des pages dynamiques, comme des fiches produit, en utilisant les paramètres de route.

---

### J3 : Pages Dynamiques - Paramètres de Route

**Objectif(s) du Jour :**
- Définir des routes dynamiques qui acceptent un paramètre (ex: `/users/:id`).
- Accéder aux paramètres de la route depuis le composant de page.
- Créer des liens vers ces routes dynamiques.

**Notion Clé : Les Numéros de Chambre d'Hôtel**
Votre application est un hôtel. Vous n'allez pas créer une page web distincte pour chaque chambre. Vous créez un seul "template de chambre" (`UserPage.vue`).
La route est définie comme `/chambres/:numero`. Le `:numero` est un **paramètre dynamique**.
- Quand un client demande la chambre `/chambres/101`, le routeur l'amène au template de chambre et lui dit : "Tu dois afficher les informations pour la chambre numéro **101**".
- S'il demande `/chambres/202`, c'est le même template, mais cette fois le routeur dit : "Affiche les infos pour la chambre **202**".
Le composant peut récupérer ce numéro (`$route.params.numero`) pour aller chercher les bonnes données à afficher.

---

#### Leçon

##### 1. Définir une Route Dynamique

Dans la configuration des routes, on utilise un deux-points (`:`) pour marquer un segment d'URL comme étant un paramètre.

```javascript
const routes = [
  // ...
  { path: '/users/:id', component: UserProfilePage }
];
```
Cette route correspondra à `/users/1`, `/users/alice`, `/users/123-abc`, etc.

##### 2. Accéder aux Paramètres

Dans le composant de la page (`UserProfilePage` dans notre exemple), Vue Router injecte l'objet `$route` qui contient les informations sur la route actuelle.
- On accède aux paramètres via `this.$route.params`.
- `this.$route.params.id` contiendra la valeur du paramètre `:id` de l'URL.

- **Exemple de Code (Page de profil utilisateur) :**
  ```html
  <!-- Dans l'application principale -->
  <router-link to="/users/1">Profil de Alice</router-link>
  <router-link to="/users/2">Profil de Bob</router-link>
  ```
  ```javascript
  const UserProfilePage = {
    template: `
      <div>
        <h2>Profil de l'utilisateur #{{ userId }}</h2>
        <!-- Dans un vrai projet, on utiliserait cet ID pour fetcher les données -->
      </div>
    `,
    computed: {
      userId() {
        // On accède au paramètre 'id' de l'URL
        return this.$route.params.id;
      }
    }
  };
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour3.html`.
2.  Mettez en place une application avec une page d'accueil (`/`) et une page de liste de produits (`/products`).
3.  La page `/products` doit afficher une liste de produits (ex: "Produit 1", "Produit 2") et chaque produit doit être un `<router-link>` pointant vers sa propre page de détail (ex: `/products/1`, `/products/2`).
4.  Créez le composant `ProductDetailPage` et la route dynamique `/products/:id`.
5.  Dans `ProductDetailPage`, affichez l'ID du produit récupéré depuis l'URL.

#### Mini-Exercice du Jour

Créez une page `NotFoundPage` et une route "catch-all" à la fin de votre tableau de routes : `{ path: '/:pathMatch(.*)*', component: NotFoundPage }`. Maintenant, si vous tapez une URL qui ne correspond à aucune autre route, l'utilisateur sera redirigé vers votre page 404.

#### Synthèse

Vous savez maintenant créer des structures d'URL complexes et dynamiques, une compétence essentielle pour la plupart des applications web (blogs, e-commerce, réseaux sociaux...). La dernière pièce du puzzle est de savoir comment déclencher une navigation non pas depuis un clic utilisateur, mais depuis votre code JavaScript.

---

### J4 : Navigation Programmatique

**Objectif(s) du Jour :**
- Comprendre les cas d'usage de la navigation programmatique.
- Utiliser `this.$router.push()` pour changer de page depuis une méthode.
- Découvrir d'autres méthodes comme `$router.replace()` et `$router.go()`.

**Notion Clé : Le Chauffeur de Taxi Télécommandé**
`<router-link>` c'est le client qui dit au chauffeur de taxi "emmène-moi à cette adresse". La **navigation programmatique**, c'est vous, depuis votre tour de contrôle, qui donnez un ordre directement au chauffeur de taxi (`this.$router`) : "Après avoir déposé ce colis (ex: formulaire soumis avec succès), va directement à la page de confirmation, sans attendre une nouvelle instruction du client".

---

#### Leçon

##### 1. Pourquoi la Navigation Programmatique ?

On l'utilise principalement après une action :
- Après une connexion réussie, rediriger vers le tableau de bord.
- Après la soumission d'un formulaire, rediriger vers une page de succès.
- Si une action échoue, rediriger vers une page d'erreur.

##### 2. L'objet `$router`

Alors que `$route` contient des informations sur la route *actuelle*, l'objet `$router` est l'instance du routeur lui-même et contient les méthodes pour *contrôler* la navigation.

- **`this.$router.push('/chemin')` :** Navigue vers une nouvelle URL. Ajoute une entrée dans l'historique de navigation (l'utilisateur peut faire "précédent").
  - Peut aussi prendre un objet : `this.$router.push({ path: '/users/1' })`.
- **`this.$router.replace('/chemin')` :** Similaire à `push`, mais remplace l'entrée actuelle dans l'historique. L'utilisateur ne peut pas revenir à la page précédente avec le bouton "précédent". Utile pour les pages de connexion.
- **`this.$router.go(n)` :** Navigue dans l'historique. `go(1)` = suivant, `go(-1)` = précédent.

- **Exemple de Code (Redirection après connexion) :**
  ```javascript
  const LoginPage = {
    template: `
      <div>
        <button @click="login">Se connecter</button>
      </div>
    `,
    methods: {
      login() {
        console.log('Connexion réussie ! Redirection...');
        // On redirige l'utilisateur vers son tableau de bord
        this.$router.push('/dashboard');
      }
    }
  };
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour4.html`.
2.  Créez une application avec une page de connexion (`/login`) et une page "Espace Privé" (`/private`).
3.  Sur la page de connexion, un bouton "Se connecter" doit appeler une méthode `login()`.
4.  Dans cette méthode, simulez une connexion et utilisez `this.$router.push('/private')` pour rediriger l'utilisateur.

#### Mini-Exercice du Jour

Créez une page de recherche avec un champ de saisie et un bouton. Quand l'utilisateur clique sur le bouton, au lieu de soumettre un formulaire, utilisez la navigation programmatique pour le rediriger vers une URL comme `/search?query=TEXTE_SAISI`. (Indice : `this.$router.push({ path: '/search', query: { q: this.searchTerm } })`).

#### Synthèse

Vous maîtrisez maintenant toutes les facettes de la navigation dans une SPA Vue.js : déclarative avec `<router-link>` et impérative avec `$router.push()`. Vous êtes prêt à construire le squelette complet d'une application multi-pages.

---

### J5 : Projet de la Semaine - Squelette d'Application Multi-Pages

**Objectif(s) du Jour :**
- Mettre en pratique l'ensemble des concepts de Vue Router.
- Structurer un projet de SPA de manière cohérente.
- Construire une base solide et réutilisable pour de futurs projets.

**Notion Clé : Le Plan de la Maison**
Aujourd'hui, vous n'allez pas meubler les pièces, mais vous allez construire les murs, les portes et les couloirs d'une maison complète. Votre projet sera le plan architectural d'une application web typique, avec un espace public (Accueil, Blog, Contact) et un espace "privé" simulé (Tableau de bord). Ce squelette est une fondation que vous pourrez réutiliser encore et encore.

---

#### PROJET DE LA SEMAINE : Squelette de Blog

Votre mission est de construire le squelette d'une application de blog, avec une navigation claire et des routes dynamiques.

**Structure et Fonctionnalités Obligatoires :**

1.  **Composants de Page :**
    - `HomePage` : Affiche un message de bienvenue.
    - `AboutPage` : Affiche du texte sur vous ou l'application.
    - `BlogPage` : Affiche une liste d'articles de blog. Chaque article doit être un `<router-link>` vers sa page de détail.
    - `PostDetailPage` : Le composant pour la route dynamique qui affiche le détail d'un article.
    - `NotFoundPage` : La page 404.

2.  **Configuration des Routes :**
    - `/` -> `HomePage`
    - `/about` -> `AboutPage`
    - `/blog` -> `BlogPage`
    - `/blog/:postId` -> `PostDetailPage` (route dynamique)
    - Une route "catch-all" qui redirige vers `NotFoundPage`.

3.  **Layout Principal :**
    - L'application doit avoir un composant `<app-navigation>` persistant en haut de la page, contenant les liens (`<router-link>`) vers "Accueil", "À Propos" et "Blog".
    - Le lien de la page active doit être visuellement distinct.
    - Sous la navigation, le `<router-view>` affichera le contenu de la page actuelle.

4.  **Logique des Composants :**
    - `BlogPage` : Ayez un petit tableau de données "en dur" pour simuler la liste des articles (ex: `[{id: 1, title: '...'}, {id: 2, ...}]`). Bouclez dessus pour générer les liens.
    - `PostDetailPage` : Doit récupérer l'ID de l'article depuis `$route.params.postId` et l'afficher (ex: "Détail de l'article #1").

5.  **(Bonus) Navigation Programmatique :**
    - Ajoutez une barre de recherche simple sur la `HomePage`. Quand l'utilisateur soumet un terme, redirigez-le de manière programmatique vers `/search?q=TERME_RECHERCHE` et affichez une page `SearchPage` (que vous devrez créer) qui indique "Résultats pour : TERME_RECHERCHE".

**Livrable :** Un unique fichier `index.html` contenant votre squelette d'application fonctionnel, déposé sur votre dépôt GitHub. La navigation doit être fluide et les routes dynamiques doivent fonctionner correctement.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez transformé une simple page Vue en une véritable application multi-vues, rapide et moderne. Vous savez maintenant structurer des applications complexes, gérer des URL propres et créer une expérience utilisateur fluide. La semaine prochaine, nous aborderons le dernier grand pilier de Vue : comment gérer un état partagé par de nombreux composants de manière propre et centralisée avec Pinia.