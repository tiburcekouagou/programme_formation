## Semaine 2 : Les Bases de CSS3

### J1 (Lundi) : Lier CSS et Cibler des Éléments

**Objectif(s) du Jour :**
- Comprendre la "Séparation des Préoccupations" (HTML pour la structure, CSS pour le style).
- Créer et lier une feuille de style externe à un fichier HTML.
- Utiliser les sélecteurs de base pour cibler et styliser des éléments : balise, classe, et ID.

**Notion Clé : La Séparation des Préoccupations**
Imaginez un acteur. Son texte, c'est le HTML : le contenu, le sens. Son costume, son maquillage, sa coiffure, c'est le CSS : l'apparence. On ne mélange pas le texte et le costume dans le même document. En web, c'est pareil : on garde le HTML propre (la structure) et on gère tout le style dans un fichier `.css` séparé. C'est une pratique professionnelle fondamentale qui rend les projets plus faciles à maintenir.

---

#### Leçon

##### 1. Lier un fichier CSS
Pour que notre HTML sache quel fichier CSS utiliser, on ajoute une balise `<link>` à l'intérieur de la section `<head>` de notre document HTML.

```html
<!-- Dans votre fichier .html, à l'intérieur de <head> -->
<head>
  <meta charset="UTF-8">
  <title>Ma Recette</title>
  <link rel="stylesheet" href="style.css"> <!-- Voici la ligne magique ! -->
</head>
```
Cette ligne dit au navigateur : "Pour styliser cette page, va chercher et applique les règles que tu trouveras dans le fichier `style.css`".

##### 2. Syntaxe d'une Règle CSS
Une règle CSS est toujours composée de la même manière : un **sélecteur** et un **bloc de déclaration** entre accolades `{}`. Chaque déclaration contient une **propriété** et une **valeur**.

```css
sélecteur {
  propriété: valeur;
  autre-propriété: autre-valeur;
}
```

##### 3. Les Sélecteurs Fondamentaux
- **Sélecteur de balise :** Cible *tous* les éléments d'un certain type.
  ```css
  /* Cible toutes les balises <p> de la page */
  p {
    color: green;
  }
  ```
- **Sélecteur de classe :** Cible les éléments qui ont un attribut `class` spécifique. Une classe peut être utilisée sur plusieurs éléments. C'est le sélecteur le plus courant et le plus utile.
  ```html
  <h2 class="section-title">Ingrédients</h2>
  ```
  ```css
  /* Cible tous les éléments avec la classe "section-title" */
  .section-title {
    text-decoration: underline;
  }
  ```
- **Sélecteur d'ID :** Cible l'élément **unique** qui a cet attribut `id`. Un ID ne doit être utilisé qu'une seule fois par page.
  ```html
  <header id="main-header">...</header>
  ```
  ```css
  /* Cible l'élément avec l'ID "main-header" */
  #main-header {
    background-color: lightgray;
  }
  ```

---

#### Mise en Pratique

1.  Ouvrez le dossier de votre projet de la semaine 1 (`bootcamp-projet-1`).
2.  Créez un nouveau fichier nommé `style.css` à côté de votre fichier `recette.html` (ou `cv.html`).
3.  Dans votre fichier HTML, ajoutez la balise `<link>` dans le `<head>` pour lier votre nouveau fichier CSS.
4.  Dans `style.css`, écrivez votre première règle pour vérifier que le lien fonctionne. Par exemple :
    ```css
    body {
      background-color: #f5f5f5; /* Un gris très clair */
    }
    ```
5.  Enregistrez les deux fichiers et rafraîchissez votre page dans le navigateur. Le fond devrait avoir changé de couleur !
6.  Ajoutez une classe `important` à un `<li>` de votre liste d'ingrédients dans le HTML. Puis, dans le CSS, créez une règle pour `.important` qui met le texte en rouge.

#### Mini-Exercice du Jour

Créez un fichier `test-selecteurs.html` avec le contenu suivant :
```html
<h1>Titre Principal</h1>
<p class="intro">Paragraphe d'introduction.</p>
<p>Un autre paragraphe.</p>
<div id="conclusion">Conclusion unique.</div>
```
Liez un nouveau fichier `test.css`. Dans ce CSS, écrivez des règles pour :
- Mettre tous les `<p>` en gris.
- Mettre uniquement le paragraphe avec la classe `intro` en italique.
- Mettre uniquement le `div` avec l'ID `conclusion` avec un fond jaune.

#### Synthèse

Vous avez établi le pont entre la structure et le style. Vous savez maintenant comment "viser" n'importe quel élément de votre page pour le modifier. Demain, nous allons explorer le large éventail de propriétés pour changer les couleurs et la typographie.

---

### J2 (Mardi) : L'Art de la Typographie et des Couleurs

**Objectif(s) du Jour :**
- Maîtriser les différentes façons de définir une couleur en CSS.
- Changer la police, la taille, et la graisse du texte.
- Améliorer la lisibilité avec l'interlignage et l'alignement.

**Notion Clé : Le Design est à 95% de la Typographie**
Sur le web, le contenu est majoritairement textuel. Un choix judicieux de polices, de tailles et de couleurs peut transformer une page illisible en une expérience de lecture agréable et professionnelle. C'est l'un des leviers les plus puissants pour améliorer un design.

---

#### Leçon

##### 1. Définir les Couleurs
- `color` : Change la couleur du texte.
- `background-color` : Change la couleur de l'arrière-plan d'un élément.

Il existe plusieurs formats pour les couleurs :
- **Noms de couleur :** `red`, `blue`, `lightseagreen` (simple, mais limité).
- **HEX (Hexadécimal) :** `#RRGGBB`. Le format le plus courant. Ex: `#FF0000` pour rouge, `#000000` pour noir. `#333` est un raccourci pour `#333333`.
- **RGB :** `rgb(255, 0, 0)` pour rouge. `rgba(255, 0, 0, 0.5)` ajoute un canal alpha pour la transparence (0.5 = 50% transparent).

##### 2. Les Propriétés de Typographie
- `font-family` : Définit la police. On liste plusieurs polices (une "pile") au cas où la première ne serait pas installée sur l'ordinateur de l'utilisateur.
  ```css
  font-family: "Helvetica Neue", Arial, sans-serif;
  ```
- `font-size` : La taille de la police. Ex: `16px`, `1.2em`, `1rem`. Pour l'instant, `px` (pixels) est le plus simple à comprendre.
- `font-weight` : La graisse de la police. `normal` (400), `bold` (700), ou des valeurs numériques.
- `line-height` : L'interlignage. Une valeur sans unité comme `1.6` est recommandée pour la lisibilité (signifie 1.6 fois la taille de la police).
- `text-align` : Aligne le texte. `left`, `right`, `center`, `justify`.

- **Exemple de Code :**
  ```css
  body {
    font-family: Georgia, serif;
    font-size: 18px;
    line-height: 1.6;
    color: #333333; /* Un gris foncé, plus doux pour les yeux que le noir pur */
  }
  
  h1 {
    font-family: "Lucida Grande", sans-serif;
    color: #A52A2A; /* Brun-rouge */
    font-size: 48px;
    text-align: center;
  }
  ```

---

#### Mise en Pratique

Reprenez vos fichiers `recette.html` et `style.css`.
1.  Dans `style.css`, définissez des styles de base pour `body` : une police `font-family` pour la lecture (ex: `Georgia, serif`), une couleur de texte `color` et un `line-height`.
2.  Ciblez votre `<h1>` et donnez-lui une police différente (ex: `Arial, sans-serif`), une taille plus grande (`font-size`), une couleur de votre choix et centrez-le.
3.  Ciblez les `<h2>` et changez leur couleur pour qu'elle corresponde à celle du `<h1>`.
4.  Visitez [Google Fonts](https://fonts.google.com/), choisissez une police qui vous plaît et suivez leurs instructions pour l'importer dans votre CSS et l'appliquer à vos titres.

#### Mini-Exercice du Jour

Créez une classe `.citation` dans votre CSS. Appliquez-la à un `<p>` dans votre HTML. Cette classe doit :
- Mettre le texte en italique (`font-style: italic;`).
- Le centrer (`text-align: center;`).
- Lui donner une couleur grise (`color: #777;`).

#### Synthèse

Vous savez maintenant contrôler l'aspect visuel fondamental de votre page. Elle est déjà beaucoup plus personnelle et lisible. Demain, nous allons aborder LE concept central de la mise en page CSS : le Modèle de Boîte (Box Model).

---

### J3 (Mercredi) : Le Modèle de Boîte (Box Model)

**Objectif(s) du Jour :**
- Comprendre les 4 couches du Box Model : contenu, `padding`, `border`, `margin`.
- Utiliser ces propriétés pour gérer les espacements.
- Adopter la bonne pratique `box-sizing: border-box`.

**Notion Clé : Tout est une Boîte**
En CSS, chaque élément HTML est traité comme une boîte rectangulaire. Cette boîte a plusieurs couches, comme une poupée russe. De l'intérieur vers l'extérieur, on trouve : le contenu (texte, image), la marge intérieure (`padding`), la bordure (`border`), et la marge extérieure (`margin`). Maîtriser ce concept est absolument essentiel pour faire de la mise en page.

---

#### Leçon

##### 1. Les 4 Couches

- **Content :** La zone où votre texte et vos images apparaissent.
- **`padding` :** L'espace *entre* le contenu et la bordure. C'est la marge intérieure de la boîte.
- **`border` :** La bordure qui entoure le `padding` et le contenu.
- **`margin` :** L'espace *à l'extérieur* de la bordure. C'est ce qui pousse les autres boîtes.

![Visualisation du Box Model](https://developer.mozilla.org/en-US/docs/Learn/CSS/Building_blocks/The_box_model/box-model.png)

##### 2. La Propriété `box-sizing`

Par défaut, si vous donnez à une boîte une `width: 200px` et un `padding: 20px`, sa largeur totale sera de 240px ! C'est contre-intuitif. La bonne pratique moderne est de dire au navigateur d'inclure le `padding` et la `border` dans la largeur définie.

```css
/* Cette règle est à mettre au début de presque tous vos projets CSS */
* {
  box-sizing: border-box;
}
```
Avec cette règle, une boîte de `width: 200px` fera *toujours* 200px de large, peu importe son `padding` ou sa `border`.

- **Exemple de Code :**
  ```css
  .card {
    width: 500px;
    padding: 25px; /* 25px d'espace tout autour à l'intérieur */
    border: 1px solid #ccc; /* Une bordure grise fine */
    margin: 20px; /* 20px d'espace tout autour à l'extérieur */
  }

  /* Pour centrer un bloc sur la page, on utilise une astuce de marge : */
  .centered-container {
    width: 80%; /* Prend 80% de la largeur de son parent */
    margin-left: auto;
    margin-right: auto;
    /* Raccourci : margin: 0 auto; (0 en haut/bas, auto à gauche/droite) */
  }
  ```

---

#### Mise en Pratique

Sur votre projet `recette.html` / `style.css` :
1.  Ajoutez la règle `* { box-sizing: border-box; }` au tout début de votre CSS.
2.  Ciblez la balise `<main>` (ou donnez-lui une classe `.container`). Donnez-lui une largeur (`width`) maximale (ex: `800px`) et centrez-la avec la technique `margin: 0 auto;`.
3.  Pour que le texte ne soit pas collé aux bords de ce conteneur, ajoutez-lui du `padding` (ex: `40px`).
4.  Ajoutez une bordure (`border`) fine et une couleur de fond (`background-color: white;`) à ce conteneur pour le faire ressortir.

#### Mini-Exercice du Jour

Créez deux `<div>` dans une page HTML. Donnez-leur une classe `.box`. Dans le CSS, donnez à `.box` une largeur, une hauteur, une couleur de fond et une `border`. Utilisez `margin` pour créer de l'espace *entre* les deux boîtes. Utilisez `padding` pour créer de l'espace *à l'intérieur* de chaque boîte.

#### Synthèse

Vous comprenez maintenant comment les éléments occupent de l'espace. Vous pouvez contrôler les marges intérieures et extérieures, ce qui est la base de toute mise en page. Demain, nous allons styliser davantage nos boîtes et les rendre interactives.

---

### J4 (Jeudi) : Habiller la Boîte et la Rendre Interactive

**Objectif(s) du Jour :**
- Styliser les bordures (arrondis, style...).
- Appliquer des images d'arrière-plan.
- Découvrir les pseudo-classes pour rendre les éléments interactifs (ex: au survol).

**Notion Clé : Le Feedback Visuel**
Une bonne interface utilisateur donne un retour à l'utilisateur. Quand il passe sa souris sur un élément cliquable, celui-ci doit réagir. C'est ce qu'on appelle le "feedback". Les pseudo-classes CSS, comme `:hover`, sont le moyen le plus simple et le plus courant de créer ce feedback essentiel.

---

#### Leçon

##### 1. Styliser les Bordures
- `border-radius` : Permet d'arrondir les coins d'une boîte. Une valeur élevée peut rendre un carré complètement rond.
- `border-style` : `solid`, `dashed`, `dotted`...
- `box-shadow` : Ajoute une ombre portée à une boîte, lui donnant un effet de profondeur.
  ```css
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1); 
  /* Décalage X, Décalage Y, Flou, Couleur (ici noir à 10% d'opacité) */
  ```

##### 2. Les Arrière-plans
- `background-image` : Permet de mettre une image en fond.
- `background-size` : `cover` (l'image couvre toute la zone, quitte à être coupée) ou `contain` (l'image est entièrement visible, quitte à laisser des bandes vides).
- `background-position` : `center`, `top`, etc.

##### 3. Les Pseudo-classes
Une pseudo-classe cible un état particulier d'un élément.
- `:hover` : L'élément est survolé par la souris.
- `:focus` : L'élément a le focus (ex: un champ de formulaire dans lequel on est en train de taper).
- `:active` : L'élément est en train d'être cliqué.

- **Exemple de Code :**
  ```css
  .button {
    display: inline-block; /* Pour que le padding s'applique correctement */
    padding: 10px 20px;
    background-color: #007bff;
    color: white;
    text-decoration: none; /* Enlève le soulignement des liens */
    border-radius: 5px;
  }
  
  .button:hover {
    background-color: #0056b3; /* Une couleur plus foncée au survol */
  }
  ```

---

#### Mise en Pratique

Sur votre projet :
1.  Ajoutez un `border-radius` (ex: `8px`) à votre conteneur principal pour adoucir les angles.
2.  Ajoutez un `box-shadow` subtil à ce même conteneur pour le décoller du fond.
3.  Ciblez tous les liens (`a`) de votre page. Enlevez leur soulignement par défaut (`text-decoration: none;`) et changez leur couleur.
4.  Créez une règle `a:hover` qui fait réapparaître le soulignement au survol.
5.  Stylisez le bouton "Envoyer" de votre formulaire pour qu'il ressemble à un vrai bouton (fond, couleur de texte, padding, pas de bordure, `border-radius`). Ajoutez un effet `:hover`.

#### Mini-Exercice du Jour

Créez un simple lien HTML. En utilisant uniquement CSS, transformez-le pour qu'il ressemble à un bouton rond avec une icône (vous pouvez utiliser un emoji pour l'icône). Le bouton doit changer de couleur et grossir légèrement au survol (utilisez la propriété `transform: scale(1.1);` dans le `:hover`).

#### Synthèse

Votre page n'est plus seulement statique, elle est devenue interactive ! Vous savez créer des effets visuels qui améliorent grandement l'expérience utilisateur. Demain, nous consolidons tout cela et nous abordons des notions un peu plus théoriques mais cruciales pour le dépannage.

---

### J5 (Vendredi) : Consolidation et Projet de la Semaine

**Objectif(s) du Jour :**
- Appliquer toutes les connaissances de la semaine au projet.
- Comprendre les notions de "Cascade" et de "Spécificité".
- Finaliser un projet HTML+CSS stylisé.

**Notion Clé : La Cascade et la Spécificité**
Pourquoi CSS s'appelle **Cascading** Style Sheets ? Parce que les styles "cascadent" ou "coulent" de haut en bas. Une règle peut en écraser une autre. La **spécificité** est la règle du jeu qui détermine quel style gagne en cas de conflit. Comprendre cela vous évitera 90% des maux de tête en CSS ("Pourquoi mon style ne s'applique pas ?!").

---

#### Leçon

##### 1. La Cascade
Les styles viennent de plusieurs sources (navigateur, vos fichiers CSS...). Les vôtres sont généralement les derniers appliqués et donc les plus forts. De plus, si vous écrivez deux règles identiques dans votre fichier, c'est la dernière qui gagne.

##### 2. La Spécificité
C'est un score que le navigateur calcule pour chaque sélecteur. Le sélecteur avec le plus haut score l'emporte.
- **ID (`#mon-id`) :** Le plus fort. Vaut 100 points.
- **Classe (`.ma-classe`) et Pseudo-classe (`:hover`) :** Vaut 10 points.
- **Balise (`p`, `div`) :** Le plus faible. Vaut 1 point.

**Exemple de conflit :**
```html
<h1 id="titre" class="page-title">Mon Titre</h1>
```
```css
/* Score : 1 (balise) */
h1 { color: blue; } 

/* Score : 10 (classe) -> Gagne contre le sélecteur de balise */
.page-title { color: green; } 

/* Score : 100 (ID) -> Gagne contre tout le reste ! */
#titre { color: red; } 
```
Le titre sera **ROUGE**, car le sélecteur d'ID est le plus spécifique. C'est pourquoi il faut utiliser les ID avec parcimonie en CSS.

---

#### PROJET DE LA SEMAINE : Mettre en Forme votre Page Sémantique

Votre mission pour aujourd'hui est de transformer le projet HTML de la semaine dernière en une page web esthétiquement agréable en utilisant **toutes** les notions vues cette semaine.

**Sujet :** Le projet de la semaine 1 (`recette.html` ou `cv.html`).

**Checklist des tâches à accomplir :**
1.  **Liaison :** Assurez-vous que votre fichier CSS est correctement lié.
2.  **Fondamentaux :** Ajoutez la règle `* { box-sizing: border-box; }`.
3.  **Palette de Couleurs :** Choisissez 2 ou 3 couleurs principales (une pour le fond, une pour le texte, une "d'accentuation" pour les titres/liens) et appliquez-les.
4.  **Typographie :** Choisissez une police lisible pour le corps du texte et une police d'accompagnement pour les titres. Gérez les tailles et les graisses.
5.  **Mise en page centrale :** Créez un conteneur principal de largeur fixe (ex: `max-width: 900px;`) et centrez-le sur la page.
6.  **Box Model :** Utilisez `padding` pour donner de l'air à votre contenu à l'intérieur du conteneur. Utilisez `margin` pour espacer vos titres et vos sections.
7.  **Finition des "Boîtes" :** Ajoutez des `border-radius` et/ou des `box-shadow` à vos conteneurs principaux (votre `main` ou votre `<article>`) pour un rendu plus moderne.
8.  **Interactivité :** Stylisez tous vos liens et boutons et assurez-vous qu'ils ont un effet `:hover` clair.
9.  **Propreté :** Votre code CSS doit être bien organisé et lisible.

**Livrable :** Poussez sur votre dépôt GitHub le projet mis à jour, contenant à la fois le fichier `.html` et le fichier `.css`.

#### Synthèse Finale de la Semaine

En cinq jours, vous êtes passé d'un document HTML noir et blanc à une page web stylisée, interactive et agréable à lire. Vous avez acquis les outils fondamentaux de la présentation web. Vous savez maintenant contrôler les espacements, les couleurs, la typographie et ajouter des effets simples.

La semaine prochaine, nous aborderons le défi majeur du CSS : créer des mises en page complexes et, surtout, les rendre adaptatives à tous les écrans (mobile, tablette, ordinateur) grâce à Flexbox, Grid et les Media Queries. Préparez-vous à prendre le contrôle total de la disposition de vos éléments.