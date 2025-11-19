## Semaine 10 : L'Architecture par Composants

### J1 : Penser en Composants : Votre Premier Composant

**Objectif(s) du Jour :**
- Comprendre l'intérêt de l'architecture par composants (réutilisabilité, maintenabilité).
- Décomposer une interface complexe en une hiérarchie de composants.
- Créer et enregistrer un premier composant Vue global.
- Utiliser ce composant dans une application parente.

**Notion Clé : Les Briques de LEGO**
Jusqu'à présent, vous avez construit vos applications comme une sculpture taillée dans un seul bloc de bois. C'est long, difficile à modifier, et si vous voulez une deuxième sculpture, vous devez tout recommencer.
Un **composant**, c'est une brique de LEGO. C'est un morceau d'interface autonome, réutilisable, avec sa propre logique et son propre template. Pour construire une application, vous n'allez plus sculpter, vous allez **assembler des briques**. Vous voulez un autre bouton ? Prenez une autre brique "bouton". Vous voulez changer tous les en-têtes du site ? Modifiez juste la brique "en-tête", et tous les en-têtes se mettront à jour.

---

#### Leçon

##### 1. Décomposer une Interface

Regardez n'importe quel site web (Facebook, Twitter, ...). Vous pouvez le décomposer :
- Tout en haut, il y a un `<AppHeader>`.
- Sur le côté, il y a une `<Sidebar>`.
- Au centre, il y a une liste de `<PostItem>`.
- Chaque `<PostItem>` contient un `<UserAvatar>` et un `<LikeButton>`.
Voilà une architecture par composants !

##### 2. Créer et Enregistrer un Composant

On peut définir un composant en utilisant `app.component()`. C'est une brique réutilisable.

- **Exemple de Code (Un composant d'en-tête) :**
  ```html
  <div id="app">
      <!-- On utilise notre composant comme une balise HTML personnalisée -->
      <app-header></app-header>

      <main>
          <p>Ceci est le contenu principal de ma page.</p>
      </main>
  </div>

  <script>
    const { createApp } = Vue;
    const app = createApp({}); // On crée l'application parente

    // On définit notre composant "brique"
    // Le premier argument est le nom de la balise (convention: kebab-case)
    // Le second est l'objet de configuration du composant
    app.component('app-header', {
      // Le 'template' est le code HTML de notre composant
      template: `
        <header>
          <h1>Mon Super Site</h1>
          <p>Le meilleur site construit avec Vue</p>
        </header>
      `
    });

    app.mount('#app');
  </script>
  ```

---

#### Mise en Pratique

1.  Créez un nouveau fichier `jour1.html`.
2.  Mettez en place une application Vue de base.
3.  Créez un composant simple nommé `app-footer`.
4.  Le template de ce composant doit contenir une balise `<footer>` avec un message de copyright, par exemple : `<footer><p>&copy; 2023 - Mon App</p></footer>`.
5.  Utilisez votre composant `<app-footer>` dans le template de votre application principale.

#### Mini-Exercice du Jour

Créez un autre composant, `<welcome-message>`, qui affiche un `<div>` contenant un `<h2>` "Bienvenue !" et un paragraphe `<p>` "Nous sommes heureux de vous voir ici.". Utilisez-le dans votre application.

#### Synthèse

Vous ne pensez plus en "pages", mais en "systèmes de composants". C'est un changement fondamental qui va décupler votre productivité. Pour l'instant, nos composants sont statiques. Demain, nous apprendrons à les rendre dynamiques et configurables en leur passant des données depuis l'extérieur, grâce aux **props**.

---

### J2 : Communication Descendante - Les Props

**Objectif(s) du Jour :**
- Comprendre comment un composant parent peut passer des données à un composant enfant.
- Déclarer des `props` dans un composant enfant.
- Lier des données du parent aux `props` de l'enfant en utilisant `v-bind`.
- Valider les `props` (type, requis, etc.).

**Notion Clé : Les Réglages d'une Machine**
Votre composant est une machine, par exemple une machine à café. Par défaut, elle fait du café noir. Mais vous voulez la configurer : "Je veux un café *avec du sucre*" ou "Je veux un café *décaféiné*". Les **props** (propriétés) sont les boutons et les cadrans de réglage de votre machine. Le composant parent utilise ces réglages (`:sucre="true"`, `:type-cafe="'deca'"`) pour dire au composant enfant comment il doit se comporter ou ce qu'il doit afficher.

---

#### Leçon

##### 1. Déclarer les Props

Dans l'objet de configuration du composant, on ajoute une option `props`.

```javascript
// Déclaration simple (moins recommandée)
props: ['username', 'age']

// Déclaration avec validation (meilleure pratique)
props: {
  username: {
    type: String, // Le type de donnée attendu
    required: true // Cette prop est-elle obligatoire ?
  },
  age: {
    type: Number,
    default: 25 // Une valeur par défaut si la prop n'est pas fournie
  }
}
```

##### 2. Passer les Props

Dans le template du parent, on utilise `v-bind` (ou le raccourci `:`) pour passer la donnée.

- **Exemple de Code (Un composant de carte utilisateur) :**
  ```html
  <div id="app">
    <!-- On passe les données 'user1' au composant via les props -->
    <user-card
      :user-name="user1.name"
      :age="user1.age"
      :is-premium="user1.premium"
    ></user-card>
  </div>

  <script>
    const app = Vue.createApp({
      data() { return {
        user1: { name: 'Alice', age: 30, premium: true }
      }}
    });

    app.component('user-card', {
      // Le composant reçoit les données et les utilise dans son template
      props: {
        userName: String,
        age: Number,
        isPremium: Boolean
      },
      template: `
        <div class="card">
          <h2>{{ userName }} <span v-if="isPremium">⭐</span></h2>
          <p>Âge : {{ age }} ans</p>
        </div>
      `
    });

    app.mount('#app');
  </script>
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour2.html`.
2.  Créez un composant `<blog-post>`.
3.  Déclarez deux `props` : `title` (String, required) et `author` (String, default: 'Anonyme').
4.  Le template du composant doit afficher le titre dans un `<h3>` et l'auteur dans un `<p>`.
5.  Dans l'application parente, utilisez ce composant deux fois, en lui passant des titres et auteurs différents.

#### Mini-Exercice du Jour

Créez un composant `<custom-button>` qui accepte une prop `buttonText`. Le template du composant affichera une balise `<button>` dont le texte est la valeur de la prop. Utilisez-le dans le parent pour créer un bouton "Valider" et un bouton "Annuler".

#### Synthèse

Vos composants ne sont plus des boîtes noires isolées. Ils sont devenus configurables et réutilisables dans une multitude de contextes. La communication se fait pour l'instant de haut en bas (Parent -> Enfant). Demain, nous allons voir comment un enfant peut communiquer avec son parent, grâce aux **événements**.

---

### J3 : Communication Ascendante - Les Événements (`$emit`)

**Objectif(s) du Jour :**
- Comprendre qu'un composant enfant ne doit pas modifier directement les props.
- Émettre des événements personnalisés depuis un composant enfant avec `$emit`.
- Écouter ces événements dans le composant parent avec `v-on`.
- Passer des données avec l'événement.

**Notion Clé : La Sonnette**
Imaginez un enfant dans sa chambre (le **composant enfant**). Sa chambre est en désordre, mais il ne peut pas aller chercher lui-même un sac poubelle dans la cuisine (il ne doit pas modifier l'état du parent). Que fait-il ? Il appuie sur une sonnette (`$emit('besoin-sac-poubelle')`) pour prévenir son parent (le **composant parent**). Le parent, qui écoute la sonnette (`@besoin-sac-poubelle="donnerSacPoubelle"`), entend le signal et décide de l'action à entreprendre (aller chercher le sac).

---

#### Leçon

##### 1. Émettre un Événement avec `$emit`

Dans une méthode du composant enfant, on utilise `this.$emit()`.
- Le premier argument est le nom de l'événement (convention: kebab-case).
- Le second argument (optionnel) est la donnée que l'on veut envoyer au parent.

##### 2. Écouter l'Événement

Dans le composant parent, on utilise `v-on` (ou le raccourci `@`) pour écouter l'événement personnalisé.

- **Exemple de Code (Un composant qui demande à être ajouté au panier) :**
  ```html
  <div id="app">
    <p>Articles dans le panier : {{ cart.length }}</p>
    <!-- Le parent écoute l'événement 'add-to-cart' -->
    <product-item
      product-name="Super Chaussures"
      @add-to-cart="handleAddToCart"
    ></product-item>
  </div>

  <script>
    const app = Vue.createApp({
      data() { return { cart: [] }},
      methods: {
        // Cette méthode est appelée quand l'enfant émet l'événement
        handleAddToCart(productName) {
          this.cart.push(productName);
          console.log(`${productName} a été ajouté au panier !`);
        }
      }
    });

    app.component('product-item', {
      props: ['productName'],
      template: `
        <div>
          <span>{{ productName }}</span>
          <!-- Au clic, on appelle une méthode qui va émettre l'événement -->
          <button @click="addToCart">Ajouter au panier</button>
        </div>
      `,
      methods: {
        addToCart() {
          // On émet un événement et on envoie le nom du produit avec
          this.$emit('add-to-cart', this.productName);
        }
      }
    });

    app.mount('#app');
  </script>
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour3.html`.
2.  Créez une application qui gère une liste de tâches (`todos`).
3.  Créez un composant `<todo-item>` qui reçoit une tâche en `prop`.
4.  Dans `<todo-item>`, ajoutez un bouton "Supprimer".
5.  Au clic sur ce bouton, le composant doit `$emit` un événement `delete-todo` en passant l'ID de la tâche en payload.
6.  Le composant parent doit écouter cet événement et, en réponse, supprimer la bonne tâche de son tableau `todos`.

#### Mini-Exercice du Jour

Créez un composant `<rating-control>` qui affiche 5 étoiles. Au clic sur une étoile, le composant doit émettre un événement `set-rating` avec le numéro de l'étoile cliquée (de 1 à 5). Le parent affichera simplement "Vous avez noté : X/5".

#### Synthèse

Le circuit de communication est désormais complet ! Les données descendent via les `props`, et les actions remontent via les `$emit`. C'est le flux de données unidirectionnel, un concept clé qui rend les applications Vue robustes et prévisibles. Demain, nous verrons comment rendre nos composants encore plus flexibles en leur permettant d'accepter du contenu HTML : les **slots**.

---

### J4 : Flexibilité et Composition - Les Slots

**Objectif(s) du Jour :**
- Comprendre la limite des props pour passer du contenu complexe.
- Utiliser le `<slot>` par défaut pour injecter du contenu dans un composant.
- Utiliser les "slots nommés" pour créer des composants avec plusieurs zones de contenu personnalisables.

**Notion Clé : Le Cadre Photo**
Un composant, c'est comme un cadre photo.
- **Les `props`** sont les réglages du cadre lui-même : couleur (`:color="'noir'"`), matériau (`:material="'bois'"`).
- **Le `<slot>`** est l'espace vide au milieu du cadre. Il ne sait pas ce qu'il va contenir. C'est vous, lorsque vous utilisez le cadre, qui décidez d'y mettre une photo de paysage, un portrait de famille, ou même un dessin d'enfant. Le slot permet au composant parent de "remplir les blancs" du composant enfant avec n'importe quel contenu HTML.

---

#### Leçon

##### 1. Le Slot par Défaut

Il suffit de placer une balise `<slot></slot>` dans le template du composant enfant. Tout le contenu placé entre les balises du composant dans le parent sera rendu à cet endroit.

- **Exemple de Code (Un composant de carte générique) :**
  ```html
  <div id="app">
    <base-card>
      <!-- Tout ce HTML sera injecté dans le slot -->
      <h3>Titre de ma carte</h3>
      <p>Ceci est un paragraphe de contenu.</p>
      <img src="https://via.placeholder.com/100" alt="">
    </base-card>
  </div>

  <script>
    // ...
    app.component('base-card', {
      template: `
        <div class="card-wrapper">
          <!-- Le contenu du parent vient se placer ici -->
          <slot></slot>
        </div>
      `
    });
    // ...
  </script>
  ```

##### 2. Les Slots Nommés

Pour plus de contrôle, on peut nommer les slots.
- **Dans l'enfant :** `<slot name="header"></slot>` et `<slot name="footer"></slot>`.
- **Dans le parent :** On utilise la directive `<template #header>` pour cibler le slot correspondant.

- **Exemple avec slots nommés :**
  ```html
  <div id="app">
    <base-card>
      <template #header>
        <h2>Titre personnalisé pour l'en-tête</h2>
      </template>

      <!-- Le contenu sans 'template' va dans le slot par défaut -->
      <p>Contenu principal.</p>

      <template #footer>
        <button>Action</button>
      </template>
    </base-card>
  </div>
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour4.html`.
2.  Créez un composant `<modal-dialog>`.
3.  Son template doit avoir une structure de modale (un fond sombre, une boîte de contenu).
4.  À l'intérieur de la boîte de contenu, placez un `<slot></slot>`.
5.  Dans le parent, utilisez `<modal-dialog>` et placez un formulaire simple à l'intérieur. Le formulaire doit apparaître dans la modale.

#### Mini-Exercice du Jour

Faites évoluer le composant `<modal-dialog>` pour qu'il ait trois slots nommés : `title`, `body` (le slot par défaut), et `actions`. Dans le parent, utilisez ces slots pour structurer le contenu de votre modale avec un titre, un corps de texte et des boutons d'action dans le pied de page.

#### Synthèse

Les slots sont l'outil ultime de composition dans Vue. Ils permettent de créer des composants de "layout" extrêmement flexibles et réutilisables (cartes, modales, panneaux...). Vous êtes maintenant prêt à construire une véritable petite bibliothèque de composants.

---

### J5 : Projet de la Semaine - Créer une Bibliothèque de Composants UI

**Objectif(s) du Jour :**
- Synthétiser toutes les connaissances sur les composants (props, events, slots).
- Penser en termes de réutilisabilité et de généricité.
- Construire trois composants UI fondamentaux qui serviront de base à de futurs projets.

**Notion Clé : Fabriquer sa Propre Boîte de LEGO**
Cette semaine, vous avez appris à utiliser les briques de LEGO. Aujourd'hui, vous allez devenir un fabricant de LEGO. Votre mission est de créer un petit "kit de démarrage" avec trois des briques les plus utiles et les plus courantes. Chaque brique doit être conçue pour être aussi flexible et réutilisable que possible, afin que vous (ou d'autres développeurs) puissiez les utiliser pour construire rapidement n'importe quelle interface.

---

#### PROJET DE LA SEMAINE : Ma Première Bibliothèque de Composants

Votre mission est de créer une page qui présente une petite bibliothèque de trois composants UI réutilisables.

**Composants à construire :**

1.  **Le Bouton : `<custom-button>`**
    - **Props :**
      - `kind` (ou `type`): une chaîne de caractères pour le style (ex: `'primary'`, `'secondary'`). Utilisez cette prop pour appliquer une classe CSS différente (`:class`).
    - **Slot :**
      - Doit utiliser le slot par défaut pour que l'on puisse définir le texte ou l'icône du bouton depuis le parent (ex: `<custom-button>Valider</custom-button>`).
    - **Événements :**
      - Doit émettre un événement `click` natif. L'utilisateur doit pouvoir faire `@click` directement dessus.

2.  **La Carte : `<info-card>`**
    - **Slots :**
      - Doit avoir deux slots nommés : `header` et `footer`.
      - Doit aussi avoir un slot par défaut pour le contenu principal.
    - **Design :**
      - Le composant doit fournir un style de base (une bordure, une ombre, du padding) pour "encadrer" le contenu qui lui est fourni.

3.  **La Modale : `<base-modal>` (le plus complexe)**
    - **Props :**
      - `show`: un booléen qui contrôle la visibilité de la modale (utilisez `v-if` sur l'élément racine de la modale).
    - **Slots :**
      - Doit avoir des slots pour le `header` (titre), `body` (contenu principal) et `footer` (boutons d'action).
    - **Événements :**
      - Doit émettre un événement `close` quand l'utilisateur clique sur un bouton "Fermer" à l'intérieur de la modale ou sur le fond semi-transparent.
      - Dans l'application parente, vous aurez une donnée (ex: `isModalVisible`) que vous passerez à la prop `:show`. Quand la modale émet `@close`, le parent mettra `isModalVisible` à `false`.

**Livrable :** Un unique fichier `index.html` qui :
1.  Définit ces trois composants.
2.  Les utilise dans le template de l'application principale pour démontrer toutes leurs fonctionnalités (plusieurs types de boutons, une carte avec du contenu, et un bouton qui ouvre la modale).

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez franchi une étape cruciale. Vous ne codez plus des applications, vous concevez des **systèmes de design** réutilisables. Cette compétence est au cœur du développement frontend moderne et est extrêmement valorisée. La semaine prochaine, nous apprendrons à connecter ces composants et ces pages entre eux pour créer de véritables applications monopages (SPA) grâce au routage.