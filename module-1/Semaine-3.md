## Semaine 3 : Mises en Page Avancées et Responsive Design

### J1 (Lundi) : Le Comportement des Blocs et les Unités Relatives

**Objectif(s) du Jour :**
- Comprendre la propriété `display` et ses valeurs fondamentales (`block`, `inline`, `inline-block`).
- Utiliser `inline-block` pour créer des mises en page simples en colonnes (et comprendre ses limites).
- Découvrir les unités relatives (`em`, `rem`) pour une typographie flexible.

**Notion Clé : Des Briques de Lego différentes**
Imaginez les éléments HTML comme des briques de Lego. Par défaut, certaines briques (`<p>`, `<h1>`, `<div>`) sont de type `block` : elles prennent toute la largeur disponible et se placent les unes en dessous des autres. D'autres (`<a>`, `<span>`, `<strong>`) sont de type `inline` : elles se placent les unes à côté des autres, comme des mots dans une phrase, et n'acceptent pas de `width` ou de `height`. `inline-block` est un hybride : il se place à côté des autres mais accepte des dimensions. Comprendre le type de "brique" que vous manipulez est la base de la mise en page.

---

#### Leçon

##### 1. La Propriété `display`
- `display: block;` : L'élément prend toute la largeur, commence sur une nouvelle ligne. On peut lui donner une `width` et une `height`. (Comportement par défaut des `<div>`, `<p>`, `<h1>`...).
- `display: inline;` : L'élément s'inscrit dans le flux du texte. Ignore `width`, `height`, et les `margin` haut/bas. (Comportement par défaut des `<a>`, `<span>`...).
- `display: inline-block;` : Le meilleur des deux mondes (pour les petites choses). L'élément se place à côté des autres (`inline`) mais on peut lui donner une `width`, une `height`, du `padding` et du `margin` (`block`).

- **Exemple de Code :**
  ```html
  <a href="#">Lien 1</a>
  <a href="#">Lien 2</a>
  ```
  ```css
  a {
    display: inline-block; /* Par défaut, les liens sont inline */
    padding: 10px;
    margin: 5px;
    background-color: lightblue;
  }
  ```
  *Sans `inline-block`, le padding et le margin ne s'appliqueraient pas correctement.*

##### 2. Les Unités Relatives pour le Texte
- `px` (pixels) : Absolu. Un texte de `16px` fera toujours 16 pixels.
- `em` : Relatif à la taille de police de l'**élément parent**. Si le parent fait `20px`, `1.5em` équivaut à 30px.
- `rem` (root em) : Relatif à la taille de police de l'**élément racine** (`<html>`). C'est le **standard moderne** pour une typographie accessible et responsive. Par défaut, `1rem` = `16px`. `2rem` = `32px`.

- **Exemple de Code :**
  ```css
  /* On définit la base sur l'élément racine */
  html {
    font-size: 16px; 
  }
  
  body {
    font-size: 1rem; /* Fait 16px */
  }
  
  h1 {
    font-size: 3rem; /* Fait 3 * 16px = 48px */
  }
  ```

---

#### Mise en Pratique

1.  Reprenez votre projet. Dans votre CSS, changez toutes les unités de `font-size` que vous aviez mises en `px` pour des unités en `rem`. Par exemple, si vous aviez `font-size: 48px;` pour votre `h1`, changez-le en `font-size: 3rem;`. L'apparence ne devrait pas changer, mais votre code est maintenant plus flexible.
2.  Créez un menu de navigation simple dans votre `<header>`.
    ```html
    <nav>
      <a href="#">Accueil</a>
      <a href="#">Recettes</a>
      <a href="#">Contact</a>
    </nav>
    ```
3.  Utilisez `display: inline-block;` sur ces liens pour leur donner du `padding` et les espacer, tout en les gardant sur la même ligne.

#### Mini-Exercice du Jour

Créez 3 `div` avec la classe `.card`. Donnez-leur une largeur fixe (ex: `30%`), une hauteur et une couleur de fond. Utilisez `display: inline-block;` pour tenter de les aligner côte à côte dans un conteneur. Observez les petits espaces indésirables qui apparaissent entre eux (c'est une des raisons pour lesquelles on utilise Flexbox aujourd'hui !).

#### Synthèse

Vous comprenez maintenant le comportement naturel des éléments HTML et comment le modifier. Vous avez aussi adopté une pratique moderne pour la gestion des tailles de police. Demain, nous allons jeter `inline-block` à la poubelle pour la mise en page et découvrir l'outil qui a révolutionné le CSS : Flexbox.

---

### J2 (Mardi) : La Révolution Flexbox (Partie 1)

**Objectif(s) du Jour :**
- Comprendre le concept de conteneur et d'items Flex.
- Transformer un conteneur en conteneur Flex avec `display: flex`.
- Maîtriser les propriétés d'alignement sur l'axe principal (`justify-content`).

**Notion Clé : Les Livres sur une Étagère**
Flexbox fonctionne comme une étagère à livres. Vous désignez une boîte comme étant l'étagère (le conteneur `flex`). Les éléments à l'intérieur deviennent des livres (les `items`). Ensuite, vous donnez des instructions à l'étagère, pas aux livres. Vous pouvez dire : "Répartissez les livres sur toute la longueur" (`justify-content: space-between`), "Rassemblez-les au centre" (`justify-content: center`), etc. C'est un modèle de mise en page **unidimensionnel** (soit une ligne, soit une colonne).

---

#### Leçon

##### 1. Activer Flexbox
La seule chose à faire pour commencer est d'appliquer `display: flex;` à un conteneur parent. Immédiatement, ses enfants directs s'aligneront sur une ligne.

##### 2. L'Axe Principal (Main Axis)
Par défaut, l'axe principal est horizontal. La propriété `justify-content` contrôle l'alignement des items sur cet axe.
- `flex-start` (défaut) : Items regroupés au début.
- `flex-end` : Items regroupés à la fin.
- `center` : Items regroupés au centre.
- `space-between` : Espace maximum entre les items. Le premier est collé au début, le dernier à la fin.
- `space-around` : Espace réparti autour de chaque item (l'espace aux extrémités est la moitié de l'espace entre les items).
- `space-evenly` : Espace parfaitement égal partout, y compris aux extrémités.

- **Exemple de Code :**
  ```html
  <div class="container">
    <div class="item">1</div>
    <div class="item">2</div>
    <div class="item">3</div>
  </div>
  ```
  ```css
  .container {
    display: flex;
    border: 2px solid black;
    padding: 10px;
  }
  .item {
    background-color: dodgerblue;
    color: white;
    padding: 20px;
  }
  
  /* Essayez de changer cette valeur ! */
  .container {
    justify-content: space-between;
  }
  ```

---

#### Mise en Pratique

Reprenez votre projet et le menu de navigation que vous avez créé hier.
1.  Ciblez le parent des liens de navigation (la balise `<nav>`).
2.  Appliquez-lui `display: flex;`. Les liens devraient s'aligner.
3.  Appliquez `justify-content: center;` ou `justify-content: flex-end;` pour déplacer tout le bloc de navigation.
4.  Dans votre `<header>`, vous avez probablement un `<h1>` et une `<nav>`. Ciblez le `<header>` et appliquez-lui `display: flex;` et `justify-content: space-between;`. Le titre se placera à gauche et la navigation à droite ! C'est aussi simple que ça.

#### Mini-Exercice du Jour

Reprenez l'exercice des 3 cartes d'hier. Utilisez `display: flex;` sur leur conteneur parent. Utilisez `justify-content` pour tester les différentes options de répartition. Observez comme les espaces indésirables ont disparu.

#### Synthèse

Vous venez de découvrir l'outil de mise en page le plus important du CSS moderne. Vous savez maintenant aligner des éléments sur une ligne avec une facilité déconcertante. Demain, nous allons explorer la deuxième dimension de Flexbox : l'alignement sur l'axe secondaire et le contrôle des items individuels.

---

### J3 (Mercredi) : Maîtrise de Flexbox (Partie 2)

**Objectif(s) du Jour :**
- Maîtriser l'alignement sur l'axe secondaire (`align-items`).
- Contrôler le comportement des items Flex individuels (`flex-grow`, `flex-basis`...).
- Gérer le passage à la ligne avec `flex-wrap`.

**Notion Clé : La Deuxième Dimension et la Flexibilité**
Si `justify-content` gère l'alignement horizontal (par défaut), `align-items` gère l'alignement vertical. C'est la solution miracle à l'un des plus vieux problèmes du CSS : **centrer verticalement**. De plus, la vraie puissance de Flexbox réside dans sa "flexibilité" : la capacité des items à grandir ou rétrécir pour occuper l'espace disponible.

---

#### Leçon

##### 1. L'Axe Secondaire (Cross Axis)
La propriété `align-items` contrôle l'alignement sur l'axe perpendiculaire à l'axe principal.
- `stretch` (défaut) : Les items s'étirent pour remplir toute la hauteur (ou largeur) du conteneur.
- `flex-start` : Items alignés en haut (par défaut).
- `flex-end` : Items alignés en bas.
- `center` : **Centre les items verticalement.**

##### 2. La Flexibilité des Items
Ces propriétés s'appliquent aux *items* Flex, pas au conteneur.
- `flex-grow` : Un nombre qui indique la capacité d'un item à "grandir" pour occuper l'espace vide. Si un item a `flex-grow: 2;` et les autres `flex-grow: 1;`, il prendra deux fois plus d'espace libre que les autres.
- `flex-shrink` : Capacité à rétrécir s'il n'y a pas assez de place.
- `flex-basis` : Taille de base de l'item avant que l'espace ne soit distribué.
- `flex` : Raccourci pour les 3 propriétés (`flex: <grow> <shrink> <basis>`). `flex: 1;` est un raccourci commun pour `flex: 1 1 0%;`, signifiant "occupe l'espace disponible équitablement".

- **Exemple de Code :**
  ```css
  .container {
    display: flex;
    height: 200px; /* On donne une hauteur pour voir l'effet */
    align-items: center; /* Magie : tout est centré verticalement */
  }
  
  .item-qui-grandit {
    flex-grow: 1; /* Cet item prendra tout l'espace restant */
  }
  ```

---

#### Mise en Pratique

1.  Revenez sur votre `<header>` que vous avez mis en `display: flex`. Donnez-lui une hauteur (`height`) ou un `padding` haut/bas. Appliquez `align-items: center;`. Votre titre et votre navigation sont maintenant parfaitement alignés verticalement.
2.  Imaginez que votre page de recette a deux sections principales : "Ingrédients" et "Préparation". Mettez-les dans un conteneur parent.
    ```html
    <div class="recipe-content">
      <section class="ingredients">...</section>
      <section class="preparation">...</section>
    </div>
    ```
3.  Appliquez `display: flex;` à `.recipe-content`. Les deux sections se mettent côte à côte.
4.  Donnez `flex: 1;` à la section `.preparation` et `flex: 0 0 300px;` (ne grandit pas, ne rétrécit pas, base de 300px) à la section `.ingredients`. La colonne des ingrédients aura une taille fixe et celle de la préparation prendra tout le reste de la place.

#### Mini-Exercice du Jour

Créez une "card" avec un `header`, un `main content` et un `footer`. Utilisez Flexbox pour que le `footer` soit toujours collé en bas de la carte, même si le contenu principal est court. (Indice : mettez le conteneur de la carte en `display: flex;` et `flex-direction: column;`, puis donnez un `flex-grow: 1;` à la zone de contenu principal).

#### Synthèse

Vous avez maintenant un contrôle quasi-total sur la mise en page unidimensionnelle. Flexbox est l'outil que vous utiliserez 80% du temps pour agencer vos composants. Demain, nous allons faire en sorte que toutes ces belles mises en page s'adaptent à la taille de l'écran.

---

### J4 (Jeudi) : S'adapter à tous les Écrans - Responsive Design

**Objectif(s) du Jour :**
- Comprendre la philosophie du "Mobile First".
- Utiliser les **Media Queries** pour appliquer des styles CSS conditionnels.
- Appliquer des transitions pour rendre les changements de style plus fluides.

**Notion Clé : Un seul Code, Plusieurs Apparences**
Le responsive design n'est pas une technologie, c'est une approche. L'idée est d'écrire un seul code HTML/CSS qui s'adapte à l'appareil qui l'affiche. Les Media Queries sont la pierre angulaire de cette approche : ce sont des "if" pour votre CSS. "SI l'écran est plus large que 768px, ALORS fais passer la mise en page en deux colonnes". On commence par styliser pour le plus petit écran (mobile), puis on ajoute des styles pour les écrans plus grands. C'est l'approche "Mobile First".

---

#### Leçon

##### 1. Le Viewport Meta Tag
La toute première chose à faire pour un site responsive est d'ajouter cette ligne dans le `<head>` de votre HTML. Elle dit au téléphone de ne pas "dézoomer" pour afficher la page.

```html
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

##### 2. Les Media Queries
La syntaxe est `@media (condition) { ...vos règles CSS ici... }`. La condition la plus courante est la largeur de l'écran.
- `min-width` : S'applique si l'écran fait **au moins** cette largeur. (Approche Mobile First)
- `max-width` : S'applique si l'écran fait **au plus** cette largeur.

##### 3. Les Transitions
La propriété `transition` anime en douceur le passage d'un état à un autre.

- **Exemple de Code (Workflow Mobile First) :**
  ```css
  /* === Styles par défaut (Mobile) === */
  .container {
    display: block; /* Les éléments sont les uns en dessous des autres */
  }

  .card {
    width: 100%;
    margin-bottom: 20px;
  }
  
  /* === Styles pour Tablettes et plus === */
  @media (min-width: 768px) {
    .container {
      display: flex; /* On passe en Flexbox sur les écrans plus grands */
      justify-content: space-between;
    }
    .card {
      width: 48%; /* Deux cartes par ligne avec un petit espace */
      margin-bottom: 0;
    }
  }

  /* === Transition fluide === */
  .card {
    transition: transform 0.3s ease;
  }
  .card:hover {
    transform: translateY(-5px); /* Au survol, la carte monte un peu */
  }
  ```

---

#### Mise en Pratique

1.  Ajoutez la balise `<meta name="viewport">` à votre projet.
2.  Prenez la mise en page en deux colonnes (ingrédients/préparation) que vous avez faite hier. Par défaut (pour mobile), faites en sorte que les deux sections soient l'une en dessous de l'autre (`flex-direction: column;` sur le conteneur ou juste `display: block;`).
3.  Enveloppez la règle CSS qui les met côte à côte (`display: flex; flex-direction: row;`) dans une media query `@media (min-width: 768px) { ... }`.
4.  Ouvrez les outils de développement de votre navigateur (F12) et activez le mode de vue adaptative (l'icône de téléphone/tablette). Réduisez la largeur de l'écran. Observez vos colonnes passer l'une en dessous de l'autre lorsque vous franchissez le seuil de 768px.
5.  Ajoutez une propriété `transition` sur un élément qui change au `:hover` (comme votre bouton) pour voir l'effet.

#### Mini-Exercice du Jour

Créez une barre de navigation. Sur mobile, les liens doivent être cachés et seul un bouton "Menu" (hamburger) est visible. Sur les écrans plus grands (`min-width: 768px`), le bouton "Menu" doit disparaître et les liens doivent apparaître, alignés horizontalement. (Indice : utilisez `display: none;` et `display: flex;` à l'intérieur de vos media queries).

#### Synthèse

C'est une étape de géant. Vous savez maintenant créer des sites qui fonctionnent et sont beaux partout. C'est une compétence non négociable pour un développeur web en 2023. Demain, nous découvrirons le deuxième grand outil de mise en page, CSS Grid, et nous lancerons le projet final de cette phase d'intégration.

---

### J5 (Vendredi) : CSS Grid et Lancement du Projet d'Intégration

**Objectif(s) du Jour :**
- Comprendre la différence entre Flexbox (1D) et CSS Grid (2D).
- Créer une grille simple avec `display: grid`.
- Lancer le projet final : intégrer une maquette "pixel perfect" et responsive.

**Notion Clé : Le Sudoku du Web**
Si Flexbox est pour aligner des choses sur une ligne ou une colonne, CSS Grid est pour organiser toute la page dans une grille à deux dimensions, comme une grille de Sudoku ou un tableur. Vous définissez les colonnes et les lignes, puis vous placez vos éléments dans les cellules que vous voulez. C'est l'outil ultime pour les mises en page complexes et asymétriques.

---

#### Leçon

##### 1. Les Bases de CSS Grid
- `display: grid;` : Appliqué au conteneur pour le transformer en grille.
- `grid-template-columns` : Définit le nombre et la taille des colonnes. L'unité `fr` (fraction) est très pratique : elle représente une fraction de l'espace disponible.
- `grid-template-rows` : Définit la taille des lignes.
- `grid-gap` (ou `gap`) : Définit l'espace entre les cellules de la grille.

- **Exemple de Code (Une mise en page "Sainte Graal") :**
  ```html
  <div class="grid-container">
    <header>Header</header>
    <nav>Nav</nav>
    <main>Main Content</main>
    <footer>Footer</footer>
  </div>
  ```
  ```css
  .grid-container {
    display: grid;
    grid-template-columns: 200px 1fr; /* 1ère colonne de 200px, 2ème prend le reste */
    grid-template-rows: auto 1fr auto; /* Header/Footer auto, Main prend le reste */
    grid-template-areas: 
      "header header"
      "nav    main"
      "footer footer";
    gap: 10px;
    height: 100vh; /* Prend toute la hauteur de l'écran */
  }
  header { grid-area: header; }
  nav { grid-area: nav; }
  main { grid-area: main; }
  footer { grid-area: footer; }
  ```

---

#### PROJET DE LA SEMAINE : Intégration d'une Landing Page

**La Mission :**
Vous allez recevoir une maquette graphique (un fichier Figma, par exemple) d'une "landing page" (page d'accueil). Votre mission est de la recréer à l'identique en HTML et CSS. Le résultat doit être "pixel perfect" (le plus proche possible de la maquette) et entièrement responsive.

**Le Workflow Professionnel : Mobile First**
1.  **Analyse (30 min) :** Ouvrez la maquette (les vues mobile et desktop). Identifiez les sections, les polices, les couleurs, les espacements.
2.  **HTML Sémantique (1h) :** Écrivez d'abord **tout** le HTML de la page, en vous basant sur la vue mobile. Structurez bien votre document avec les balises sémantiques.
3.  **CSS Mobile (3h) :** Écrivez **tout** le CSS pour que la page soit parfaite sur mobile. N'utilisez aucune media query pour l'instant.
4.  **CSS Tablette & Desktop (le reste du temps) :** Maintenant, ajoutez des media queries (`@media (min-width: ...)`). À l'intérieur, modifiez les règles nécessaires (souvent des `display: flex` ou `grid`) pour adapter la mise en page aux écrans plus grands. Travaillez par "points de rupture" (breakpoints) : un pour les tablettes (~768px), un pour les desktops (~1024px).

**Livrables :**
- Un dossier de projet avec votre `index.html`, `style.css` et les images.
- Le projet doit être déposé sur GitHub.
- **Bonus :** Déployez votre page sur Netlify ou GitHub Pages pour avoir une URL live.

**Critères de Succès :**
- **Sémantique HTML :** Le code HTML est propre et utilise les bonnes balises.
- **Fidélité à la Maquette :** La page ressemble-t-elle à la maquette sur les grands écrans ?
- **Qualité du Responsive :** La page est-elle parfaitement utilisable et esthétique sur un petit écran de mobile (ex: 375px de large) ?
- **Qualité du CSS :** Le code est-il bien organisé ? Utilisez-vous Flexbox/Grid pour la mise en page ? Les unités sont-elles adaptées (`rem`) ?

#### Synthèse Finale de la Phase d'Intégration

Félicitations ! En trois semaines, vous êtes passé d'une page blanche à la capacité d'intégrer des designs complexes et professionnels qui fonctionnent sur tous les appareils. Vous avez acquis le socle de compétences de l'intégrateur web. C'est une étape immense. La prochaine phase consistera à donner vie à ces pages statiques en y ajoutant de l'interactivité et de l'intelligence avec JavaScript.