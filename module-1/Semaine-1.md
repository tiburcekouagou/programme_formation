## Semaine 1 : Introduction et Fondations HTML5

### J1 : Qu'est-ce qu'une Page Web ? Le Squelette de Base

**Objectif(s) du Jour :**
- Comprendre le dialogue Client/Serveur et le rôle de HTTP.
- Décomposer une URL et comprendre sa signification.
- Créer le squelette non négociable de toute page HTML5.

**Notion Clé : Le dialogue du Web**
Imaginez que vous commandez une pizza. Vous (le **Client**) utilisez votre téléphone (le **Navigateur**) pour appeler l'adresse de la pizzeria (l'**URL**). Votre commande suit un protocole de langage (le protocole **HTTP**). La pizzeria (le **Serveur**) reçoit votre commande, prépare la pizza (la page web) et vous la renvoie. HTML, c'est la recette de base de cette pizza.

---

#### Leçon

##### 1. Le Dialogue Client-Serveur

- **Client :** Votre navigateur (Chrome, Firefox, etc.) qui *demande* des pages.
- **Serveur :** Un ordinateur puissant, toujours allumé, qui stocke les sites web et les *envoie* quand on les lui demande.
- **HTTP/HTTPS :** Le langage, le protocole de communication que le client et le serveur utilisent pour se comprendre. HTTPS est la version sécurisée.

##### 2. Anatomie d'une URL

Prenons `https://www.marmiton.org/recettes/gateau.html` :
- `https://` : Le protocole utilisé.
- `www.marmiton.org` : Le nom de domaine, l'adresse du serveur.
- `/recettes/` : Un chemin, comme un dossier sur le serveur.
- `gateau.html` : Le fichier spécifique que l'on demande.

##### 3. La Structure de Base d'un Document HTML

Toute page web, sans exception, est construite sur ce squelette. C'est le point de départ de tout.

- **Exemple de Code (Le Squelette Obligatoire) :**
  ```html
  <!DOCTYPE html>
  <html lang="fr">
    <head>
      <meta charset="UTF-8">
      <title>Titre de ma page</title>
    </head>
    <body>
      <!-- C'est ici que tout le contenu visible apparaîtra -->
    </body>
  </html>
  ```
  - `<!DOCTYPE html>` : Déclare au navigateur que c'est bien un document HTML5.
  - `<html>` : La racine de tout le document. L'attribut `lang="fr"` est important pour l'accessibilité et le référencement.
  - `<head>` : La "tête" de la page. Contient les informations *sur* la page (titre de l'onglet, encodage des caractères, liens vers CSS...), mais n'est pas visible directement.
  - `<body>` : Le "corps" de la page. **Tout ce qui est visible par l'utilisateur se trouve ici.**

---

#### Mise en Pratique

1.  Créez un dossier sur votre ordinateur nommé `bootcamp-projet-1`.
2.  Ouvrez ce dossier avec votre éditeur de code (VS Code).
3.  Créez un nouveau fichier nommé `recette.html`.
4.  Copiez-collez le squelette de code ci-dessus dans ce fichier.
5.  Changez le `<title>` pour "Ma Recette de Crêpes".
6.  Enregistrez le fichier et ouvrez-le avec votre navigateur (clic droit > "Ouvrir avec...").
7.  **Félicitations !** Vous venez de créer et d'afficher votre toute première page web. Elle est vide, mais elle existe !

#### Mini-Exercice du Jour

Créez un second fichier, `test.html`, dans le même dossier. Mettez-y le squelette de base et donnez-lui le titre "Page de Test". Vérifiez que le titre de l'onglet du navigateur est correct.

#### Synthèse

Aujourd'hui, vous avez compris le dialogue qui anime le web et vous avez posé les fondations de votre première page. Demain, nous allons commencer à la remplir avec du contenu : du texte !

---

### J2 : Donner du Sens au Texte

**Objectif(s) du Jour :**
- Structurer le texte avec des titres et des paragraphes.
- Mettre en exergue certaines parties du texte.
- Comprendre l'importance de la hiérarchie du contenu.

**Notion Clé : Le Document Structuré**
Une page web n'est pas un simple traitement de texte. C'est un document structuré. Les titres (`<h1>`, `<h2>`...) ne sont pas juste là pour faire "gros", ils indiquent une hiérarchie, comme dans un rapport ou un livre. `<h1>` est le titre du livre, `<h2>` est le titre d'un chapitre, `<h3>` celui d'une sous-partie. C'est crucial pour les moteurs de recherche et l'accessibilité.

---

#### Leçon

##### 1. Les Titres et Paragraphes

- `<h1>` à `<h6>` : Les balises de titre. Il ne doit y avoir **qu'un seul `<h1>` par page**, car c'est le titre principal.
- `<p>` : La balise pour un paragraphe de texte standard.

##### 2. Mettre le texte en valeur

- `<strong>` : Indique une **forte importance**. Le navigateur l'affiche en gras par défaut.
- `<em>` : Indique une **emphase**. Le navigateur l'affiche en italique par défaut.
- `<!-- ... -->` : Permet d'écrire un commentaire dans le code, invisible pour l'utilisateur.

- **Exemple de Code :**
  ```html
  <h1>Le Titre Principal de la Page</h1>
  <p>Ceci est un paragraphe d'introduction.</p>
  
  <h2>Un sous-titre de niveau 2</h2>
  <p>Ce paragraphe contient une information <strong>très importante</strong>. Il faut y faire <em>particulièrement attention</em>.</p>

  <!-- Section suivante à rédiger -->
  ```

---

#### Mise en Pratique

Reprenez votre fichier `recette.html`. À l'intérieur de la balise `<body>`, ajoutez :
1.  Un titre principal `<h1>` : "Recette des crêpes parfaites".
2.  Un paragraphe `<p>` d'introduction qui décrit la recette. Mettez un mot en `<strong>` et un autre en `<em>`.
3.  Un sous-titre `<h2>` : "Un peu d'histoire".
4.  Un autre paragraphe `<p>` sous ce sous-titre.

Enregistrez et rafraîchissez la page dans votre navigateur. Vous devriez voir votre texte apparaître, structuré.

#### Mini-Exercice du Jour

Créez une nouvelle page `article.html`. Imaginez que vous écrivez un article de journal. Structurez-le avec un `<h1>`, deux `<h2>`, et des paragraphes pour chaque section.

#### Synthèse

Votre page a maintenant du contenu textuel structuré. C'est un grand pas ! Demain, nous allons la rendre vraiment "web" en y ajoutant des listes, des images et surtout, des liens hypertextes.

---

### J3 : Listes, Images et le Coeur du Web : les Liens

**Objectif(s) du Jour :**
- Créer des listes à puces et des listes numérotées.
- Insérer une image dans une page.
- Créer des liens pour naviguer entre les pages ou vers des sites externes.

**Notion Clé : L'Hypertexte**
Le "HT" de HTML signifie "HyperText". C'est la capacité de lier des documents entre eux qui a fait du web ce qu'il est. La balise `<a>` (ancre) est la brique fondamentale de cette toile mondiale.

---

#### Leçon

##### 1. Les Listes

- `<ul>` (Unordered List) : Crée une liste à puces.
- `<ol>` (Ordered List) : Crée une liste numérotée.
- `<li>` (List Item) : Représente chaque élément dans une liste (`<ul>` ou `<ol>`).

##### 2. Les Images

- `<img>` : Une balise "orpheline" (pas de balise fermante) pour insérer une image.
  - `src` (source) : Attribut obligatoire qui indique le chemin vers l'image.
  - `alt` (alternative text) : Attribut **essentiel** qui décrit l'image. Crucial pour l'accessibilité (lecteurs d'écran) et si l'image ne se charge pas.

##### 3. Les Liens

- `<a>` : La balise de lien.
  - `href` (hypertext reference) : Attribut obligatoire qui contient l'URL de destination.
  - Le texte entre `<a>` et `</a>` est le texte cliquable.

- **Exemple de Code :**
  ```html
  <h2>Ingrédients</h2>
  <ul>
    <li>Farine</li>
    <li>Oeufs</li>
  </ul>
  
  <h2>Préparation</h2>
  <ol>
    <li>Mélanger...</li>
    <li>Laisser reposer...</li>
  </ol>
  
  <img src="crepes.jpg" alt="Une pile de crêpes dorées sur une assiette.">
  
  <p>
    Pour plus de recettes, visitez <a href="https://www.marmiton.org">Marmiton</a>.
  </p>
  ```

---

#### Mise en Pratique

Dans votre `recette.html` :
1.  Ajoutez un `<h2>` "Ingrédients", suivi d'une liste `<ul>` contenant au moins 4 ingrédients.
2.  Ajoutez un `<h2>` "Préparation", suivi d'une liste `<ol>` décrivant les étapes.
3.  Trouvez une image de crêpes sur internet (par exemple sur [Unsplash](https://unsplash.com/)), enregistrez-la sous le nom `crepes.jpg` dans votre dossier `bootcamp-projet-1`.
4.  Insérez cette image avec la balise `<img>` juste après votre `<h1>`. N'oubliez pas l'attribut `alt` !
5.  Ajoutez un lien vers une autre page (ex: votre page `test.html` ou un site externe).

#### Mini-Exercice du Jour

Créez une page `portfolio.html`. Ajoutez un titre, puis une liste non ordonnée de vos projets. Chaque nom de projet dans la liste doit être un lien (pour l'instant, mettez `href="#"`).

#### Synthèse

Votre page est maintenant multimédia et connectée ! Demain, nous allons apprendre à organiser tous ces éléments dans des conteneurs logiques grâce aux balises sémantiques d'HTML5.

---

### J4 : L'Architecture de la Page - HTML Sémantique

**Objectif(s) du Jour :**
- Comprendre la différence entre `<div>` et les balises sémantiques.
- Utiliser `<header>`, `<footer>`, `<nav>`, `<main>` pour la structure globale.
- Utiliser `<section>` et `<article>` pour organiser le contenu.

**Notion Clé : Donner du Sens**
Avant HTML5, on organisait tout avec des `<div>`, des boîtes génériques sans signification. C'était comme construire une maison avec des pièces toutes nommées "Pièce". HTML5 a introduit des balises sémantiques qui sont comme des `<div>` mais avec un nom qui a du sens : `<header>` (en-tête), `<footer>` (pied de page), `<nav>` (navigation)... Cela rend le code infiniment plus lisible pour les humains, les moteurs de recherche et les technologies d'assistance.

---

#### Leçon

##### 1. Les Conteneurs de Page Principaux

- `<header>` : L'en-tête de la page ou d'une section. Contient souvent le logo, le titre principal, la navigation.
- `<nav>` : Contient les liens de navigation principaux.
- `<main>` : Le contenu **unique et principal** de la page. Il ne doit y en avoir qu'un seul par page.
- `<footer>` : Le pied de page. Contient les informations de copyright, liens annexes, etc.

##### 2. Les Conteneurs de Contenu

- `<section>` : Regroupe un ensemble de contenus thématiquement liés. Doit presque toujours avoir un titre.
- `<article>` : Représente un contenu autonome, qui pourrait être redistribué ailleurs (un article de blog, un post de forum, un produit...).
- `<aside>` : Pour le contenu tangentiel, en marge du contenu principal (une barre latérale, des liens connexes...).
- `<div>` : La boîte générique. À n'utiliser que pour du regroupement stylistique, quand aucune autre balise sémantique ne convient.

- **Exemple de Code (Structure d'une page de blog) :**
  ```html
  <body>
    <header>
      <h1>Mon Super Blog</h1>
      <nav>...</nav>
    </header>
  
    <main>
      <article>
        <header>
          <h2>Titre de l'article</h2>
        </header>
        <p>Contenu de l'article...</p>
        <footer>
          <p>Posté par...</p>
        </footer>
      </article>
      
      <aside>
        <h3>Articles récents</h3>
      </aside>
    </main>
    
    <footer>
      <p>&copy; 2023 Mon Super Blog</p>
    </footer>
  </body>
  ```

---

#### Mise en Pratique

Refactorisez votre `recette.html` !
1.  Encadrez tout le contenu de `<body>` avec les balises `<header>`, `<main>` et `<footer>` de manière appropriée. (Le `<h1>` et l'image vont dans le `<header>` de la page, le reste du contenu dans `<main>`, et créez un `<footer>` pour le copyright).
2.  Dans `<main>`, regroupez le contenu de la recette (introduction, ingrédients, préparation) dans une balise `<article>`.
3.  À l'intérieur de l'`<article>`, regroupez les ingrédients dans une `<section>` et la préparation dans une autre `<section>`.

Votre code est maintenant beaucoup plus propre et significatif, même si l'apparence dans le navigateur n'a pas changé.

#### Mini-Exercice du Jour

Reprenez votre page `portfolio.html`. Structurez-la avec `<header>`, `<main>`, `<footer>`. Placez votre liste de projets dans une `<section>` à l'intérieur du `<main>`.

#### Synthèse

Vous savez maintenant architecturer une page de manière professionnelle. C'est une compétence très recherchée. Demain, nous verrons les deux derniers types de contenu majeurs : les tableaux pour les données et les formulaires pour l'interaction.

---

### J5 : Données Tabulaires et Interaction - Tableaux & Formulaires

**Objectif(s) du Jour :**
- Créer un tableau pour afficher des données structurées.
- Construire un formulaire simple pour permettre à l'utilisateur de soumettre des informations.
- Consolider toutes les connaissances de la semaine pour le projet.

**Notion Clé : Entrées & Sorties**
Jusqu'à présent, vous avez surtout géré des "sorties" : afficher de l'information. Les tableaux sont une manière structurée de le faire pour des données complexes. Les formulaires sont le principal moyen de gérer les "entrées" : permettre à l'utilisateur d'envoyer des informations vers le serveur.

---

#### Leçon

##### 1. Les Tableaux

Utilisez les tableaux **uniquement** pour des données tabulaires (horaires, statistiques, comparaisons...). N'utilisez **jamais** de tableaux pour la mise en page.
- `<table>` : Le conteneur du tableau.
- `<tr>` (Table Row) : Une ligne du tableau.
- `<th>` (Table Header) : Une cellule d'en-tête (centrée et en gras par défaut).
- `<td>` (Table Data) : Une cellule de donnée standard.

##### 2. Les Formulaires

- `<form>` : Le conteneur du formulaire. Attributs importants : `action` (où envoyer les données) et `method` (comment : GET ou POST).
- `<label>` : L'étiquette textuelle d'un champ. L'attribut `for` doit correspondre à l'attribut `id` du champ pour les lier.
- `<input>` : Le champ de saisie. L'attribut `type` est crucial (`text`, `email`, `password`, `date`, `checkbox`...).
- `<textarea>` : Un champ de saisie pour du texte sur plusieurs lignes.
- `<button type="submit">` : Le bouton qui envoie le formulaire.

- **Exemple de Code :**
  ```html
  <!-- Tableau d'informations nutritionnelles -->
  <table>
    <tr>
      <th>Nutriment</th>
      <th>Quantité</th>
    </tr>
    <tr>
      <td>Calories</td>
      <td>250kcal</td>
    </tr>
  </table>

  <!-- Formulaire de commentaire -->
  <form action="/submit-comment" method="POST">
    <label for="username">Votre Nom :</label>
    <input type="text" id="username" name="username">

    <label for="comment">Votre commentaire :</label>
    <textarea id="comment" name="comment"></textarea>

    <button type="submit">Envoyer</button>
  </form>
  ```

---

#### Mise en Pratique

Dans votre `recette.html`, après la section de préparation :
1.  Ajoutez un `<h2>` "Informations Nutritionnelles" et créez un petit `<table>` avec quelques valeurs.
2.  Ajoutez un `<h2>` "Laissez un commentaire" et créez un `<form>` permettant de laisser son nom et un message.

#### PROJET DE LA SEMAINE : Votre Page Sémantique

Vous avez maintenant toutes les briques. Votre mission pour la fin de la semaine est de créer une page HTML sémantique complète.

**Sujet au Choix :**
1.  **Page de Recette :** Finalisez et enrichissez la page `recette.html` que nous avons construite ensemble.
2.  **CV en Ligne :** Créez une nouvelle page `cv.html` qui présente votre parcours.

**Contraintes Obligatoires :**
- Le code doit être valide (utilisez le [W3C Validator](https://validator.w3.org/)).
- Utiliser la structure sémantique complète (`<header>`, `<main>`, `<footer>`, `<section>`).
- Contenir au moins un titre de chaque niveau de `<h1>` à `<h3>`.
- Contenir au moins une liste (`<ul>` ou `<ol>`), une image (`<img>`), un lien (`<a>`), un tableau (`<table>`) et un formulaire (`<form>`).
- Tous les attributs `alt` pour les images et `for` pour les labels doivent être présents.

**Livrable :** Un unique fichier `.html` déposé sur votre dépôt GitHub.

#### Synthèse Finale de la Semaine

Félicitations ! Vous êtes parti de zéro et avez construit une page web complète et sémantiquement correcte. Vous avez appris le langage qui structure l'intégralité du web. C'est une base extrêmement solide. La semaine prochaine, nous allons prendre cette page "brute" et la rendre magnifique en apprenant à la styliser avec CSS. Préparez-vous à ajouter des couleurs, des polices et à contrôler la mise en page 