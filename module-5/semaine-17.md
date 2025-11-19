## Semaine 17 : Les Fondamentaux de PHP

### J1 : Votre Premier Script PHP avec Laragon - Syntaxe et Variables

**Objectif(s) du Jour :**
- Comprendre le rôle de PHP en tant que langage de script côté serveur.
- Découvrir et utiliser Laragon comme environnement de développement tout-en-un.
- Écrire et exécuter son premier script PHP en utilisant le workflow de Laragon.
- Maîtriser la syntaxe de base : balises PHP, variables, types de données et commentaires.

**Notion Clé : Le Chef Cuisinier en Coulisses**
Imaginez un restaurant. Le client (le **navigateur**) voit un menu (la page **HTML**). Quand il passe une commande (fait une **requête**), cette commande ne va pas directement au menu, elle va en cuisine.
**PHP** est le **chef cuisinier** qui travaille en coulisses, sur le **serveur**. Il reçoit la commande, la lit, prépare un plat spécial et personnalisé (par exemple, il va chercher le nom de l'utilisateur dans une base de données), puis il met ce plat dans une assiette (génère du **HTML**) et l'envoie au client. Le client ne voit jamais la cuisine ou le chef, il ne voit que le plat final. La grande particularité de PHP est qu'il peut mélanger ses instructions directement dans la "recette" HTML.

---

#### Leçon

##### 1. Environnement de Développement avec Laragon

Oubliez les configurations complexes. **Laragon** est une boîte à outils portable et puissante qui installe et gère pour vous tout ce dont vous avez besoin : un serveur web (Apache), PHP, une base de données (MySQL), et bien plus. Son grand avantage est sa simplicité et ses "jolies URL".

**Le workflow avec Laragon :**
1.  **Démarrer :** Lancez Laragon et cliquez sur "Start All".
2.  **Créer un projet :** C'est la magie de Laragon. Au lieu de créer manuellement des dossiers, vous pouvez faire un clic droit sur l'icône de Laragon dans la barre des tâches > "Create website" > "Blank". Laragon va créer le dossier pour vous et configurer automatiquement une "jolie URL".
3.  **Emplacement des fichiers :** Vos projets se trouvent dans le dossier `C:\laragon\www`.
4.  **Accès au projet :** Si vous nommez votre projet `mon-site`, vous n'y accéderez pas via `localhost/mon-site`, mais via une URL bien plus propre : `http://mon-site.test`.

##### 2. Syntaxe de Base

- Un script PHP commence par `<?php` et se termine par `?>`.
- Chaque instruction se termine par un point-virgule `;`.
- On peut insérer des blocs PHP n'importe où dans un fichier HTML.

##### 3. Variables et Types

- Les variables commencent toujours par un dollar `$`. Ex: `$nom = "Alice";`.
- PHP a des types de données similaires à JavaScript : `string`, `integer`, `float`, `boolean`, `array`, `object`.
- L'opérateur de concaténation pour les chaînes de caractères est le point `.`.

- **Exemple de Code (Votre première page PHP) :**
  ```php
  <!DOCTYPE html>
  <html lang="fr">
  <head>
      <title>Ma Première Page PHP avec Laragon</title>
  </head>
  <body>
      <h1>Bonjour, le monde !</h1>

      <?php
          // Ceci est un commentaire sur une ligne
          /* Ceci est un commentaire
             sur plusieurs lignes */
          
          $nom_visiteur = "Alice";
          $age_visiteur = 30;
      ?>

      <p>
          Le visiteur s'appelle 
          <?php echo $nom_visiteur; ?> 
          et il a 
          <?php echo $age_visiteur; ?> 
          ans.
      </p>
      
      <!-- Syntaxe alternative plus concise -->
      <p>Bienvenue, <?= $nom_visiteur ?> !</p>
      
      <!-- Concaténation -->
      <?php echo '<p>Message concaténé : ' . $nom_visiteur . ' est ici.</p>'; ?>

  </body>
  </html>
  ```
  `<?= ... ?>` est un raccourci pour `<?php echo ...; ?>`.

---

#### Mise en Pratique

1.  **Démarrez Laragon :** Lancez l'application et cliquez sur le bouton "Start All". Vérifiez que les services "Apache" et "MySQL" sont bien en vert.

2.  **Créez votre projet :** Faites un clic droit sur l'icône de Laragon dans la barre des tâches (près de l'horloge), puis allez dans `Create website` et choisissez `Blank`. Quand il vous demande un nom de projet, tapez `bootcamp-php` et validez.

3.  **Trouvez votre projet :** Laragon a automatiquement créé un dossier `C:\laragon\www\bootcamp-php`. Allez dans ce dossier. Vous y trouverez un fichier `index.php` par défaut.

4.  **Modifiez votre premier fichier :** Ouvrez ce fichier `index.php` avec votre éditeur de code (VS Code).

5.  **Écrivez le code :** Supprimez tout le contenu du fichier et remplacez-le par l'exemple de code fourni dans la leçon ci-dessus. Enregistrez le fichier.

6.  **Visualisez le résultat :** Ouvrez votre navigateur web (Chrome, Firefox...) et allez à l'adresse magique que Laragon a créée pour vous : `http://bootcamp-php.test`. Vous devriez voir votre page avec les variables PHP affichées.

#### Mini-Exercice du Jour

Créez un nouveau fichier `calcul.php` dans votre dossier `C:\laragon\www\bootcamp-php`. Déclarez deux variables `$nombre1` et `$nombre2`. Affichez le résultat de leur addition, soustraction, multiplication et division directement dans le HTML. Accédez-y via `http://bootcamp-php.test/calcul.php`.

#### Synthèse

Vous avez fait vos premiers pas dans un nouvel écosystème backend en utilisant un environnement de développement moderne et efficace. Vous comprenez comment PHP s'intègre au HTML pour générer du contenu dynamique et comment Laragon simplifie radicalement la création et l'accès à vos projets. Demain, nous allons explorer les structures de contrôle (conditions, boucles) et les fonctions pour ajouter de la logique à nos scripts.
---

### J2 : Logique et Structure - Conditions, Boucles et Fonctions

**Objectif(s) du Jour :**
- Utiliser les structures conditionnelles (`if`, `else`, `switch`) en PHP.
- Parcourir des données avec les boucles (`for`, `while`, `foreach`).
- Définir et appeler des fonctions pour organiser et réutiliser le code.
- Comprendre la différence entre `include` et `require`.

**Notion Clé : La Recette de Cuisine Modulaire**
Si votre script PHP est une recette de cuisine, les structures de contrôle et les fonctions en sont les instructions et les sous-préparations.
- **Conditions (`if`) :** "Si le four est préchauffé, enfournez le plat. Sinon, attendez."
- **Boucles (`foreach`) :** "Pour chaque pomme dans le panier, épluchez-la."
- **Fonctions (`function`) :** C'est une sous-recette que vous pouvez appeler plusieurs fois. Au lieu de réécrire "mélanger la farine, le sucre et les œufs" à chaque fois, vous créez une fonction `preparerLaPate()` et vous l'appelez quand vous en avez besoin.
- **`include` / `require` :** C'est comme dire "Pour la sauce, référez-vous à la recette de la page 12 de mon livre de cuisine". Cela permet de découper une longue recette en plusieurs fichiers plus lisibles.

---

#### Leçon

##### 1. Conditions et Boucles

La syntaxe est très similaire à celle de JavaScript.
```php
$age = 18;
if ($age >= 18) {
  echo "Vous êtes majeur.";
} else {
  echo "Vous êtes mineur.";
}

$fruits = ["Pomme", "Banane", "Orange"];
foreach ($fruits as $fruit) {
  echo "<p>" . $fruit . "</p>";
}
```

##### 2. Fonctions

```php
function saluer($nom) {
  return "Bonjour, " . $nom . " !";
}

echo saluer("Bob"); // Affiche "Bonjour, Bob !"
```

##### 3. Inclure des Fichiers

`include` et `require` permettent d'insérer le contenu d'un autre fichier PHP.
- `include 'header.php';` : Si le fichier n'est pas trouvé, affiche un avertissement et continue l'exécution.
- `require 'database.php';` : Si le fichier n'est pas trouvé, provoque une erreur fatale et arrête le script. À utiliser pour les fichiers essentiels.

- **Exemple de Code (Structure modulaire) :**
  ```php
  // fichier: header.php
  <header><h1>Mon Site</h1></header>

  // fichier: footer.php
  <footer><p>&copy; 2023</p></footer>

  // fichier: index.php
  <!DOCTYPE html>
  <html>
  <body>
    <?php require 'header.php'; ?>
    <main><p>Contenu de la page...</p></main>
    <?php require 'footer.php'; ?>
  </body>
  </html>
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour2.php`.
2.  Déclarez un tableau de noms. Utilisez une boucle `foreach` pour afficher chaque nom dans un élément de liste `<li>`.
3.  Créez une fonction `calculerAge($anneeDeNaissance)` qui retourne l'âge. Appelez-la et affichez le résultat.
4.  Créez une structure de site avec `index.php`, `header.php` et `footer.php` comme dans l'exemple et faites-la fonctionner.

#### Mini-Exercice du Jour

Créez un tableau associatif (équivalent d'un objet en JS) `$produit = ["nom" => "T-shirt", "prix" => 15];`. Créez une fonction `afficherProduit($produit)` qui génère le HTML pour afficher le nom et le prix du produit.

#### Synthèse

Votre code PHP est maintenant plus structuré et logique. Vous savez comment répéter des actions, prendre des décisions et organiser votre code en blocs réutilisables. Demain, nous allons voir comment PHP gère les données envoyées par l'utilisateur via les formulaires, grâce aux superglobales.

---

### J3 : Interagir avec l'Utilisateur - Les Superglobales

**Objectif(s) du Jour :**
- Comprendre ce que sont les variables superglobales.
- Récupérer des données depuis l'URL avec `$_GET`.
- Traiter les données d'un formulaire avec `$_POST`.
- Comprendre les bases de la sécurité : ne jamais faire confiance aux données de l'utilisateur (`htmlspecialchars`).

**Notion Clé : Les Boîtes aux Lettres Magiques**
Les **superglobales** sont des variables spéciales, créées par PHP, qui sont accessibles depuis n'importe où dans votre code. Elles sont comme des boîtes aux lettres magiques pour communiquer avec le monde extérieur.
- **`$_GET` :** C'est la boîte aux lettres pour les **messages écrits sur une carte postale**. L'URL est `page.php?nom=Alice&ville=Paris`. Tout le monde peut voir le message. PHP met automatiquement `["nom" => "Alice", "ville" => "Paris"]` dans la boîte `$_GET`.
- **`$_POST` :** C'est la boîte aux lettres pour les **lettres scellées dans une enveloppe**. Quand vous soumettez un formulaire avec `method="POST"`, les données sont envoyées dans le corps de la requête, de manière invisible. PHP les dépose dans la boîte `$_POST`.

---

#### Leçon

##### 1. `$_GET`

Utilisé pour récupérer des paramètres depuis l'URL.

```php
// URL: /profil.php?id=123
$userId = $_GET['id']; // $userId vaut "123"
```

##### 2. `$_POST`

Utilisé pour récupérer les données d'un formulaire HTML envoyé avec la méthode `POST`.

- **Exemple de Code (Formulaire de connexion) :**
  ```html
  <!-- fichier: login.php -->
  <form action="traitement.php" method="POST">
      <label for="email">Email :</label>
      <input type="email" name="email" id="email">
      
      <label for="password">Mot de passe :</label>
      <input type="password" name="password" id="password">
      
      <button type="submit">Se connecter</button>
  </form>
  ```
  ```php
  // fichier: traitement.php
  <?php
  // On vérifie si les données ont bien été envoyées
  if (isset($_POST['email']) && isset($_POST['password'])) {
      // Important : Toujours nettoyer les données de l'utilisateur !
      $email = htmlspecialchars($_POST['email']);
      $password = htmlspecialchars($_POST['password']);
      
      echo "Tentative de connexion avec l'email : " . $email;
  } else {
      echo "Veuillez remplir le formulaire.";
  }
  ?>
  ```
- **`htmlspecialchars()` :** Une fonction de sécurité cruciale qui convertit les caractères spéciaux HTML (`<`, `>`) en leurs entités (`&lt;`, `&gt;`). Cela empêche un utilisateur d'injecter du code HTML ou JavaScript malveillant dans votre page (attaque XSS).

---

#### Mise en Pratique

1.  Créez une page `formulaire.php` contenant un formulaire simple qui demande un nom et qui envoie ses données en `POST` à une page `salutation.php`.
2.  Créez la page `salutation.php` qui récupère le nom depuis `$_POST`, le nettoie avec `htmlspecialchars`, et affiche un message "Bonjour, [nom] !".
3.  Testez votre formulaire.

#### Mini-Exercice du Jour

Créez une page `produits.php` qui affiche une liste de liens comme `<a href="detail.php?id=1">Produit 1</a>`, `<a href="detail.php?id=2">Produit 2</a>`. Créez ensuite la page `detail.php` qui récupère l'ID depuis `$_GET` et affiche "Vous consultez la page du produit numéro [id]".

#### Synthèse

Vous savez maintenant comment recevoir et traiter des données de l'utilisateur, ce qui est le cœur de toute application web interactive. La sécurité est primordiale, ne l'oubliez jamais ! Demain, nous verrons comment conserver des informations sur l'utilisateur d'une page à l'autre grâce aux sessions.

---

### J4 : Se Souvenir de l'Utilisateur - Les Sessions (`$_SESSION`)

**Objectif(s) du Jour :**
- Comprendre le problème de la nature "sans état" de HTTP.
- Démarrer et utiliser une session avec `session_start()`.
- Stocker et récupérer des données dans la superglobale `$_SESSION`.
- Mettre en place un système de connexion/déconnexion simple.

**Notion Clé : Le Ticket de Vestiaire**
HTTP est amnésique. Chaque fois que vous chargez une page, le serveur vous a complètement oublié. Comment faire pour qu'il se souvienne que vous êtes "Alice" et que vous êtes connectée ?
Les **sessions** sont la solution.
1.  Quand vous vous connectez, le serveur vous donne un **ticket de vestiaire unique** (un ID de session) et le stocke dans un cookie de votre navigateur. En même temps, dans sa propre arrière-salle (sur le serveur), il ouvre une **boîte de rangement** portant le même numéro que votre ticket.
2.  Dans cette boîte (`$_SESSION`), il peut stocker des informations sur vous : `$_SESSION['user_name'] = 'Alice'`.
3.  À chaque nouvelle page que vous visitez, votre navigateur présente automatiquement votre ticket de vestiaire. Le serveur regarde le numéro, retrouve la bonne boîte de rangement, et sait immédiatement qui vous êtes.

---

#### Leçon

##### 1. Démarrer une Session

Il faut appeler `session_start();` **au tout début** de chaque page où vous voulez utiliser les sessions, avant toute sortie HTML.

##### 2. Manipuler `$_SESSION`

C'est un tableau associatif comme les autres.
- **Stocker :** `$_SESSION['cle'] = 'valeur';`
- **Récupérer :** `$valeur = $_SESSION['cle'];`
- **Vérifier :** `isset($_SESSION['cle'])`
- **Détruire une variable :** `unset($_SESSION['cle']);`
- **Détruire toute la session :** `session_destroy();`

- **Exemple de Code (Système de connexion simple) :**
  ```php
  // fichier: login_process.php
  session_start();
  // (Après avoir vérifié le mot de passe...)
  $_SESSION['user_email'] = $email_verifie;
  header('Location: profil.php'); // Redirige l'utilisateur
  exit();

  // fichier: profil.php
  session_start();
  if (!isset($_SESSION['user_email'])) {
    header('Location: login.php'); // Si pas connecté, renvoyer au login
    exit();
  }
  $email = $_SESSION['user_email'];
  echo "<h1>Bienvenue sur votre profil, $email !</h1>";
  
  // fichier: logout.php
  session_start();
  session_destroy();
  header('Location: login.php');
  exit();
  ```

---

#### Mise en Pratique

1.  Créez un système de connexion simple avec `login.php` (le formulaire) et `dashboard.php` (la page protégée).
2.  Sur une page de traitement, simulez une connexion réussie et stockez l'email de l'utilisateur dans `$_SESSION['email']`.
3.  Sur `dashboard.php`, vérifiez si `$_SESSION['email']` existe. Si non, redirigez vers `login.php`. Si oui, affichez un message de bienvenue.
4.  Créez une page `logout.php` qui détruit la session.

#### Mini-Exercice du Jour

Créez un compteur de pages vues. Sur chaque page de votre site, incrémentez une variable `$_SESSION['page_views']` et affichez sa valeur.

#### Synthèse

Vous savez maintenant gérer un état persistant pour vos utilisateurs, ce qui permet de créer des espaces membres et des expériences personnalisées. La semaine prochaine, en découvrant Laravel, vous verrez que le framework rend cette gestion encore plus simple et sécurisée. Pour finir la semaine, une brève introduction à la POO.

---

### J5 : Introduction à la Programmation Orientée Objet (POO) en PHP

**Objectif(s) du Jour :**
- Comprendre les concepts de base de la POO : classes, objets, propriétés, méthodes.
- Définir une classe simple en PHP.
- Instancier un objet à partir d'une classe.
- Utiliser les propriétés et les méthodes d'un objet.

**Notion Clé : Le Plan de la Voiture**
Jusqu'à présent, vous avez manipulé des données et des fonctions séparément. La POO regroupe les données et les fonctions qui les manipulent en une seule entité.
- **Une Classe :** C'est le **plan de construction** d'une voiture. Le plan (`class Voiture`) définit les caractéristiques qu'une voiture doit avoir (ses **propriétés** : `$couleur`, `$marque`) et ce qu'elle peut faire (ses **méthodes** : `demarrer()`, `accelerer()`).
- **Un Objet :** C'est une **voiture réelle** construite à partir du plan. `$maVoiture = new Voiture();` crée une instance spécifique. `$maVoiture` est un objet. On peut alors interagir avec lui : `$maVoiture->couleur = 'rouge';`, `$maVoiture->demarrer();`.

---

#### Leçon

##### Syntaxe d'une Classe

```php
class User {
  // Propriétés (les données)
  public $email;
  public $username;
  
  // Constructeur : méthode spéciale appelée lors de la création de l'objet
  public function __construct($email, $username) {
    $this->email = $email;
    $this->username = $username;
  }
  
  // Méthode (les actions)
  public function sayHello() {
    return "Bonjour, je suis " . $this->username . ".";
  }
}

// Instanciation : on crée un objet
$user1 = new User('alice@email.com', 'Alice');
$user2 = new User('bob@email.com', 'Bob');

// Utilisation
echo $user1->email; // Affiche 'alice@email.com'
echo $user2->sayHello(); // Affiche "Bonjour, je suis Bob."
```
- `$this` fait référence à l'objet courant, comme en JavaScript.
- `->` est l'opérateur pour accéder aux propriétés et méthodes d'un objet.

---

#### PROJET DE LA SEMAINE : Site Dynamique avec Formulaire de Contact

Votre mission est de synthétiser toutes les connaissances de la semaine pour créer un petit site web dynamique.

**Structure et Fonctionnalités Obligatoires :**

1.  **Structure du Site :**
    - Un site de 3 pages (ex: Accueil, À propos, Contact).
    - Utilisez `require` pour inclure un `header.php` et un `footer.php` communs sur toutes les pages.

2.  **Page de Contact (`contact.php`) :**
    - Doit contenir un formulaire avec des champs pour le nom, l'email et un message.
    - Le formulaire doit envoyer ses données en `POST` à une page de traitement (`process_contact.php`).

3.  **Page de Traitement (`process_contact.php`) :**
    - Doit récupérer les données du formulaire (`$_POST`).
    - Doit effectuer une validation simple (vérifier que les champs ne sont pas vides).
    - Doit nettoyer les données avec `htmlspecialchars`.
    - (Partie projet) Simulez l'envoi d'un email. Utilisez la fonction `mail()` de PHP si votre environnement est configuré, sinon, écrivez simplement les données dans un fichier texte `messages.log` en utilisant `file_put_contents('messages.log', $data, FILE_APPEND);`.
    - (Bonus POO) Créez une classe `Message` avec des propriétés pour le nom, l'email et le texte. Dans `process_contact.php`, instanciez un nouvel objet `Message` avec les données du formulaire.
    - Après le traitement, redirigez l'utilisateur vers une page de remerciement (`merci.php`) en utilisant `header('Location: merci.php');`.

**Livrable :** Un dépôt GitHub contenant les fichiers de votre projet de site dynamique. Le `README.md` doit expliquer comment le lancer localement.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez appris les bases d'un des langages les plus répandus du web. Vous savez créer des pages dynamiques, gérer des formulaires, maintenir une session utilisateur et vous avez eu un premier aperçu de la puissance de la POO. Vous êtes maintenant prêt à découvrir comment un framework comme Laravel décuple la puissance de PHP et simplifie radicalement le développement.