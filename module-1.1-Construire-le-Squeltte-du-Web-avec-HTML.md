# Module 1 : Construire le Squelette du Web avec HTML

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Comprendre le rôle de HTML dans la création d'une page web.
- Écrire un document HTML valide et bien structuré.
- Utiliser les balises sémantiques d'HTML5 pour donner du sens à votre contenu.
- Insérer du texte, des liens, des images et des listes.
- Créer des tableaux pour afficher des données tabulaires.
- Construire des formulaires simples pour l'interaction utilisateur.
- Structurer une page complète de type "article" ou "CV".

## 2. Prérequis

- Un ordinateur et un accès à internet.
- Un navigateur web (Chrome, Firefox, Edge...).
- Un éditeur de texte. Nous recommandons fortement **Visual Studio Code** (gratuit).
- Aucune connaissance en programmation n'est requise. Juste de la curiosité !

## 3. Résumé du Concept (Qu'est-ce que HTML ?)

Imaginez que vous construisez une maison. HTML (HyperText Markup Language) n'est ni la peinture, ni les meubles, ni l'électricité. **HTML, ce sont les fondations, les murs porteurs, le toit.** C'est le **squelette** qui donne sa structure et son sens à une page web.

Ce n'est pas un langage de programmation, mais un **langage de balisage**. Il utilise des "balises" (comme `<h1>` ou `<p>`) pour dire au navigateur : "Ceci est un titre principal", "Ceci est un paragraphe", "Ceci est une image".

Sans HTML, le web ne serait qu'un immense fichier texte illisible. Votre mission est d'apprendre à utiliser ces balises pour transformer un contenu brut en une structure logique et cohérente, prête à être mise en forme avec CSS (le module suivant !).

## 4. Plan d’Apprentissage

*   **Chapitre 1 : Les Fondations**
    *   Structure d'un document HTML
    *   Les balises `<html>`, `<head>`, `<body>`
    *   Le Doctype et les métadonnées
*   **Chapitre 2 : Le Contenu Textuel**
    *   Titres (`<h1>` à `<h6>`)
    *   Paragraphes (`<p>`)
    *   Mise en exergue (`<strong>`, `<em>`)
*   **Chapitre 3 : Listes & Liens**
    *   Listes non ordonnées (`<ul>`)
    *   Listes ordonnées (`<ol>`)
    *   Liens hypertextes (`<a>`)
*   **Chapitre 4 : Images & Médias**
    *   Insérer une image (`<img>`)
    *   L'importance de l'attribut `alt`
*   **Chapitre 5 : La Structure Sémantique**
    *   Organiser la page : `<header>`, `<footer>`, `<main>`, `<nav>`
    *   Structurer le contenu : `<section>`, `<article>`, `<aside>`
*   **Chapitre 6 : Tableaux & Formulaires**
    *   Créer un tableau (`<table>`, `<tr>`, `<th>`, `<td>`)
    *   Construire un formulaire simple (`<form>`, `<label>`, `<input>`, `<button>`)

## 5. Leçons

### Leçon 1 : Les Fondations

Toute page HTML valide possède une structure de base. Le `<head>` contient les informations sur la page (le titre de l'onglet, les métadonnées) qui ne sont pas visibles directement. Le `<body>` contient tout le contenu visible par l'utilisateur.

- **Exemple de code simple :**
  ```html
  <!DOCTYPE html>
  <html>
    <head>
      <title>Ma Première Page</title>
    </head>
    <body>
      Contenu visible de ma page.
    </body>
  </html>
  ```
- **Exemple de code appliqué à un cas réel (le squelette de notre future page de recette) :**
  ```html
  <!DOCTYPE html>
  <html lang="fr">
    <head>
      <meta charset="UTF-8">
      <title>Recette des crêpes parfaites</title>
    </head>
    <body>
      <!-- Le contenu de notre recette viendra ici -->
    </body>
  </html>
  ```

### Leçon 2 : Le Contenu Textuel

Le texte est roi sur le web. HTML nous donne des outils pour le hiérarchiser. `<h1>` est le titre le plus important (un seul par page !), `<h2>` un sous-titre, etc. `<p>` est utilisé pour les blocs de texte courants. `<strong>` indique une forte importance (gras), et `<em>` une emphase (italique).

- **Exemple de code simple :**
  ```html
  <h1>Titre Principal</h1>
  <h2>Un sous-titre</h2>
  <p>Ceci est un paragraphe de texte. Il peut contenir des mots en <strong>gras</strong> ou en <em>italique</em>.</p>
  ```
- **Exemple de code appliqué à notre recette :**
  ```html
  <!-- Dans le <body> -->
  <h1>Recette des crêpes parfaites</h1>
  <p>Une recette <em>simple et rapide</em> pour régaler toute la famille. Le secret ? Un peu de patience pour laisser reposer la pâte !</p>
  ```

### Leçon 3 : Listes & Liens

Les listes permettent d'organiser l'information. `<ul>` pour une liste à puces (les ingrédients), `<ol>` pour une liste numérotée (les étapes). Le lien `<a>` est le cœur du web, il connecte les pages entre elles via son attribut `href`.

- **Exemple de code simple :**
  ```html
  <ul>
    <li>Pomme</li>
    <li>Banane</li>
  </ul>
  <ol>
    <li>Première étape</li>
    <li>Deuxième étape</li>
  </ol>
  <a href="https://www.google.com">Aller sur Google</a>
  ```
- **Exemple de code appliqué à notre recette :**
  ```html
  <!-- Dans le <body> -->
  <h2>Ingrédients</h2>
  <ul>
    <li>300g de farine</li>
    <li>3 œufs</li>
    <li>60cl de lait</li>
    <li>50g de beurre fondu</li>
  </ul>

  <h2>Préparation</h2>
  <ol>
    <li>Mélanger la farine et les œufs.</li>
    <li>Ajouter le lait petit à petit.</li>
    <li>Finir avec le beurre fondu et laisser reposer 1h.</li>
  </ol>
  <p>Recette inspirée par <a href="https://www.marmiton.org">Marmiton</a>.</p>
  ```

### Leçon 4 : Images & Médias

Une image vaut mille mots. La balise `<img>` est une balise "vide" (elle n'a pas de balise fermante). Elle a besoin de deux attributs essentiels : `src` (la source de l'image) et `alt` (un texte alternatif décrivant l'image, crucial pour l'accessibilité et si l'image ne charge pas).

- **Exemple de code simple :**
  ```html
  <img src="chemin/vers/mon-image.jpg" alt="Description de l'image">
  ```
- **Exemple de code appliqué à notre recette :**
  ```html
  <!-- Dans le <body>, juste après le <h1> -->
  <img src="crepes.jpg" alt="Une pile de crêpes dorées avec du sucre glace.">
  ```
  *(Note : ce code suppose qu'une image nommée `crepes.jpg` se trouve dans le même dossier que votre fichier HTML.)*

### Leçon 5 : La Structure Sémantique

Au lieu d'utiliser des `<div>` partout, HTML5 nous offre des balises qui décrivent le rôle de chaque bloc. C'est comme nommer les pièces d'une maison (cuisine, salon, chambre) au lieu de les appeler toutes "Pièce". C'est essentiel pour les moteurs de recherche et les lecteurs d'écran.

- **Exemple de code simple :**
  ```html
  <body>
    <header>En-tête du site</header>
    <nav>Navigation principale</nav>
    <main>
      <section>
        <h1>Contenu principal</h1>
      </section>
    </main>
    <footer>Pied de page</footer>
  </body>
  ```
- **Exemple de code appliqué à notre recette (en assemblant tout) :**
  ```html
  <main>
    <article>
      <header>
        <h1>Recette des crêpes parfaites</h1>
        <p>Publié le 26 octobre 2023</p>
      </header>
      <img src="crepes.jpg" alt="Une pile de crêpes dorées...">
      
      <section>
        <h2>Ingrédients</h2>
        <ul>...</ul>
      </section>

      <section>
        <h2>Préparation</h2>
        <ol>...</ol>
      </section>

      <footer>
        <p>Recette inspirée par <a href="https://www.marmiton.org">Marmiton</a>.</p>
      </footer>
    </article>
  </main>
  ```

### Leçon 6 : Tableaux & Formulaires

Les tableaux (`<table>`) sont faits **uniquement** pour présenter des données tabulaires (horaires, comparaisons, stats...). Les formulaires (`<form>`) sont la principale façon pour un utilisateur d'envoyer des informations au site. La balise `<label>` est très importante pour lier le texte à son champ de saisie (`<input>`).

- **Exemple de code simple :**
  ```html
  <!-- Tableau -->
  <table>
    <tr>
      <th>Nom</th>
      <th>Âge</th>
    </tr>
    <tr>
      <td>Alice</td>
      <td>30</td>
    </tr>
  </table>

  <!-- Formulaire -->
  <form>
    <label for="nom">Votre nom :</label>
    <input type="text" id="nom" name="user_name">
    <button type="submit">Envoyer</button>
  </form>
  ```
- **Exemple de code appliqué (ajoutons un formulaire de commentaire à notre recette) :**
  ```html
  <!-- Dans l'<footer> de l'article ou après -->
  <section>
    <h2>Laissez un commentaire</h2>
    <form>
      <div>
        <label for="pseudo">Pseudo :</label>
        <input type="text" id="pseudo" name="pseudo">
      </div>
      <div>
        <label for="commentaire">Commentaire :</label>
        <textarea id="commentaire" name="commentaire"></textarea>
      </div>
      <button type="submit">Poster</button>
    </form>
  </section>
  ```

## 6. Exercices Pratiques

Créez un nouveau fichier `.html` pour chaque exercice.

- **Niveau Débutant : Ma Chanson Préférée**
  Créez une page avec le titre (`<h1>`) de votre chanson préférée. Ajoutez le nom de l'artiste (`<h2>`) puis les paroles de la chanson en utilisant des paragraphes (`<p>`). Mettez le refrain en gras (`<strong>`).

- **Niveau Intermédiaire : Mon Top 5 de Films**
  Créez une page listant votre top 5 de films. Utilisez un titre principal `<h1>`. Utilisez une liste ordonnée (`<ol>`). Chaque élément de la liste (`<li>`) devra contenir le titre du film, et ce titre devra être un lien (`<a>`) qui pointe vers la page IMDb ou Wikipédia du film.

- **Niveau Avancé : Structure d'un Article de Blog**
  Créez la structure d'une page d'article de blog sur un sujet qui vous passionne. La page doit obligatoirement utiliser `<header>`, `<main>`, `<article>`, `<section>`, et `<footer>`. L'article doit contenir un titre principal, au moins deux sous-titres, une image, et une liste.

## 7. Mini-projet Guidé : Créer une page de liens "Mon Profil"

Nous allons créer une page simple qui rassemble tous vos liens importants, comme un "Linktree".

1.  **Étape 1 : La structure**
    Créez un fichier `index.html`. Mettez en place la structure de base (`<!DOCTYPE>`, `<html>`, `<head>`, `<body>`). Donnez un titre à votre page dans `<title>`, par exemple "Mon Profil - [Votre Nom]".

2.  **Étape 2 : L'en-tête**
    Dans le `<body>`, ajoutez une image de profil (utilisez un placeholder si vous n'en avez pas) et votre nom dans un `<h1>`.
    ```html
    <img src="https://via.placeholder.com/150" alt="Photo de profil">
    <h1>[Votre Nom]</h1>
    ```

3.  **Étape 3 : La liste de liens**
    Créez une liste non ordonnée (`<ul>`). Chaque élément de la liste (`<li>`) contiendra un lien (`<a>`). Créez au moins 3 liens : un vers votre portfolio (mettez "#" si vous n'en avez pas), un vers votre profil LinkedIn, et un vers votre profil GitHub.
    ```html
    <ul>
      <li><a href="#">Mon Portfolio</a></li>
      <li><a href="https://linkedin.com/in/...">Mon profil LinkedIn</a></li>
      <li><a href="https://github.com/...">Mon profil GitHub</a></li>
    </ul>
    ```

4.  **Étape 4 : Le pied de page**
    Ajoutez un `<footer>` tout en bas du `<body>` avec une petite note de copyright.
    ```html
    <footer>
      <p>© 2023 - [Votre Nom]</p>
    </footer>
    ```
Vous avez maintenant une page complète et fonctionnelle !

## 8. Projet Final Non Guidé : Votre CV en Ligne

L'objectif est de créer une page unique `cv.html` qui servira de CV en ligne, en utilisant uniquement HTML.

**Livrables :**
1.  Un fichier `cv.html`.
2.  Le code doit être propre et bien indenté.

**Contenu obligatoire :**
- Un en-tête (`<header>`) avec votre nom (`<h1>`) et votre titre/poste recherché (`<h2>` ou `<p>`).
- Une section "Contact" (`<section>`) contenant un formulaire (`<form>`) avec des champs pour le nom, l'email, le message et un bouton d'envoi.
- Une section "Expériences Professionnelles" (`<section>`) utilisant des titres (`<h3>`), des paragraphes (`<p>`) et des listes (`<ul>`) pour décrire chaque poste.
- Une section "Formation" (`<section>`) structurée de la même manière que les expériences.
- Une section "Compétences" (`<section>`) qui utilise un tableau (`<table>`) pour lister des compétences et votre niveau (ex: Débutant, Intermédiaire, Avancé).
- Un pied de page (`<footer>`) avec des liens vers vos réseaux sociaux professionnels.

Vous devez choisir les balises les plus sémantiques possibles pour chaque élément.

## 9. Critères d'Évaluation

Votre projet final sera évalué sur les critères suivants :

- **Validité du code (non négociable) :** Le code doit passer la validation du [W3C Validator](https://validator.w3.org/) sans erreurs.
- **Utilisation de la sémantique :** Les balises `<header>`, `<footer>`, `<main>`, `<section>`, `<nav>`, `<article>` sont-elles utilisées correctement ? Le choix des balises (`<ul>` vs `<ol>`, `<strong>` vs `<b>`) est-il justifié ?
- **Structure et Hiérarchie :** La hiérarchie des titres (`<h1>`, `<h2>`, etc.) est-elle logique ? Le document est-il bien structuré ?
- **Accessibilité :** Toutes les images ont-elles un attribut `alt` pertinent ? Les `label` sont-ils correctement associés à leurs `input` dans les formulaires ?
- **Complétude :** Le projet contient-il tous les éléments demandés dans le cahier des charges ?

## 10. Ressources Complémentaires Fiables

- **MDN Web Docs (Mozilla Developer Network) :** LA référence absolue pour tout ce qui concerne le web. C'est votre nouvelle encyclopédie.
  - [Tutoriel HTML sur MDN](https://developer.mozilla.org/fr/docs/Web/HTML)
- **W3C HTML Validator :** L'outil officiel pour vérifier si votre code HTML est valide. Prenez l'habitude de l'utiliser.
  - [validator.w3.org](https://validator.w3.org/)
- **freeCodeCamp :** Plateforme d'apprentissage interactive avec des centaines d'exercices.
  - [Responsive Web Design Certification](https://www.freecodecamp.org/learn/2022/responsive-web-design/)
- **HTML Reference by Codrops :** Une référence visuelle et très bien faite de toutes les balises HTML.
  - [htmlreference.io](https://htmlreference.io/)