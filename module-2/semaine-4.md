## Semaine 4 : Les Bases de JavaScript

### J1 (Lundi) : "Hello, JavaScript !" - Variables et Console

**Objectif(s) du Jour :**
- Comprendre le rôle de JavaScript et sa différence avec HTML/CSS.
- Lier un fichier JavaScript à une page HTML.
- Utiliser la console du navigateur, votre nouvel outil N°1.
- Déclarer des variables pour stocker des informations (`let`, `const`).
- Connaître les types de données primitifs (String, Number, Boolean).

**Notion Clé : Donner des Ordres au Navigateur**
HTML décrit la structure (un squelette). CSS décrit l'apparence (des vêtements). JavaScript, lui, donne des **ordres** : c'est le cerveau et le système nerveux. Il ne décrit rien, il *fait* des choses. Votre premier outil pour voir le résultat de ces ordres n'est pas la page web elle-même, mais la **console des outils de développement** (`F12`). C'est votre laboratoire, votre terrain de jeu pour tester chaque instruction.

---

#### Leçon

##### 1. Lier un fichier JavaScript
Comme pour le CSS, on lie notre fichier `.js`. La convention est de placer la balise `<script>` juste avant la fin de la balise `</body>`. Pourquoi ? Pour s'assurer que tout le HTML est chargé *avant* que le JavaScript ne tente de le manipuler.

```html
<!-- Dans votre fichier .html -->
    ...
    <script src="script.js"></script>
  </body>
</html>
```

##### 2. La Console, votre Meilleure Amie
La fonction `console.log()` vous permet d'afficher n'importe quoi dans la console de votre navigateur. C'est l'outil de débogage le plus fondamental.

```javascript
// Dans votre fichier script.js
console.log("Hello, World!");
console.log(42);
```

##### 3. Les Variables : des Boîtes pour vos Données
Une variable est une "boîte" nommée dans laquelle vous stockez une information.
- `let` : Déclare une variable dont la valeur **peut changer**. C'est une boîte avec un couvercle que l'on peut ouvrir.
- `const` : Déclare une constante dont la valeur **ne peut pas changer** une fois assignée. C'est une boîte scellée. On utilise `const` par défaut, et `let` uniquement si on sait que la valeur doit être modifiée.

##### 4. Les Types de Données Primitifs
- **String** (chaîne de caractères) : Du texte, toujours entre guillemets (`"` ou `'`).
- **Number** (nombre) : Des chiffres, pour les calculs.
- **Boolean** (booléen) : Ne peut avoir que deux valeurs : `true` (vrai) ou `false` (faux).

- **Exemple de Code :**
  ```javascript
  const nomUtilisateur = "Alice"; // String
  let score = 0;                 // Number
  const estConnecte = true;        // Boolean

  console.log("L'utilisateur s'appelle :");
  console.log(nomUtilisateur);

  score = 10; // On peut changer la valeur d'une variable déclarée avec 'let'
  console.log("Nouveau score :");
  console.log(score);

  // Ceci provoquera une erreur, car on ne peut pas changer une constante :
  // nomUtilisateur = "Bob";
  ```

---

#### Mise en Pratique

1.  Créez un dossier `bootcamp-semaine-4`. À l'intérieur, créez `index.html` et `script.js`.
2.  Dans `index.html`, mettez une structure HTML de base et liez votre `script.js`.
3.  Dans `script.js`, écrivez `console.log("Mon script est bien chargé !");`.
4.  Ouvrez `index.html` dans votre navigateur, ouvrez la console (F12) et vérifiez que le message s'affiche.
5.  Dans `script.js`, déclarez des variables pour décrire un film : `titreFilm` (const), `anneeSortie` (const), `noteSpectateurs` (let). Affichez chaque variable dans la console.

#### Mini-Exercice du Jour

Créez une variable `nombreDeVies` initialisée à 9 avec `let`. En dessous, réassignez cette variable pour la diminuer de 1. Affichez la nouvelle valeur dans la console. Créez une constante `nomDuJeu` et essayez de la modifier pour voir l'erreur apparaître dans la console.

#### Synthèse

Vous avez écrit vos premières lignes de code qui *s'exécute*. Vous savez comment "parler" au navigateur via la console et comment stocker des informations. C'est la première étape de la programmation. Demain, nous allons apprendre à faire réfléchir notre programme en lui faisant prendre des décisions.

---

### J2 (Mardi) : Prendre des Décisions avec les Conditions

**Objectif(s) du Jour :**
- Comprendre les opérateurs de comparaison (`===`, `>`, `<`...).
- Utiliser `if`, `else if` et `else` pour exécuter du code sous certaines conditions.
- Combiner des conditions avec les opérateurs logiques (`&&`, `||`).

**Notion Clé : La Bifurcation**
Un programme devient vraiment puissant quand il peut adapter son comportement. Les conditions sont des "bifurcations" sur la route de votre code. "SI l'utilisateur a plus de 18 ans, ALORS affiche-lui cette page, SINON, affiche-lui un message d'avertissement". C'est le cœur de toute logique de programmation.

---

#### Leçon

##### 1. La Vérité est Binaire (Vrai ou Faux)
Toute condition en JavaScript est évaluée à un booléen : `true` ou `false`.

##### 2. Les Opérateurs de Comparaison
- `===` : Égalité stricte (valeur ET type). **Utilisez toujours celui-ci !**
- `!==` : Inégalité stricte.
- `>` : Strictement supérieur à.
- `<` : Strictement inférieur à.
- `>=` : Supérieur ou égal à.
- `<=` : Inférieur ou égal à.

##### 3. La Structure `if / else`
- `if (condition)` : Le code entre les `{}` ne s'exécute que si la `condition` est `true`.
- `else` : Le plan B. Le code dans ce bloc s'exécute si la condition du `if` est `false`.
- `else if (autreCondition)` : Permet de tester plusieurs conditions à la suite.

##### 4. Les Opérateurs Logiques
- `&&` (ET) : `condition1 && condition2` est `true` seulement si les **deux** conditions sont `true`.
- `||` (OU) : `condition1 || condition2` est `true` si **au moins une** des deux conditions est `true`.

- **Exemple de Code :**
  ```javascript
  const age = 25;
  const aLePermis = true;

  if (age >= 18) {
    console.log("Vous êtes majeur.");
  } else {
    console.log("Vous êtes mineur.");
  }

  // Combinaison de conditions
  if (age >= 18 && aLePermis === true) {
    console.log("Vous pouvez conduire la voiture.");
  } else if (age >= 18 && aLePermis === false) {
    console.log("Vous êtes majeur mais vous ne pouvez pas conduire.");
  } else {
    console.log("Interdiction de conduire.");
  }
  ```

---

#### Mise en Pratique

Dans votre `script.js` :
1.  Créez une constante `heure` avec une valeur numérique entre 0 et 23.
2.  Écrivez une structure `if/else if/else` qui affiche "Bonjour" si l'heure est avant 18h, et "Bonsoir" sinon.
3.  Améliorez-la pour afficher "Bonne nuit" si l'heure est après 22h ou avant 6h, "Bonjour" entre 6h et 18h, et "Bonsoir" le reste du temps.
4.  Créez deux variables booléennes `emailVerifie` et `paiementOK`. Écrivez une condition qui n'affiche "Accès au cours premium" que si les deux sont `true`.

#### Mini-Exercice du Jour

Créez une variable `note` (sur 20). Écrivez une condition qui affiche dans la console :
- "Excellent" si la note est supérieure à 16.
- "Bien" si la note est entre 14 et 16 (inclus).
- "Assez bien" si la note est entre 12 et 14 (exclu).
- "Passable" si la note est entre 10 et 12 (exclu).
- "Insuffisant" pour tout le reste.

#### Synthèse

Votre programme n'est plus une ligne droite, il peut maintenant prendre des chemins différents. Vous avez acquis le principal outil de la logique. Demain, nous verrons comment faire répéter des actions à notre programme avec les boucles.

---

### J3 (Mercredi) : Répéter des Actions avec les Boucles

**Objectif(s) du Jour :**
- Comprendre la nécessité de répéter des actions sans dupliquer de code.
- Utiliser la boucle `for` pour itérer un nombre de fois défini.
- Utiliser la boucle `while` pour itérer tant qu'une condition est vraie.
- Éviter le piège des boucles infinies.

**Notion Clé : L'Automatisation**
Imaginez devoir écrire `console.log("Bonjour")` 100 fois. C'est long, fastidieux et stupide. Les boucles sont la réponse. Elles sont l'outil d'automatisation du développeur, permettant d'exécuter un même bloc de code autant de fois que nécessaire, avec de légères variations à chaque passage.

---

#### Leçon

##### 1. La Boucle `for`
Parfaite quand on sait **combien de fois** on veut répéter l'action. Sa syntaxe se décompose en 3 parties : `for (initialisation; condition; incrémentation)`.
- **Initialisation :** Crée un compteur (ex: `let i = 0`). S'exécute une seule fois, au début.
- **Condition :** La boucle continue tant que cette condition est `true` (ex: `i < 10`).
- **Incrémentation :** Ce qui se passe après chaque tour de boucle (ex: `i++`, qui est un raccourci pour `i = i + 1`).

```javascript
// Affiche les nombres de 0 à 9
for (let i = 0; i < 10; i++) {
  console.log("Le compteur vaut : " + i);
}
```

##### 2. La Boucle `while`
Parfaite quand on veut répéter une action **tant qu'une condition est vraie**, mais qu'on ne sait pas à l'avance combien de tours cela prendra.
**Attention :** Il faut s'assurer que la condition deviendra `false` à un moment donné, sinon c'est la boucle infinie et votre navigateur plantera !

```javascript
let nombreDeVies = 3;

while (nombreDeVies > 0) {
  console.log("Vous avez encore " + nombreDeVies + " vies.");
  // Très important : on modifie la variable de la condition dans la boucle !
  nombreDeVies--; // Raccourci pour nombreDeVies = nombreDeVies - 1
}

console.log("Game Over.");
```

---

#### Mise en Pratique

Dans votre `script.js` :
1.  Écrivez une boucle `for` qui affiche la table de multiplication de 7 (de 1 * 7 à 10 * 7).
2.  Créez une variable `batterie` à 100. Écrivez une boucle `while` qui affiche "Il reste X% de batterie" et qui diminue la batterie de 10 à chaque tour, tant que la batterie est au-dessus de 20%. À la fin, affichez "Batterie faible, veuillez recharger".

#### Mini-Exercice du Jour : Le "FizzBuzz"

C'est un exercice de programmation classique. Écrivez une boucle `for` qui compte de 1 à 100.
- Si le nombre est un multiple de 3, affichez "Fizz".
- Si le nombre est un multiple de 5, affichez "Buzz".
- Si le nombre est un multiple de 3 ET de 5, affichez "FizzBuzz".
- Sinon, affichez le nombre.
(Indice : l'opérateur modulo `%` vous donne le reste d'une division. `i % 3 === 0` signifie que `i` est un multiple de 3).

#### Synthèse

Vous savez maintenant automatiser des tâches répétitives. Vous avez les trois piliers de l'algorithmique de base : les variables (stocker), les conditions (décider), et les boucles (répéter). Demain, nous apprendrons à organiser notre code en blocs réutilisables : les fonctions.

---

### J4 (Jeudi) : Organiser son Code avec les Fonctions

**Objectif(s) du Jour :**
- Comprendre l'intérêt des fonctions pour ne pas se répéter (principe DRY).
- Déclarer et appeler une fonction.
- Passer des informations à une fonction via les paramètres.
- Récupérer un résultat d'une fonction avec `return`.

**Notion Clé : La Recette de Cuisine**
Une fonction, c'est comme une recette de cuisine que vous écrivez une bonne fois pour toutes. La recette a un nom ("Gâteau au chocolat"), elle a besoin d'ingrédients (les **paramètres**), elle suit une série d'étapes (le corps de la fonction), et à la fin, elle produit un résultat (le gâteau, la valeur de **retour**). Une fois la recette écrite, vous pouvez la réutiliser autant de fois que vous voulez, avec des ingrédients légèrement différents.

---

#### Leçon

##### 1. Déclarer et Appeler une Fonction
- **Déclaration :** On écrit la "recette".
- **Appel :** On exécute la "recette".

```javascript
// 1. Déclaration de la fonction
function saluer() {
  console.log("Bonjour à tous !");
}

// 2. Appel de la fonction (on peut le faire autant de fois qu'on veut)
saluer();
saluer();
```

##### 2. Les Paramètres (les ingrédients)
Les paramètres sont des variables que la fonction reçoit pour travailler avec.

```javascript
function saluerQuelquun(nom) { // 'nom' est un paramètre
  console.log("Bonjour, " + nom + " !");
}

saluerQuelquun("Alice"); // "Alice" est l'argument passé au paramètre 'nom'
saluerQuelquun("Bob");
```

##### 3. Le Retour (`return` - le plat final)
Une fonction peut (et souvent doit) renvoyer un résultat. L'instruction `return` met fin à la fonction et renvoie la valeur spécifiée.

```javascript
function additionner(a, b) {
  const resultat = a + b;
  return resultat; // La fonction "renvoie" la valeur de resultat
}

const somme = additionner(5, 3); // On stocke la valeur de retour (8) dans la variable 'somme'
console.log(somme); // Affiche 8
```

---

#### Mise en Pratique

Dans votre `script.js` :
1.  Créez une fonction `afficherTableMultiplication` qui prend un nombre en paramètre et qui utilise une boucle `for` pour afficher sa table de multiplication. Appelez-la avec différents nombres (ex: `afficherTableMultiplication(5)`, `afficherTableMultiplication(9)`).
2.  Créez une fonction `calculerPrixTTC` qui prend un prix HT en paramètre. À l'intérieur, calculez le prix TTC (prix HT * 1.20) et utilisez `return` pour le renvoyer.
3.  Appelez cette fonction et stockez le résultat dans une variable que vous afficherez ensuite dans la console.

#### Mini-Exercice du Jour

Créez une fonction `estMajeur` qui prend un `age` en paramètre. À l'intérieur, utilisez une condition `if/else`. Si l'âge est supérieur ou égal à 18, la fonction doit `return true`. Sinon, elle doit `return false`. Testez votre fonction en affichant le résultat de `estMajeur(25)` et `estMajeur(15)` dans la console.

#### Synthèse

Votre code est maintenant beaucoup plus organisé, lisible et réutilisable. Vous ne violez plus le principe DRY ("Don't Repeat Yourself"). Vous possédez toutes les briques logiques pour construire notre premier projet. Demain, on assemble tout !

---

### J5 (Vendredi) : Projet de la Semaine - Le Jeu du "Plus ou Moins"

**Objectif(s) du Jour :**
- Combiner variables, conditions, boucles et fonctions pour créer un programme complet.
- Apprendre à générer un nombre aléatoire.
- Apprendre à demander une saisie à l'utilisateur.
- Finaliser le projet de la semaine.

**Notion Clé : De la Logique au Programme**
Aujourd'hui, il n'y a pas de nouvelle notion de structure majeure. Le défi est d'utiliser tout ce que vous avez appris pour résoudre un problème concret : créer un jeu. Vous allez devoir traduire une logique humaine ("le nombre est trop grand", "tu as gagné") en code JavaScript.

---

#### Leçon - Les Outils du Jour

##### 1. Demander une Saisie à l'Utilisateur : `prompt()`
La fonction `prompt()` affiche une petite fenêtre demandant à l'utilisateur de taper quelque chose. Elle renvoie ce que l'utilisateur a tapé sous forme de **String**.
Attention, il faudra convertir ce String en Nombre avec `parseInt()`.

```javascript
const reponse = prompt("Quel âge avez-vous ?");
const age = parseInt(reponse); // Convertit "30" en 30
```

##### 2. Générer un Nombre Aléatoire : `Math.random()` et `Math.floor()`
- `Math.random()` : Renvoie un nombre décimal aléatoire entre 0 (inclus) et 1 (exclu).
- `Math.floor()` : Arrondit un nombre à l'entier inférieur.

Pour obtenir un nombre entier aléatoire entre 1 et 100 :
```javascript
const nombreAleatoire = Math.floor(Math.random() * 100) + 1;
```

---

#### PROJET DE LA SEMAINE : Le Jeu du "Plus ou Moins" dans la Console

**La Mission :**
Créez un script qui réalise un jeu du "Juste Prix" entièrement dans la console et avec des `prompt`.

**Logique du Jeu / Cahier des Charges :**
1.  Le programme choisit un nombre aléatoire entre 1 et 100 et le stocke dans une constante `nombreSecret`.
2.  Le programme demande à l'utilisateur "Devinez le nombre entre 1 et 100" via un `prompt`.
3.  Il entre ensuite dans une boucle `while`. La boucle doit continuer **tant que** le nombre de l'utilisateur n'est pas égal au `nombreSecret`.
4.  À l'intérieur de la boucle :
    a.  Comparez le nombre de l'utilisateur au `nombreSecret`.
    b.  Si le nombre de l'utilisateur est plus petit, affichez "C'est plus !" avec `alert()` ou `console.log()` et demandez-lui un nouveau nombre.
    c.  Si le nombre de l'utilisateur est plus grand, affichez "C'est moins !" et demandez-lui un nouveau nombre.
5.  Une fois sorti de la boucle (ce qui signifie que l'utilisateur a trouvé le bon nombre), affichez "Bravo, vous avez trouvé ! Le nombre était bien [nombreSecret]".

**Bonus :**
- Comptez le nombre de tentatives et affichez-le à la fin.
- Limitez le nombre de tentatives (ex: 7 vies) et affichez "Perdu !" si l'utilisateur n'a pas trouvé à temps.

**Livrable :** Votre fichier `script.js` contenant le jeu fonctionnel, déposé sur votre dépôt GitHub.

#### Synthèse Finale de la Semaine

**FÉLICITATIONS !** En une semaine, vous êtes passé de "qu'est-ce que le code ?" à la création d'un programme logique et interactif. Vous avez manipulé les concepts fondamentaux qui sont la base de TOUS les langages de programmation. Vous avez stocké de l'information, pris des décisions, répété des actions et organisé votre code.

La semaine prochaine, nous allons prendre ces super-pouvoirs et les appliquer là où ça devient vraiment amusant : la page web elle-même. Nous allons apprendre à manipuler le HTML et le CSS avec JavaScript, pour faire apparaître, disparaître et bouger des éléments en direct. Préparez-vous à rendre vos pages vivantes 