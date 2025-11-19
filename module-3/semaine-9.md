## Semaine 9 : Les Fondamentaux de Vue.js

### J1 : Le "Pourquoi" d'un Framework et la Réactivité

**Objectif(s) du Jour :**
- Comprendre les limites du JavaScript "vanilla" pour des applications complexes.
- Découvrir le concept de "programmation déclarative" de Vue.
- Créer sa première application Vue et comprendre la magie de la réactivité.
- Lier des données de l'état (state) au template.

**Notion Clé : Le Tableur Magique**
Imaginez un tableur (comme Excel). Dans la cellule A1, vous avez le chiffre `10`. Dans la cellule B1, vous avez `20`. Dans la cellule C1, vous écrivez la formule `=A1+B1`. La cellule C1 affiche `30`.
Maintenant, si vous changez la valeur de A1 pour `15`, que se passe-t-il ? La cellule C1 se met à jour **automatiquement** et affiche `35`. Vous n'avez pas eu à dire à C1 "recalcule-toi !".
**Vue.js, c'est ce tableur magique pour vos pages web.** Vous définissez vos données (A1, B1), vous déclarez comment les afficher (la formule en C1), et Vue s'occupe de mettre à jour l'affichage automatiquement quand les données changent. C'est la **réactivité**. Fini le `document.querySelector` pour chaque mise à jour !

---

#### Leçon

##### 1. Pourquoi un Framework ?

En JavaScript "vanilla", pour changer un texte sur la page, vous devez :
1.  Sélectionner l'élément du DOM.
2.  Modifier sa propriété `textContent` ou `innerHTML`.
C'est une approche **impérative** : vous donnez des ordres étape par étape. Pour de grosses applications, cela devient un cauchemar à maintenir.

Vue.js propose une approche **déclarative** : vous décrivez l'état final que vous souhaitez, et Vue se charge de le réaliser.

##### 2. Votre Première Application Vue

On peut commencer à utiliser Vue très simplement en l'important via une balise `<script>` dans notre HTML.

- **Exemple de Code (Le Squelette Vue.js) :**
  ```html
  <!DOCTYPE html>
  <html lang="fr">
  <head>
      <title>Ma Première App Vue</title>
      <!-- On importe Vue.js -->
      <script src="https://unpkg.com/vue@3"></script>
  </head>
  <body>
      <!-- Cette div est la "zone de contrôle" de notre app Vue -->
      <div id="app">
          <!-- Les doubles accolades permettent d'afficher une donnée -->
          <h1>{{ message }}</h1>
      </div>

      <script>
          const { createApp } = Vue;

          createApp({
              // La fonction data() contient l'état (le "state") de notre application
              data() {
                  return {
                      message: "Bonjour, Vue.js !"
                  };
              }
          }).mount('#app'); // On dit à Vue de prendre le contrôle de la div avec l'id "app"
      </script>
  </body>
  </html>
  ```

##### 3. La Réactivité en Action

Si vous ouvrez cette page dans le navigateur, ouvrez la console et tapez `app.message = "Le message a changé !"`. Vous verrez le `<h1>` se mettre à jour instantanément, sans aucune manipulation manuelle du DOM.

---

#### Mise en Pratique

1.  Créez un nouveau dossier `bootcamp-vue`.
2.  Créez un fichier `jour1.html`.
3.  Copiez-collez le squelette de code ci-dessus dans ce fichier.
4.  Ouvrez-le dans votre navigateur.
5.  Modifiez la valeur de `message` dans votre code pour voir le changement.
6.  Changez la valeur de `message` directement depuis la console du navigateur pour voir la réactivité.

#### Mini-Exercice du Jour

Créez une application Vue simple qui affiche un compteur. Dans `data`, créez une propriété `count` initialisée à `0`. Affichez-la dans le HTML avec `{{ count }}`. Pour l'instant, vous ne pouvez pas encore le faire changer avec un bouton, mais vous pouvez le faire depuis la console !

#### Synthèse

Aujourd'hui, vous avez découvert un changement de paradigme majeur. Vous ne donnez plus d'ordres au DOM, vous décrivez un état et vous laissez le framework travailler. Demain, nous allons voir comment l'utilisateur peut interagir avec cet état grâce aux directives `v-on` et `v-bind`.

---

### J2 : Directives : Donner des Ordres à HTML (`v-on` & `v-bind`)

**Objectif(s) du Jour :**
- Réagir aux actions de l'utilisateur (clics, etc.) avec `v-on`.
- Définir des fonctions réutilisables avec le bloc `methods`.
- Lier dynamiquement des attributs HTML aux données avec `v-bind`.

**Notion Clé : La Télécommande et l'Écran d'Information**
- `v-on` (ou `@`) est le **bouton de votre télécommande**. Quand vous appuyez sur `@click`, vous envoyez un signal à votre application pour qu'elle *fasse quelque chose* (lancer une méthode).
- `v-bind` (ou `:`) est l'**écran d'information** de votre appareil. Il affiche une information qui dépend de l'état interne. Par exemple, l'attribut `disabled` d'un bouton est lié (`:disabled`) à une donnée `isLoading`. Si `isLoading` est `true`, le bouton se désactive.

---

#### Leçon

##### 1. Gérer les Événements avec `v-on`

La directive `v-on` permet d'écouter les événements du DOM et d'exécuter du code quand ils se produisent.
- **Syntaxe complète :** `v-on:click="maMethode"`
- **Raccourci (utilisé 99% du temps) :** `@click="maMethode"`
- Les méthodes sont définies dans un objet `methods` dans notre application Vue.

##### 2. Lier des Attributs avec `v-bind`

La directive `v-bind` permet de lier dynamiquement la valeur d'un attribut HTML à une donnée de notre application.
- **Syntaxe complète :** `v-bind:href="monUrl"`
- **Raccourci (utilisé 99% du temps) :** `:href="monUrl"`

- **Exemple de Code (Compteur Interactif) :**
  ```html
  <div id="app">
      <p>Compteur : {{ count }}</p>
      <!-- @click appelle la méthode 'increment' -->
      <button @click="increment">Incrémenter</button>
      <!-- Le bouton est désactivé si 'count' est inférieur à 0 -->
      <button @click="decrement" :disabled="count <= 0">Décrémenter</button>
  </div>
  
  <script>
    Vue.createApp({
      data() {
        return {
          count: 0
        };
      },
      // Les fonctions qui modifient notre état ou exécutent des actions
      methods: {
        increment() {
          // 'this' fait référence à l'instance de l'application
          this.count++;
        },
        decrement() {
          this.count--;
        }
      }
    }).mount('#app');
  </script>
  ```

---

#### Mise en Pratique

Reprenez l'exercice du compteur d'hier.
1.  Ajoutez un objet `methods` à votre application Vue.
2.  Créez une méthode `increment()` qui augmente la valeur de `count`.
3.  Ajoutez un bouton dans votre HTML et utilisez `@click` pour appeler cette méthode.
4.  Testez : chaque clic sur le bouton doit maintenant augmenter le compteur affiché.

#### Mini-Exercice du Jour

Créez une application avec une donnée `messageVisible` initialisée à `true`. Ajoutez un bouton qui, au clic, inverse la valeur de `messageVisible` (de `true` à `false` et vice-versa). Pour l'instant, vous ne verrez rien changer visuellement, mais vous pourrez vérifier dans la console Vue Devtools (extension de navigateur à installer !) que la donnée change bien.

#### Synthèse

Vous savez maintenant créer une boucle d'interaction complète : l'utilisateur déclenche une action (`@click`), qui appelle une méthode, qui modifie l'état (`data`), qui met à jour l'affichage (`{{...}}`) et les attributs (`:disabled`). Demain, nous allons voir comment afficher des listes entières et des éléments conditionnels avec `v-for` et `v-if`.

---

### J3 : Affichage Dynamique : Listes et Conditions (`v-for` & `v-if`)

**Objectif(s) du Jour :**
- Afficher une liste d'éléments à partir d'un tableau de données avec `v-for`.
- Comprendre l'importance de l'attribut `:key`.
- Afficher ou masquer des blocs de HTML conditionnellement avec `v-if`, `v-else` et `v-else-if`.

**Notion Clé : Les Instructions de Montage**
- `v-for` : C'est l'instruction "Pour chacune des vis dans le sachet, vissez-en une ici". Vue va répéter un bloc de HTML pour chaque élément d'un tableau.
- `v-if` : C'est l'instruction "Si la pièce A est du modèle 'deluxe', ajoutez la lumière LED. Sinon, ne faites rien". Vue va ajouter ou retirer complètement un bloc de HTML du DOM en fonction d'une condition.

---

#### Leçon

##### 1. Rendu de Listes avec `v-for`

`v-for` permet de parcourir un tableau et de générer du HTML pour chaque élément.
- **Syntaxe :** `v-for="element in monTableau"`
- **`:key` est Obligatoire :** Pour aider Vue à optimiser les mises à jour de la liste, chaque élément doit avoir une clé unique, généralement l'ID de l'objet.
  `v-for="item in items" :key="item.id"`

##### 2. Rendu Conditionnel avec `v-if`

`v-if` permet de n'afficher un élément que si une condition est vraie.
- **Syntaxe :** `v-if="maCondition"`
- On peut enchaîner avec `v-else-if` et `v-else`.

- **Exemple de Code (Liste de Tâches Simple) :**
  ```html
  <div id="app">
      <h2>Mes Tâches</h2>
      <div v-if="tasks.length === 0">
          Bravo, vous n'avez plus rien à faire !
      </div>
      <ul v-else>
          <!-- On boucle sur le tableau 'tasks' -->
          <li v-for="task in tasks" :key="task.id">
              {{ task.text }}
          </li>
      </ul>
  </div>

  <script>
    Vue.createApp({
      data() {
        return {
          tasks: [
            { id: 1, text: 'Apprendre v-for' },
            { id: 2, text: 'Apprendre v-if' },
            { id: 3, text: 'Construire un truc génial' }
          ]
        };
      }
    }).mount('#app');
  </script>
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour3.html`.
2.  Créez une application Vue avec un tableau d'utilisateurs dans `data`. Chaque utilisateur sera un objet avec un `id` et un `name`.
3.  Utilisez `v-for` pour afficher ces utilisateurs dans une liste `<ul>`. N'oubliez pas le `:key`.
4.  Testez en ajoutant un nouvel utilisateur au tableau depuis la console. La liste doit se mettre à jour.

#### Mini-Exercice du Jour

Reprenez la liste d'utilisateurs. Ajoutez une propriété `isOnline: true/false` à chaque objet utilisateur. En utilisant `v-if` à l'intérieur du `v-for`, affichez un petit badge "🟢 En ligne" uniquement à côté des utilisateurs dont la propriété `isOnline` est `true`.

#### Synthèse

Vous savez maintenant générer des interfaces dynamiques complexes à partir de vos données. `v-for` et `v-if` sont deux des directives les plus utilisées. Demain, nous allons découvrir une fonctionnalité très puissante pour manipuler des données dérivées de manière efficace : les propriétés calculées.

---

### J4 : Les Données Intelligentes - Propriétés Calculées (Computed)

**Objectif(s) du Jour :**
- Comprendre quand et pourquoi utiliser une propriété calculée.
- Différencier une `method` d'une `computed property`.
- Créer une `computed property` pour dériver une donnée de l'état.

**Notion Clé : Le Calculateur à Mémoire Cache**
Imaginez que vous deviez calculer le total d'un panier d'achats.
- **Une `method` :** C'est un calculateur simple. Chaque fois que vous lui demandez le total, il refait l'addition de tous les articles, même si rien n'a changé. C'est un peu bête.
- **Une `computed property` :** C'est un calculateur intelligent avec une mémoire. La première fois, il fait l'addition et **met le résultat en cache**. Tant que les articles du panier ne changent pas, si vous lui redemandez le total, il vous donne instantanément le résultat en mémoire sans refaire le calcul. Il ne recalculera que si un article est ajouté ou supprimé. C'est beaucoup plus performant.

---

#### Leçon

##### 1. Qu'est-ce qu'une Propriété Calculée ?

Une propriété calculée est une donnée qui est calculée à partir d'autres données. Elle est définie dans l'objet `computed`.
Elle est réactive : si une de ses dépendances change, elle se met à jour.
Elle est mise en cache : elle n'est ré-évaluée que si ses dépendances changent.

##### 2. `methods` vs. `computed`

- Utilisez `computed` pour des données que vous voulez afficher dans le template et qui dépendent d'autres données.
- Utilisez `methods` en réponse à un événement (comme un `@click`) pour modifier l'état.

- **Exemple de Code (Filtrage de liste) :**
  ```html
  <div id="app">
    <input v-model="searchTerm" placeholder="Filtrer les fruits...">
    <ul>
      <!-- On boucle sur la propriété calculée, pas sur le tableau original ! -->
      <li v-for="fruit in filteredFruits" :key="fruit">{{ fruit }}</li>
    </ul>
  </div>

  <script>
  Vue.createApp({
    data() {
      return {
        searchTerm: '',
        fruits: ['Pomme', 'Banane', 'Orange', 'Fraise', 'Kiwi']
      };
    },
    computed: {
      // Cette "donnée" est calculée
      filteredFruits() {
        if (!this.searchTerm) {
          return this.fruits;
        }
        return this.fruits.filter(fruit =>
          fruit.toLowerCase().includes(this.searchTerm.toLowerCase())
        );
      }
    }
  }).mount('#app');
  </script>
  ```
  Note : On a introduit `v-model` ici, un raccourci pour lier la valeur d'un champ de formulaire à une donnée. C'est l'équivalent de `:value="searchTerm" @input="event => searchTerm = event.target.value"`.

---

#### Mise en Pratique

1.  Créez un fichier `jour4.html`.
2.  Créez une application Vue avec un `firstName` et un `lastName` dans `data`.
3.  Créez une propriété calculée `fullName` qui concatène les deux.
4.  Affichez `{{ fullName }}` dans le template. Modifiez les prénoms et noms pour voir le nom complet se mettre à jour automatiquement.

#### Mini-Exercice du Jour

Créez une application avec une donnée `message`. Créez une propriété calculée `reversedMessage` qui retourne le message inversé (`this.message.split('').reverse().join('')`). Affichez les deux dans le template.

#### Synthèse

Les propriétés calculées sont essentielles pour garder votre logique de template propre et vos applications performantes. Elles permettent de séparer la logique de transformation des données de la simple présentation. Vous avez maintenant tous les outils pour le projet de la semaine !

---

### J5 : Projet de la Semaine - La To-Do List version Vue.js

**Objectif(s) du Jour :**
- Mettre en pratique toutes les notions fondamentales de Vue vues cette semaine.
- Construire une application interactive complète.
- Apprécier la différence de clarté et de concision par rapport à une solution en JavaScript vanilla.

**Notion Clé : L'Assemblage Final**
C'est le moment de prendre toutes les briques que nous avons fabriquées cette semaine (réactivité, directives, méthodes, propriétés calculées) et de construire notre première maison Vue.js. La To-Do List est le projet parfait car elle nécessite : de l'affichage de liste (`v-for`), de l'ajout/suppression (méthodes via `@click`), du style conditionnel (`:class`), de l'ajout de nouvelles tâches (liaison de formulaire avec `v-model`), et du comptage de tâches restantes (`computed`).

---

#### PROJET DE LA SEMAINE : Re-créer la To-Do List

Votre mission est de reconstruire l'application To-Do List que vous aviez faite en JavaScript vanilla, mais cette fois-ci, en utilisant la puissance de Vue.js.

**Contraintes et Fonctionnalités Obligatoires :**

1.  **État de l'application (`data`) :**
    - Un tableau `todos` où chaque tâche est un objet `{ id: Date.now(), text: '...', completed: false }`.
    - Une chaîne `newTodoText` pour stocker le texte du champ de saisie.

2.  **Affichage des tâches (`v-for`) :**
    - Affichez la liste des tâches.
    - Utilisez la directive `v-for` et n'oubliez pas le `:key`.

3.  **Ajout d'une tâche (`v-model`, `@submit`) :**
    - Un formulaire avec un champ de texte.
    - Utilisez `v-model` pour lier le champ de texte à `newTodoText`.
    - À la soumission du formulaire (`@submit.prevent`), une méthode `addTodo` doit créer une nouvelle tâche, l'ajouter au tableau `todos`, et vider le champ de saisie.

4.  **Marquer une tâche comme terminée (`:class`, `@click`) :**
    - Le texte de la tâche doit être barré si sa propriété `completed` est `true`. Utilisez une liaison de classe dynamique `:class="{ 'completed-class': todo.completed }"`.
    - Un clic sur une tâche (ou une case à cocher) doit appeler une méthode qui inverse la valeur de `todo.completed`.

5.  **Supprimer une tâche (`@click`) :**
    - Chaque tâche doit avoir un bouton "Supprimer".
    - Au clic, une méthode `removeTodo(todo)` doit retirer la tâche correspondante du tableau `todos`.

6.  **Compteur de tâches restantes (`computed`) :**
    - Affichez le nombre de tâches qui ne sont pas encore terminées.
    - Cette valeur doit être une **propriété calculée** basée sur le tableau `todos`.

**Livrable :** Un unique fichier `index.html` contenant votre application To-Do List complète, déposé sur votre dépôt GitHub. Le code doit être propre et utiliser toutes les notions vues cette semaine.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez fait vos premiers pas dans le monde des frameworks JavaScript modernes. Comparez le code de cette To-Do list avec celui de la version en JavaScript vanilla. La clarté, la concision et la puissance de l'approche déclarative devraient être évidentes. La semaine prochaine, nous irons plus loin en découpant notre application en morceaux réutilisables : les composants.