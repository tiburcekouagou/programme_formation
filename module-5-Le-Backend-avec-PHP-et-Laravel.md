# Module 6 : La Puissance d'un Framework Intégré - Le Backend avec PHP & Laravel

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Comprendre les bases de la syntaxe et du fonctionnement de PHP.
- Maîtriser le pattern MVC (Modèle-Vue-Contrôleur) tel qu'implémenté par Laravel.
- Utiliser l'outil en ligne de commande `artisan` pour accélérer le développement.
- Gérer la structure d'une base de données SQL avec les **migrations**.
- Interagir avec la base de données de manière élégante grâce à l'ORM **Eloquent**.
- Créer des interfaces utilisateur dynamiques rendues côté serveur avec le moteur de template **Blade**.
- Implémenter un système d'authentification complet en quelques commandes.
- Construire une application web monolithique complète, de la base de données à l'interface.

## 2. Prérequis

- Avoir complété le **Module 5 (Node.js & Express)**. Vous comprenez déjà les concepts de backend, de routes, d'API, de base de données et d'authentification.
- Un environnement de développement local pour PHP et Laravel. Nous recommandons :
  - **Windows :** [Laragon](https://laragon.org/)
  - **Mac :** [Laravel Herd](https://herd.laravel.com/)
- Avoir installé **Composer**, le gestionnaire de dépendances pour PHP.

## 3. Résumé du Concept (Qu'est-ce que PHP & Laravel ?)

Vous avez appris à construire votre backend avec Node.js et Express, en assemblant vous-même chaque pièce (le routeur, l'ORM, l'authentification...). C'est une approche flexible et puissante.

Laravel propose une philosophie différente : c'est un framework **"batteries-incluses"** et **opinionated**. Il vous fournit une structure de projet complète et une boîte à outils extrêmement riche pour toutes les tâches courantes du développement web. Il a une "opinion" sur la meilleure façon d'organiser votre code, ce qui, en retour, vous rend incroyablement productif.

Oubliez l'assemblage : Laravel vous donne une voiture de sport clé en main. Vous voulez un système de connexion ? C'est une commande. Gérer votre base de données ? Les migrations sont là pour ça. Interagir avec vos données ? L'ORM Eloquent est d'une simplicité redoutable. Afficher des données ? Le moteur de template Blade est intégré.

Votre mission est d'apprendre à piloter cette voiture de sport, en maîtrisant ses conventions pour construire des applications robustes et complètes à une vitesse impressionnante.

## 4. Plan d’Apprentissage

*   **Chapitre 1 : PHP et l'écosystème Laravel**
    *   Bases de la syntaxe PHP (variables, tableaux, fonctions)
    *   Installer un projet Laravel avec Composer
    *   Découvrir la structure des dossiers et l'outil `artisan`
*   **Chapitre 2 : Le Flux MVC : Routes, Contrôleurs, Vues**
    *   Définir des routes dans `routes/web.php`
    *   Créer un `Controller` pour la logique métier
    *   Créer une `View` avec le moteur de template Blade
*   **Chapitre 3 : La Base de Données avec Eloquent**
    *   Les **Migrations** : le versioning de votre base de données
    *   Les **Modèles Eloquent** : votre interface avec les tables
    *   Interroger la base de données (find, where, get...)
*   **Chapitre 4 : La Puissance de Blade**
    *   Afficher des variables `{{ }}`
    *   Structures de contrôle (`@if`, `@foreach`)
    *   Layouts et héritage (`@extends`, `@section`)
*   **Chapitre 5 : Gestion des Formulaires et CRUD**
    *   Créer un formulaire et le protéger contre les attaques CSRF (`@csrf`)
    *   Valider les données entrantes avec les `Form Requests`
    *   Implémenter la logique CRUD dans un contrôleur
*   **Chapitre 6 : La Magie de Laravel : Authentification & Relations**
    *   Installer un kit de démarrage comme Laravel Breeze
    *   Protéger des routes avec le middleware `auth`
    *   Définir des relations entre les modèles (ex: un `User` a plusieurs `Posts`)

## 5. Leçons

### Leçon 1 : PHP et l'écosystème Laravel

Avant de courir, il faut marcher. Un rapide tour de la syntaxe PHP est nécessaire. Ensuite, on plonge dans Laravel en créant notre premier projet et en découvrant `artisan`, notre couteau suisse en ligne de commande.

- **Exemple de code simple (Syntaxe PHP) :**
  ```php
  <?php
  // Les variables commencent par $
  $nom = "Alice";
  echo "Bonjour, " . $nom; // Concaténation avec le point

  // Un tableau associatif (similaire à un objet JS)
  $utilisateur = [
      "nom" => "Bob",
      "age" => 30
  ];
  echo $utilisateur["nom"];
  ?>
  ```
- **Exemple de code appliqué (Créer un projet et une première route) :**
  *Dans votre terminal*
  ```bash
  # Installe le projet "mon-blog"
  composer create-project laravel/laravel mon-blog
  cd mon-blog
  # Démarre le serveur de développement
  php artisan serve
  ```

### Leçon 2 : Le Flux MVC : Routes, Contrôleurs, Vues

C'est le cycle de vie d'une requête dans Laravel. Une URL (la **Route**) est interceptée, elle appelle une méthode dans un **Contrôleur**. Le Contrôleur fait son travail (ex: récupérer des données) et renvoie une **Vue** qui sera affichée à l'utilisateur.

- **Exemple de code simple :**
  *Fichier `routes/web.php`*
  ```php
  use App\Http\Controllers\HomeController;
  
  Route::get('/', [HomeController::class, 'index']);
  ```
  *Fichier `app/Http/Controllers/HomeController.php`*
  ```php
  class HomeController extends Controller {
      public function index() {
          return view('welcome'); // Renvoie la vue 'resources/views/welcome.blade.php'
      }
  }
  ```
- **Exemple de code appliqué (Passer des données à une vue) :**
  *Fichier `app/Http/Controllers/HomeController.php`*
  ```php
  public function index() {
      $nom = "Jeanne";
      return view('welcome', ['nom' => $nom]); // On passe la variable 'nom' à la vue
  }
  ```
  *Fichier `resources/views/welcome.blade.php`*
  ```html
  <!-- On peut maintenant utiliser la variable directement -->
  <h1>Bonjour, {{ $nom }} !</h1>
  ```

### Leçon 3 : La Base de Données avec Eloquent

On ne touche plus directement à la base de données. Les **migrations** décrivent la structure de nos tables en PHP. Les **modèles Eloquent** sont des classes PHP qui représentent ces tables, nous permettant de manipuler les données comme de simples objets.

- **Exemple de code simple (Créer une migration et un modèle) :**
  *Dans votre terminal*
  ```bash
  # Crée le fichier de migration ET le fichier de modèle Post.php
  php artisan make:model Post -m 
  ```
  *Fichier `database/migrations/xxxx_create_posts_table.php`*
  ```php
  Schema::create('posts', function (Blueprint $table) {
      $table->id(); // Crée une colonne 'id' auto-incrémentée
      $table->string('title');
      $table->text('content');
      $table->timestamps(); // Crée les colonnes 'created_at' et 'updated_at'
  });
  ```
- **Exemple de code appliqué (Récupérer des données avec Eloquent) :**
  *Fichier `app/Http/Controllers/PostController.php`*
  ```php
  use App\Models\Post; // Important d'importer le modèle

  public function index() {
      // Récupère tous les articles de la table 'posts' et les trie par date de création
      $posts = Post::latest()->get(); 
      
      // Renvoie la vue 'posts.index' en lui passant les articles
      return view('posts.index', ['posts' => $posts]);
  }
  ```

### Leçon 4 : La Puissance de Blade

Blade est un moteur de template qui rend la création de vues dynamique et simple. Sa syntaxe est claire et il permet de créer des layouts réutilisables pour éviter de répéter le code HTML commun (`<head>`, `<body>`, navigation...).

- **Exemple de code simple :**
  *Fichier `resources/views/posts/index.blade.php`*
  ```html
  @if (count($posts) > 0)
    <ul>
      @foreach ($posts as $post)
        <li>{{ $post->title }}</li>
      @endforeach
    </ul>
  @else
    <p>Aucun article trouvé.</p>
  @endif
  ```
- **Exemple de code appliqué (Créer un layout de base) :**
  *Fichier `resources/views/layouts/app.blade.php` (le layout parent)*
  ```html
  <html>
  <head><title>Mon Blog</title></head>
  <body>
    <div class="container">
      @yield('content') <!-- Le contenu spécifique à la page viendra ici -->
    </div>
  </body>
  </html>
  ```
  *Fichier `resources/views/posts/index.blade.php` (la page enfant)*
  ```html
  @extends('layouts.app') <!-- Hérite du layout app.blade.php -->

  @section('content')
    <h1>Liste des articles</h1>
    <!-- ... le code avec @foreach ... -->
  @endsection
  ```

### Leçon 5 : Gestion des Formulaires et CRUD

Laravel simplifie et sécurise la gestion des formulaires. L'arobase `@csrf` est une protection essentielle. La validation des données est intégrée et très puissante.

- **Exemple de code simple (Un formulaire de création) :**
  *Fichier `resources/views/posts/create.blade.php`*
  ```html
  <form action="/posts" method="POST">
    @csrf <!-- Protection CSRF obligatoire -->
    <input type="text" name="title">
    <button type="submit">Créer</button>
  </form>
  ```
- **Exemple de code appliqué (Logique de stockage dans le contrôleur) :**
  *Fichier `app/Http/Controllers/PostController.php`*
  ```php
  public function store(Request $request) {
      // Valider les données de la requête
      $validated = $request->validate([
          'title' => 'required|unique:posts|max:255',
          'content' => 'required',
      ]);
      
      // Créer un nouveau post avec les données validées
      Post::create($validated);
      
      // Rediriger vers la liste des articles avec un message de succès
      return redirect('/posts')->with('success', 'Article créé !');
  }
  ```

### Leçon 6 : La Magie de Laravel : Authentification & Relations

C'est là que Laravel brille. En quelques commandes, on peut mettre en place un système complet de connexion/inscription. Ensuite, on peut définir des relations entre nos données (un utilisateur a plusieurs articles, un article appartient à un utilisateur).

- **Exemple de code simple (Installer Laravel Breeze et protéger une route) :**
  *Dans votre terminal*
  ```bash
  composer require laravel/breeze --dev
  php artisan breeze:install
  npm install && npm run dev
  ```
  *Fichier `routes/web.php`*
  ```php
  // Seul un utilisateur connecté pourra accéder à la page de création d'article
  Route::get('/posts/create', [PostController::class, 'create'])->middleware('auth');
  ```
- **Exemple de code appliqué (Définir et utiliser une relation) :**
  *Fichier `app/Models/User.php`*
  ```php
  public function posts() {
    return $this->hasMany(Post::class); // Un utilisateur a plusieurs articles
  }
  ```
  *Fichier `app/Models/Post.php`*
  ```php
  public function user() {
    return $this->belongsTo(User::class); // Un article appartient à un utilisateur
  }
  ```
  *Utilisation dans une vue Blade*
  ```html
  <p>Auteur : {{ $post->user->name }}</p> <!-- Accès magique à l'auteur de l'article ! -->
  ```

## 6. Exercices Pratiques

- **Niveau Débutant : Page "À Propos"**
  Créez une route `/about` qui pointe vers une méthode `about` dans un `PageController`. Cette méthode doit renvoyer une vue `about.blade.php` qui hérite de votre layout de base et affiche un simple texte de présentation.

- **Niveau Intermédiaire : Liste de Tâches (sans BDD)**
  Créez une page qui affiche une liste de tâches stockées en dur dans un tableau PHP dans votre contrôleur. La vue doit utiliser une boucle `@foreach` pour afficher chaque tâche.

- **Niveau Avancé : Mini-Gallerie d'Images**
  Créez un CRUD complet pour une galerie d'images. Un modèle `Image` avec un champ `url` et `caption`. L'utilisateur doit pouvoir voir la liste des images, ajouter une nouvelle image via un formulaire, et la supprimer. Le tout doit être connecté à une base de données.

## 7. Mini-projet Guidé : Un Livre d'Or (Guestbook)

On va construire un livre d'or simple où les visiteurs peuvent laisser un message.

1.  **Étape 1 : Modèle et Migration**
    Exécutez `php artisan make:model Message -m`. Dans la migration, ajoutez un champ `name` (string) et `body` (text). Exécutez `php artisan migrate`.

2.  **Étape 2 : Routes et Contrôleur**
    Exécutez `php artisan make:controller MessageController`. Dans `routes/web.php`, créez une route `GET /` qui pointe vers la méthode `index` du contrôleur, et une route `POST /` qui pointe vers la méthode `store`.

3.  **Étape 3 : Afficher les Messages (index)**
    Dans la méthode `index`, récupérez tous les messages avec `Message::latest()->get()` et renvoyez une vue `guestbook.blade.php` en leur passant les messages.

4.  **Étape 4 : La Vue et le Formulaire**
    Dans `guestbook.blade.php`, créez une boucle `@foreach` pour afficher les messages existants. En dessous, créez un formulaire qui pointe vers la route `POST /` avec les champs `name` et `body`, sans oublier le `@csrf`.

5.  **Étape 5 : Stocker le Nouveau Message (store)**
    Dans la méthode `store`, validez les données entrantes. Si elles sont valides, créez un nouveau message avec `Message::create(...)` et redirigez l'utilisateur vers la page d'accueil.

## 8. Projet Final Non Guidé : Un Forum de Discussion Simple

Créez une application Laravel complète qui fonctionne comme un forum basique.

**Livrables :**
1.  Un dépôt GitHub contenant le code complet de votre application Laravel.
2.  Un `README.md` expliquant comment installer et lancer le projet.

**Fonctionnalités requises :**
- **Authentification complète :** Utilisez Laravel Breeze. Les utilisateurs doivent pouvoir s'inscrire, se connecter et se déconnecter.
- **Gestion des Sujets de Discussion (Threads) :**
  - Seuls les utilisateurs connectés peuvent créer un nouveau sujet de discussion.
  - Tous les utilisateurs (même non connectés) peuvent voir la liste des sujets.
  - Chaque sujet a un titre et un contenu. Il est lié à l'utilisateur qui l'a créé.
  - L'auteur d'un sujet doit pouvoir le modifier ou le supprimer.
- **Gestion des Réponses (Replies) :**
  - Les utilisateurs connectés peuvent répondre à un sujet existant.
  - Chaque réponse est liée à un sujet et à l'utilisateur qui l'a postée.
- **Relations Eloquent :** Les relations `User-Thread`, `User-Reply`, et `Thread-Reply` doivent être correctement implémentées.
- **Design :** L'interface doit être propre et responsive. Vous pouvez utiliser un framework CSS simple comme [Tailwind CSS](https://tailwindcss.com/) (inclus avec Breeze) ou [Bootstrap](https://getbootstrap.com/).

## 9. Critères d'Évaluation

- **Respect des conventions Laravel :** Le code est-il bien organisé ? Artisan, Eloquent, Blade sont-ils utilisés correctement ?
- **Architecture MVC :** La logique est-elle au bon endroit (contrôleurs) et non dans les routes ou les vues ?
- **Base de données :** Les migrations sont-elles bien écrites ? Les relations Eloquent sont-elles fonctionnelles et utilisées efficacement ?
- **Authentification & Autorisation :** Le système de connexion fonctionne-t-il ? Un utilisateur peut-il modifier uniquement son propre contenu ?
- **Qualité du code :** Le code est-il lisible, commenté si nécessaire, et sécurisé (validation des données, protection CSRF) ?

## 10. Ressources Complémentaires Fiables

- **Documentation Officielle de Laravel :** C'est LA bible. Extrêmement bien écrite et complète.
  - [laravel.com/docs](https://laravel.com/docs)
- **Laracasts :** Considéré comme la meilleure plateforme de screencasts vidéo pour apprendre Laravel. La série "Laravel From Scratch" est un incontournable (certaines vidéos sont gratuites).
  - [laracasts.com](https://laracasts.com/)
- **Documentation Officielle de PHP :** Pour toute question sur le langage PHP lui-même.
  - [php.net/manual/fr/](https://www.php.net/manual/fr/)
- **Laravel News :** Le blog officiel pour se tenir au courant des dernières nouveautés de l'écosystème.
  - [laravel-news.com](https://laravel-news.com/)