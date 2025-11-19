# Module 2 : Donner Vie au Web avec CSS

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Lier une feuille de style CSS à un document HTML.
- Utiliser les sélecteurs CSS pour cibler n'importe quel élément HTML.
- Maîtriser le "modèle de boîte" (Box Model) pour gérer les dimensions et les espacements.
- Styliser le texte (polices, couleurs, tailles) et les arrière-plans.
- Créer des mises en page complexes et modernes avec Flexbox.
- Organiser des grilles bidimensionnelles avec CSS Grid.
- Rendre un site web "responsive" pour qu'il s'adapte parfaitement aux mobiles, tablettes et ordinateurs.
- Appliquer des transitions et des transformations simples pour une expérience utilisateur dynamique.

## 2. Prérequis

- Avoir complété le **Module 1 : Construire le Squelette du Web avec HTML**.
- Maîtriser la création et la structuration d'un fichier `.html`.
- Disposer d'un éditeur de texte (VS Code recommandé) et d'un navigateur web.

## 3. Résumé du Concept (Qu'est-ce que CSS ?)

Si HTML est le squelette de votre page web, **CSS (Cascading Style Sheets) en est la peau, les vêtements et le style**. C'est le langage qui permet de contrôler l'apparence de votre contenu : couleurs, polices, espacements, positionnement, et même des animations.

La force de CSS réside dans la **séparation des préoccupations**. Votre fichier HTML s'occupe du *sens* et de la *structure*, tandis qu'un fichier `.css` séparé gère toute la *présentation*. Cette organisation rend votre projet plus facile à maintenir : pour changer la couleur de tous vos titres, vous ne modifiez qu'une seule ligne dans votre fichier CSS, au lieu de devoir modifier chaque page HTML.

Le mot "Cascading" (cascade) est crucial : il décrit comment les styles, venant de différentes sources, s'appliquent et s'annulent entre eux. Apprendre CSS, c'est apprendre à maîtriser cette cascade pour obtenir le design précis que vous désirez.

## 4. Plan d’Apprentissage

*   **Chapitre 1 : Lier CSS et Sélectionner des Éléments**
    *   Les 3 méthodes d'application de CSS (et pourquoi l'externe est la meilleure)
    *   Sélecteurs de base : balise, classe, ID
    *   Combiner les sélecteurs
*   **Chapitre 2 : Couleurs, Texte et Arrière-plans**
    *   Changer la couleur du texte et de l'arrière-plan
    *   Gérer la typographie (polices, taille, graisse)
*   **Chapitre 3 : Le Modèle de Boîte (Box Model)**
    *   Contenu, `padding`, `border`, `margin`
    *   La différence entre `box-sizing: content-box` et `border-box`
*   **Chapitre 4 : La Mise en Page avec Flexbox**
    *   Introduction à Flexbox : l'axe principal et l'axe secondaire
    *   Aligner et distribuer les éléments
*   **Chapitre 5 : Transitions et Effets Visuels Simples**
    *   Animer les changements d'état (`transition`)
    *   Les pseudo-classes (`:hover`, `:focus`)
*   **Chapitre 6 : Le Responsive Design**
    *   Le viewport meta tag
    *   Les Media Queries pour adapter le design à la taille de l'écran

## 5. Leçons

### Leçon 1 : Lier CSS et Sélectionner des Éléments

Pour commencer, nous devons créer un fichier `style.css` et le lier à notre `index.html`. Ensuite, nous utilisons des "sélecteurs" pour dire à CSS quels éléments HTML nous voulons styliser. Une classe (`.ma-classe`) est réutilisable, un ID (`#mon-id`) est unique.

- **Exemple de code simple :**

  *Fichier `index.html` (dans le `<head>`)*
  ```html
  <link rel="stylesheet" href="style.css">
  ```
  *Fichier `style.css`*
  ```css
  /* Sélectionne toutes les balises <p> */
  p {
    color: blue;
  }
  
  /* Sélectionne les éléments avec la classe "highlight" */
  .highlight {
    background-color: yellow;
  }
  ```
- **Exemple de code appliqué à notre page de recette HTML :**

  *Fichier `recette.html`*
  ```html
  <!-- ... dans le body ... -->
  <h2 class="section-title">Ingrédients</h2>
  <ul>
    <li class="essential">300g de farine</li>
    <!-- ... -->
  </ul>
  ```
  *Fichier `style.css`*
  ```css
  /* Met tous les titres h2 en couleur chocolat */
  .section-title {
    color: #583e2e;
  }

  /* Met en gras les ingrédients essentiels */
  .essential {
    font-weight: bold;
  }
  ```

### Leçon 2 : Couleurs, Texte et Arrière-plans

C'est la partie la plus visible du design. On peut définir les couleurs par leur nom (`red`), en hexadécimal (`#FF0000`) ou en RGB/RGBA. La typographie est tout aussi importante pour la lisibilité.

- **Exemple de code simple :**
  ```css
  body {
    background-color: #f4f4f4;
    font-family: Arial, sans-serif;
  }

  h1 {
    color: #333333;
    font-size: 2.5em; /* 2.5 fois la taille de police de base */
  }
  ```
- **Exemple de code appliqué à notre recette :**
  ```css
  body {
    font-family: 'Georgia', serif;
    line-height: 1.6; /* Améliore la lisibilité */
    background-color: #fffaf0;
  }

  h1, h2 {
    font-family: 'Helvetica', sans-serif;
    color: #d16400;
  }
  ```

### Leçon 3 : Le Modèle de Boîte (Box Model)

Chaque élément sur une page web est une boîte rectangulaire. Cette boîte est composée de 4 couches : le contenu, le `padding` (marge intérieure), la `border` (bordure), et la `margin` (marge extérieure). Maîtriser ce concept est **fondamental** pour toute mise en page.

- **Exemple de code simple :**
  ```css
  .ma-boite {
    width: 200px;
    padding: 20px; /* 20px d'espace à l'intérieur */
    border: 1px solid black;
    margin: 30px; /* 30px d'espace à l'extérieur */
  }
  ```
- **Exemple de code appliqué à notre recette (pour encadrer les sections) :**
  ```css
  .section-title {
    color: #583e2e;
    border-bottom: 2px solid #e0c9a6; /* Une jolie bordure sous le titre */
    padding-bottom: 10px; /* Espace entre le texte et la bordure */
  }

  article {
    width: 800px; /* Limite la largeur de l'article pour la lisibilité */
    margin: 40px auto; /* Centre l'article sur la page */
    padding: 30px;
    background-color: white;
    border-radius: 8px; /* Adoucit les coins */
    box-shadow: 0 4px 8px rgba(0,0,0,0.1); /* Ajoute une ombre subtile */
  }
  ```

### Leçon 4 : La Mise en Page avec Flexbox

Flexbox est un modèle de mise en page unidimensionnel conçu pour aligner et distribuer l'espace entre les éléments d'un conteneur. C'est l'outil moderne par excellence pour créer des en-têtes, des navigations, des galeries, et aligner des éléments verticalement.

- **Exemple de code simple :**
  ```html
  <div class="container">
    <div>1</div>
    <div>2</div>
  </div>
  ```
  ```css
  .container {
    display: flex;
    justify-content: space-between; /* Place les éléments aux extrémités */
  }
  ```
- **Exemple de code appliqué (pour mettre les listes d'ingrédients et de préparation côte à côte) :**
  ```html
  <div class="recipe-body">
      <section>...</section> <!-- Ingrédients -->
      <section>...</section> <!-- Préparation -->
  </div>
  ```
  ```css
  .recipe-body {
    display: flex;
    gap: 40px; /* Espace entre les deux colonnes */
  }
  .recipe-body section {
    flex: 1; /* Chaque section prend une part égale de l'espace */
  }
  ```

### Leçon 5 : Transitions et Effets Visuels Simples

Les `:pseudo-classes` permettent de styliser un élément dans un état particulier (survolé, cliqué, etc.). La propriété `transition` permet d'animer en douceur le passage d'un état à un autre, rendant l'interface plus agréable.

- **Exemple de code simple :**
  ```css
  .bouton {
    background-color: blue;
    transition: background-color 0.3s ease; /* Anime le changement de couleur */
  }
  .bouton:hover {
    background-color: darkblue; /* Changement au survol */
  }
  ```
- **Exemple de code appliqué (pour rendre les liens de notre recette interactifs) :**
  ```css
  a {
    color: #d16400;
    text-decoration: none; /* Enlève le soulignement par défaut */
    transition: color 0.2s;
  }
  a:hover {
    color: #583e2e;
    text-decoration: underline; /* Ajoute un soulignement au survol */
  }
  ```

### Leçon 6 : Le Responsive Design

Un site moderne doit être consultable sur n'importe quel écran. Les *Media Queries* sont des règles CSS qui ne s'appliquent que si certaines conditions sont remplies, généralement la largeur de l'écran.

- **Exemple de code simple :**
  ```css
  .container {
    background-color: blue;
  }

  /* Si l'écran fait 600px de large ou moins... */
  @media (max-width: 600px) {
    .container {
      background-color: red; /* ...le fond devient rouge. */
    }
  }
  ```
- **Exemple de code appliqué (pour que notre recette s'affiche bien sur mobile) :**
  ```css
  /* Styles par défaut (Mobile First) */
  .recipe-body {
    display: block; /* Les sections sont l'une en dessous de l'autre par défaut */
  }

  /* Si l'écran fait au moins 768px de large (tablettes et plus)... */
  @media (min-width: 768px) {
    .recipe-body {
      display: flex; /* ...on passe en mode Flexbox côte à côte */
      gap: 40px;
    }
  }
  ```

## 6. Exercices Pratiques

Utilisez les fichiers HTML des exercices du module précédent.

- **Niveau Débutant : Donner du Style à ma Chanson**
  Prenez votre page "Ma Chanson Préférée". Créez un fichier `style.css`. Changez la police de toute la page. Mettez le titre (`<h1>`) dans une couleur différente et plus grande. Centrez tout le texte de la page.

- **Niveau Intermédiaire : Styliser mon Top 5**
  Prenez votre page "Mon Top 5 de Films". Donnez à chaque film (`<li>`) une bordure, du `padding`, et une couleur de fond. Faites en sorte que la couleur de fond change lorsque vous survolez l'élément avec la souris (`:hover`).

- **Niveau Avancé : Un Article de Blog Élégant**
  Prenez votre page "Article de Blog". Limitez la largeur maximale du contenu à `900px` et centrez-le sur la page. Donnez une police différente aux titres et au corps du texte (utilisez [Google Fonts](https://fonts.google.com/)). Mettez l'image en pleine largeur de l'article, et le `<footer>` avec un fond gris clair et le texte centré.

## 7. Mini-projet Guidé : Créer une Carte de Profil

Nous allons styliser une carte de profil simple, un composant UI très courant.

1.  **Étape 1 : Le HTML**
    Créez un `index.html` avec la structure suivante et liez un fichier `style.css`.
    ```html
    <div class="profile-card">
      <img class="profile-avatar" src="https://via.placeholder.com/100" alt="Avatar">
      <h2 class="profile-name">Jeanne Doe</h2>
      <p class="profile-title">Développeuse Web</p>
      <a href="#" class="profile-button">Contacter</a>
    </div>
    ```

2.  **Étape 2 : Le conteneur principal**
    Dans `style.css`, ciblez `.profile-card`. Donnez-lui une largeur, une bordure, une ombre (`box-shadow`), et un `border-radius` pour arrondir les coins. Centrez le texte avec `text-align: center`.
    ```css
    .profile-card {
      width: 300px;
      margin: 50px auto;
      padding: 20px;
      border: 1px solid #ddd;
      border-radius: 10px;
      box-shadow: 0 2px 5px rgba(0,0,0,0.1);
      text-align: center;
    }
    ```

3.  **Étape 3 : L'avatar**
    Ciblez `.profile-avatar`. Pour le rendre rond, mettez son `border-radius` à `50%`.
    ```css
    .profile-avatar {
      width: 100px;
      height: 100px;
      border-radius: 50%;
    }
    ```

4.  **Étape 4 : La typographie**
    Ciblez le nom (`.profile-name`) et le titre (`.profile-title`). Changez leurs couleurs et leurs marges pour gérer l'espacement vertical.
    ```css
    .profile-name {
      margin-top: 15px;
      margin-bottom: 5px;
      color: #333;
    }
    .profile-title {
      color: #777;
      font-style: italic;
      margin-top: 0;
    }
    ```

5.  **Étape 5 : Le bouton**
    Stylisez le lien `.profile-button` pour qu'il ressemble à un bouton. Donnez-lui un `background-color`, une `color` pour le texte, du `padding`, et enlevez le soulignement (`text-decoration: none`). Ajoutez un effet `:hover` pour le rendre interactif.
    ```css
    .profile-button {
      display: inline-block; /* Nécessaire pour appliquer padding/margin */
      margin-top: 20px;
      padding: 10px 25px;
      background-color: #007BFF;
      color: white;
      border-radius: 5px;
      text-decoration: none;
      transition: background-color 0.3s;
    }
    .profile-button:hover {
      background-color: #0056b3;
    }
    ```

## 8. Projet Final Non Guidé : Rendre votre CV en Ligne Magnifique

Reprenez le projet final du module HTML, votre `cv.html`. Votre mission est de le styliser entièrement avec un fichier `style.css`.

**Livrables :**
1.  Le fichier `cv.html` (qui inclut maintenant un `<link>` vers votre CSS).
2.  Un nouveau fichier `style.css` contenant tout votre style.

**Contraintes et Objectifs :**
- **Professionnel et Lisible :** Le design doit être propre, sobre et facile à lire.
- **Palette de Couleurs :** Définissez une palette de 2 à 3 couleurs et tenez-vous-y.
- **Typographie :** Choisissez une police pour les titres et une pour le corps du texte (via Google Fonts).
- **Mise en page Flexbox :** Utilisez Flexbox pour créer une mise en page en deux colonnes (par exemple, une colonne principale plus large pour les expériences/formations, et une colonne latérale plus fine pour le contact/compétences).
- **Responsive :** Le design DOIT être responsive. Sur petit écran (< 768px), les colonnes doivent passer l'une en dessous de l'autre pour rester lisibles.
- **Interactivité :** Ajoutez des effets de survol (`:hover`) subtils sur les liens et les boutons.

**Idée bonus :** Essayez de vous inspirer d'un design de CV que vous aimez sur des sites comme Dribbble ou Behance. N'essayez pas de le copier parfaitement, mais de capturer son esprit.

## 9. Critères d'Évaluation

- **Organisation du CSS :** Le fichier `style.css` est-il bien organisé et commenté ?
- **Sélecteurs pertinents :** Les classes sont-elles bien nommées et utilisées à bon escient ? L'abus des ID ou des sélecteurs trop spécifiques est-il évité ?
- **Maîtrise du Box Model :** Les espacements (`padding`, `margin`) sont-ils cohérents et maîtrisés ? `box-sizing: border-box` est-il utilisé ?
- **Mise en Page Moderne :** La mise en page principale est-elle réalisée avec Flexbox (ou Grid) et non avec des techniques obsolètes ?
- **Qualité du Responsive Design :** Le site est-il parfaitement utilisable sur un écran de 320px de large ? La transition vers le design "desktop" est-elle fluide ?
- **Esthétique et Finitions :** La palette de couleurs est-elle harmonieuse ? Les polices sont-elles lisibles ? Y a-t-il une attention aux détails (transitions, ombres subtiles, etc.) ?
- **Validité du code :** Le code CSS passe-t-il la validation du [W3C CSS Validator](https://jigsaw.w3.org/css-validator/)?

## 10. Ressources Complémentaires Fiables

- **MDN Web Docs :** Encore et toujours la meilleure ressource.
  - [Tutoriel CSS sur MDN](https://developer.mozilla.org/fr/docs/Web/CSS)
- **CSS-Tricks :** Une source inépuisable de guides pratiques et d'articles de fond.
  - [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- **Flexbox Froggy :** Un jeu pour apprendre Flexbox de manière ludique. Indispensable.
  - [flexboxfroggy.com](https://flexboxfroggy.com/)
- **Grid Garden :** Le même concept que Flexbox Froggy, mais pour apprendre CSS Grid.
  - [cssgridgarden.com](https://cssgridgarden.com/)
- **Adobe Color :** Un outil formidable pour créer des palettes de couleurs harmonieuses.
  - [color.adobe.com](https://color.adobe.com/fr/create/color-wheel)
- **Google Fonts :** Une bibliothèque immense de polices de caractères gratuites et faciles à intégrer.
  - [fonts.google.com](https://fonts.google.com/)