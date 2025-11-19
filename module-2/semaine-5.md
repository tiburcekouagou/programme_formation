## Semaine 5 : Gérer des Collections de Données - Fonctions, Tableaux & Objets

### J1 (Lundi) : Les Objets, ou la Carte d'Identité de vos Données

**Objectif(s) du Jour :**
- Comprendre pourquoi on a besoin de regrouper des informations liées.
- Créer un objet littéral pour représenter une entité unique.
- Accéder aux propriétés d'un objet en utilisant la notation pointée et la notation par crochets.
- Modifier et ajouter des propriétés à un objet.

**Notion Clé : L'Étiquette sur la Boîte**
Jusqu'à présent, pour décrire un utilisateur, vous aviez besoin de plusieurs variables : `const nomUtilisateur = "Alice"`, `const ageUtilisateur = 30`, `const emailUtilisateur = "alice@mail.com"`. C'est comme avoir des post-it séparés pour chaque information. Un **objet** est une structure de données qui permet de regrouper toutes ces informations liées dans une seule "boîte", une seule variable, sous la forme de paires `clé: valeur`. C'est comme une carte d'identité : toutes les infos sur une personne au même endroit.

---

#### Leçon

##### 1. Créer un Objet Littéral
Un objet est délimité par des accolades `{}`. À l'intérieur, on liste les paires `clé: valeur`, séparées par des virgules. La clé est le nom de la propriété (souvent un mot sans guillemets), la valeur peut être de n'importe quel type (String, Number, Boolean, et même un autre objet ou un tableau !).

```javascript
const utilisateur = {
  nom: "Alice",
  age: 30,
  estAdmin: false,
  ville: "Paris"
};
```

##### 2. Accéder aux Propriétés
- **Notation pointée (`.`):** La plus simple et la plus courante.
  ```javascript
  console.log(utilisateur.nom); // Affiche "Alice"
  console.log(utilisateur.age);  // Affiche 30
  ```
- **Notation par crochets (`[]`):** Obligatoire si la clé contient des espaces ou des caractères spéciaux, ou si le nom de la clé est stocké dans une variable.
  ```javascript
  console.log(utilisateur["ville"]); // Affiche "Paris"
  
  const cleAAcceder = "estAdmin";
  console.log(utilisateur[cleAAcceder]); // Affiche false
  ```

##### 3. Modifier et Ajouter des Propriétés
Même si un objet est déclaré avec `const`, on peut modifier ses propriétés internes.

```javascript
const voiture = {
  marque: "Renault",
  modele: "Clio"
};

// Modifier une propriété existante
voiture.modele = "Megane";

// Ajouter une nouvelle propriété
voiture.couleur = "rouge";

console.log(voiture); // Affiche { marque: "Renault", modele: "Megane", couleur: "rouge" }
```

---

#### Mise en Pratique

1.  Dans un nouveau fichier `script.js`, créez un objet `film` qui représente votre film préféré. Il doit contenir au moins les propriétés suivantes : `titre` (String), `annee` (Number), `realisateur` (String), et `vu` (Boolean).
2.  Affichez une phrase dans la console qui utilise plusieurs propriétés de votre objet. Exemple : `console.log("Le film " + film.titre + " réalisé par " + film.realisateur + " est sorti en " + film.annee + ".");`
3.  Modifiez la propriété `vu` pour la passer à `true` (si elle était `false`).
4.  Ajoutez une nouvelle propriété `note` (un nombre sur 10) à votre objet `film`. Affichez l'objet entier dans la console pour voir les changements.

#### Mini-Exercice du Jour

Créez un objet `personnageJeu` avec les propriétés `nom`, `niveau` (un nombre), et `pointsDeVie` (un nombre). Simulez une attaque : diminuez les `pointsDeVie` du personnage. Simulez une montée de niveau : augmentez le `niveau` du personnage de 1. Affichez l'objet `personnageJeu` après chaque modification.

#### Synthèse

Vous savez maintenant structurer des données complexes pour représenter une seule entité. Les objets sont partout en JavaScript, c'est une notion fondamentale. Demain, nous allons voir comment gérer non pas une, mais une **liste** de ces entités avec les tableaux.

---

### J2 (Mardi) : Les Tableaux, pour Gérer des Listes

**Objectif(s) du Jour :**
- Créer un tableau pour stocker une liste d'éléments.
- Accéder aux éléments d'un tableau via leur index.
- Connaître la propriété `.length` pour savoir la taille du tableau.
- Ajouter et supprimer des éléments d'un tableau (`push`, `pop`).
- Itérer sur un tableau avec une boucle `for`.

**Notion Clé : Le Rayon de Supermarché**
Si un objet est une carte d'identité, un **tableau** (Array) est un rayon de supermarché. Il contient une collection ordonnée d'articles. Chaque article a une place précise, un **index**, qui commence toujours à **zéro**. Le premier article est à l'index 0, le deuxième à l'index 1, etc. Un tableau peut contenir n'importe quoi : des Strings, des Numbers, et même des objets !

---

#### Leçon

##### 1. Créer un Tableau
Un tableau est délimité par des crochets `[]`. Les éléments sont séparés par des virgules.

```javascript
const fruits = ["Pomme", "Banane", "Fraise"];
const nombres = [1, 2, 3, 5, 8];
const utilisateurs = [ // Un tableau d'objets !
  { nom: "Alice", age: 30 },
  { nom: "Bob", age: 25 }
];
```

##### 2. Accéder aux Éléments
On utilise l'index de l'élément entre crochets.

```javascript
console.log(fruits[0]); // Affiche "Pomme" (le premier élément)
console.log(fruits[2]); // Affiche "Fraise"
console.log(utilisateurs[1].nom); // Affiche "Bob"
```

##### 3. Propriétés et Méthodes de Base
- `.length` : Donne le nombre d'éléments dans le tableau.
- `.push(element)` : Ajoute un élément à la **fin** du tableau.
- `.pop()` : Supprime et renvoie le **dernier** élément du tableau.

```javascript
const couleurs = ["rouge", "vert"];
console.log(couleurs.length); // Affiche 2

couleurs.push("bleu");
console.log(couleurs); // Affiche ["rouge", "vert", "bleu"]

couleurs.pop();
console.log(couleurs); // Affiche ["rouge", "vert"]
```

##### 4. Parcourir un Tableau avec une Boucle
La boucle `for` est parfaite pour passer en revue chaque élément d'un tableau.

```javascript
const animaux = ["chat", "chien", "poisson"];

for (let i = 0; i < animaux.length; i++) {
  console.log("L'animal à l'index " + i + " est un " + animaux[i]);
}
```

---

#### Mise en Pratique

1.  Créez un tableau `listeDeCourses` contenant 3 chaînes de caractères.
2.  Affichez le premier et le dernier élément de la liste dans la console.
3.  Ajoutez "Chocolat" à la fin de votre liste avec `.push()`.
4.  Écrivez une boucle `for` qui parcourt votre `listeDeCourses` et affiche chaque élément dans la console, préfixé par "Il faut acheter : ".

#### Mini-Exercice du Jour

Créez un tableau d'objets `etudiants`. Chaque objet doit avoir un `nom` et une `note`. Le tableau doit contenir au moins 3 étudiants. Écrivez une boucle `for` qui parcourt le tableau. Pour chaque étudiant, affichez une phrase comme : "[Nom de l'étudiant] a eu la note de [note de l'étudiant]".

#### Synthèse

Vous pouvez maintenant gérer des collections de données. La combinaison d'objets (pour la structure) et de tableaux (pour les listes) est le fondement de la quasi-totalité des applications web. Demain, nous allons découvrir des méthodes de tableau beaucoup plus puissantes et modernes que la simple boucle `for`.

---

### J3 (Mercredi) : Méthodes de Tableau Modernes (forEach, map, filter)

**Objectif(s) du Jour :**
- Découvrir des manières plus déclaratives de parcourir un tableau.
- Utiliser `.forEach()` comme alternative à la boucle `for`.
- Utiliser `.map()` pour transformer chaque élément d'un tableau en un nouveau tableau.
- Utiliser `.filter()` pour créer un nouveau tableau contenant uniquement les éléments qui passent un test.
- Comprendre le concept de "fonction de callback".

**Notion Clé : L'Usine de Traitement**
Imaginez vos données comme des objets sur un tapis roulant. Les méthodes de tableau modernes sont des machines spécialisées :
- `.forEach()` est un **inspecteur** : il regarde chaque objet passer, mais ne modifie pas le tapis roulant.
- `.map()` est une **presse** : il prend chaque objet, le transforme en quelque chose de nouveau (ex: le peint en rouge) et le met sur un **nouveau** tapis roulant.
- `.filter()` est un **trieur** : il regarde chaque objet et, s'il correspond à un critère, le déplace sur un **nouveau** tapis roulant.
Ces méthodes prennent en paramètre une "fonction de callback", qui est la notice d'instruction pour la machine.

---

#### Leçon

Une **fonction de callback** est simplement une fonction que l'on passe en argument à une autre fonction.

##### 1. `.forEach(callback)` - Pour Parcourir
Similaire à une boucle `for`, mais souvent plus lisible.

```javascript
const fruits = ["Pomme", "Banane", "Fraise"];
fruits.forEach(function(fruit) {
  console.log(fruit);
});
```

##### 2. `.map(callback)` - Pour Transformer
Crée un **nouveau** tableau de même taille, où chaque élément est le résultat de la fonction de callback.

```javascript
const nombres = [1, 2, 3, 4];
const carres = nombres.map(function(nombre) {
  return nombre * nombre;
});
// carres vaut maintenant [1, 4, 9, 16]
// Le tableau 'nombres' n'a pas été modifié.
```

##### 3. `.filter(callback)` - Pour Sélectionner
Crée un **nouveau** tableau contenant uniquement les éléments pour lesquels la fonction de callback a renvoyé `true`.

```javascript
const nombres = [10, 5, 22, 8, 17];
const nombresSupA10 = nombres.filter(function(nombre) {
  return nombre > 10;
});
// nombresSupA10 vaut maintenant [22, 17]
```

---

#### Mise en Pratique

Reprenez le tableau d'objets `etudiants` de l'exercice d'hier.
1.  Réécrivez la boucle `for` qui affichait les noms et les notes en utilisant `.forEach()`.
2.  Utilisez `.map()` pour créer un **nouveau** tableau `nomsEtudiants` qui ne contient que les noms des étudiants.
3.  Utilisez `.filter()` pour créer un **nouveau** tableau `bonsEtudiants` qui ne contient que les étudiants ayant une note supérieure ou égale à 12. Affichez ce nouveau tableau dans la console.

#### Mini-Exercice du Jour

Vous avez un tableau de prix `[20, 15, 50, 45]`.
- Utilisez `.map()` pour créer un nouveau tableau avec tous les prix augmentés de 10%.
- Utilisez `.filter()` pour créer un nouveau tableau contenant uniquement les prix inférieurs à 30.
- Enchaînez les deux : créez un nouveau tableau qui ne contient que les prix inférieurs à 30, auxquels vous avez appliqué une augmentation de 10%.

#### Synthèse

Vous avez appris à manipuler des tableaux de manière plus expressive, plus lisible et moins sujette aux erreurs qu'avec des boucles `for` manuelles. C'est la façon de faire en JavaScript moderne. Demain, nous allons approfondir la notion de fonction et de "portée" (scope).

---

### J4 (Jeudi) : Portée des Variables et Fonctions Fléchées

**Objectif(s) du Jour :**
- Comprendre la différence entre portée globale et portée locale (de fonction).
- Appréhender le concept de "shadowing" (masquage de variable).
- Apprendre la syntaxe des fonctions fléchées (ES6).

**Notion Clé : Les Pièces d'une Maison**
La **portée** (scope) définit où une variable est accessible dans votre code. Imaginez votre programme comme une maison.
- La **portée globale** est le jardin : toute variable déclarée ici est visible depuis n'importe quelle pièce de la maison. C'est à éviter le plus possible pour ne pas créer de conflits.
- Chaque **fonction** est une pièce de la maison (un "scope local"). Une variable déclarée avec `let` ou `const` à l'intérieur d'une pièce n'est visible que dans cette pièce. On ne peut pas y accéder depuis le jardin ou une autre pièce.

---

#### Leçon

##### 1. Portée Globale vs Locale
```javascript
const variableGlobale = "Je suis dans le jardin";

function maFonction() {
  const variableLocale = "Je suis dans le salon";
  console.log(variableGlobale); // OK, on peut voir le jardin depuis le salon.
  console.log(variableLocale);  // OK, on est dans le salon.
}

maFonction();
// console.log(variableLocale); // ERREUR ! On est dans le jardin, on ne peut pas voir dans le salon.
```

##### 2. Le "Shadowing"
Si une variable locale a le même nom qu'une variable globale, elle a la priorité à l'intérieur de la fonction.

```javascript
let nom = "Alice"; // Globale

function autreFonction() {
  let nom = "Bob"; // Locale, elle "masque" la variable globale
  console.log(nom); // Affiche "Bob"
}

autreFonction();
console.log(nom); // Affiche "Alice"
```

##### 3. Les Fonctions Fléchées (Arrow Functions)
C'est une syntaxe plus courte et plus moderne pour écrire des fonctions, introduite avec ES6. Elle est particulièrement pratique pour les fonctions de callback.

```javascript
// Fonction classique
const addition = function(a, b) {
  return a + b;
};

// Équivalent en fonction fléchée
const additionFlechee = (a, b) => {
  return a + b;
};

// Si la fonction ne fait qu'un 'return', on peut encore la raccourcir :
const additionUltraCourte = (a, b) => a + b;
```

---

#### Mise en Pratique

1.  Réécrivez toutes les fonctions de callback que vous avez utilisées hier avec `.map()` et `.filter()` en utilisant la syntaxe des fonctions fléchées.
    ```javascript
    // Avant
    const carres = nombres.map(function(nombre) {
      return nombre * nombre;
    });

    // Après
    const carres = nombres.map(nombre => nombre * nombre);
    ```
2.  Déclarez une variable globale `let score = 100;`. Créez une fonction `jouerManche` qui déclare une variable locale `score` à 10 et l'affiche. En dehors de la fonction, affichez à nouveau la variable `score` globale pour vérifier qu'elle n'a pas été modifiée.

#### Mini-Exercice du Jour

Créez un tableau de noms. Utilisez `.filter()` avec une fonction fléchée pour ne garder que les noms qui ont plus de 4 lettres. Utilisez `.map()` avec une fonction fléchée pour transformer chaque nom restant en sa version en majuscules (indice : `nom.toUpperCase()`).

#### Synthèse

Vous comprenez maintenant un concept fondamental de la programmation, la portée, qui vous évitera de nombreux bugs. Vous maîtrisez également la syntaxe moderne des fonctions fléchées, ce qui rendra votre code plus concis. Demain, nous assemblons tout cela dans le projet de la semaine.

---

### J5 (Vendredi) : Projet de la Semaine - Gestionnaire de Contacts en Console

**Objectif(s) du Jour :**
- Synthétiser l'utilisation des objets, tableaux, fonctions, boucles et conditions.
- Structurer un petit programme modulaire.
- Manipuler un tableau d'objets (ajouter, lister, supprimer).

**Notion Clé : Le Cycle de Vie des Données (CRUD en Mémoire)**
Ce projet est une simulation en miniature de ce que font toutes les applications : **C**reate (créer), **R**ead (lire), **U**pdate (mettre à jour), **D**elete (supprimer) des données. Ici, notre "base de données" sera un simple tableau JavaScript qui vit en mémoire. Vous allez devoir créer des fonctions pour chaque opération, qui modifient ce tableau.

---

#### PROJET DE LA SEMAINE : Gestionnaire de Contacts

**La Mission :**
Créez un script qui simule un gestionnaire de contacts. Le programme doit proposer un menu et permettre à l'utilisateur d'interagir jusqu'à ce qu'il décide de quitter.

**Cahier des Charges :**
1.  **La Structure de Données :**
    - Au début de votre script, créez un tableau `contacts` qui contiendra des objets.
    - Chaque objet contact doit avoir une propriété `nom` et une propriété `prenom`.

2.  **L'Architecture du Programme :**
    - Votre programme doit être organisé en fonctions : `afficherMenu()`, `ajouterContact()`, `listerContacts()`, `supprimerContact()`.
    - Le corps principal du programme sera une boucle `while` qui continue tant que l'utilisateur n'a pas choisi de quitter.
    - À chaque tour de boucle, le menu s'affiche, le programme demande à l'utilisateur de choisir une option, puis appelle la fonction correspondante.

3.  **Les Fonctionnalités :**
    - **Lister les contacts :** La fonction `listerContacts()` doit parcourir le tableau `contacts` et afficher chaque contact dans la console (ex: "Nom : Dupont, Prénom : Jean"). Si la liste est vide, elle doit afficher "Votre liste de contacts est vide.".
    - **Ajouter un contact :** La fonction `ajouterContact()` doit :
      a. Demander le nom et le prénom de l'utilisateur via deux `prompt`.
      b. Créer un nouvel objet contact avec ces informations.
      c. Ajouter ce nouvel objet au tableau `contacts` avec `.push()`.
      d. Afficher un message de confirmation.
    - **Supprimer un contact (Version Simplifiée) :** La fonction `supprimerContact()` peut simplement utiliser `.pop()` pour supprimer le dernier contact ajouté.
    - **Quitter :** Si l'utilisateur choisit cette option, la boucle `while` doit s'arrêter et le programme doit afficher "Au revoir !".

**Livrable :** Votre fichier `script.js` contenant le gestionnaire de contacts fonctionnel, déposé sur votre dépôt GitHub.

**Bonus (pour les plus rapides) :**
- Améliorez la fonction `supprimerContact()` : demandez l'index du contact à supprimer, et utilisez la méthode `.splice(index, 1)` pour le retirer du tableau.
- Utilisez `alert()` pour les messages à l'utilisateur et `console.log()` uniquement pour lister les contacts, pour une meilleure expérience.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez fait un bond de géant. Vous ne manipulez plus seulement des variables simples, mais de véritables structures de données organisées. Vous savez comment créer des listes d'objets complexes et comment les traiter de manière moderne et efficace. Ce que vous avez fait avec ce gestionnaire de contacts (ajouter, lister, supprimer) est exactement le cœur logique de milliards d'applications web.

La semaine prochaine, nous allons enfin faire le lien entre la puissance de JavaScript et le monde visuel du HTML/CSS. Nous allons apprendre à manipuler le DOM, c'est-à-dire à utiliser JS pour créer, modifier et supprimer des éléments HTML en direct sur la page. Fini la console, place à l'interactivité 