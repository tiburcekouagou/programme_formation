## Semaine 18 : Introduction à Laravel

### J1 : Le Framework Moderne - Installation et Structure

**Objectif(s) du Jour :**
- Comprendre ce qu'est un framework et les avantages de Laravel (élégance, productivité).
- Découvrir les deux outils clés : Composer (gestionnaire de paquets) et Artisan (outil en ligne de commande).
- Installer un nouveau projet Laravel en utilisant Composer via le terminal de Laragon.
- Explorer la structure de dossiers d'un projet Laravel et comprendre le rôle de chaque répertoire principal.

**Notion Clé : La Boîte de LEGO Professionnelle**
Si le PHP "vanilla" de la semaine dernière, c'était de sculpter du bois brut, **Laravel** est une **boîte de LEGO professionnelle** pour construire des applications web.
- **Composer :** C'est le service de livraison qui vous apporte toutes les briques dont vous avez besoin (Laravel lui-même, et toutes ses dépendances). C'est le NPM du monde PHP.
- **Le projet Laravel :** C'est le kit de démarrage. Il ne contient pas seulement des briques en vrac, mais des modules déjà pré-assemblés et organisés dans des boîtes étiquetées (`app`, `routes`, `resources`...).
- **Artisan :** C'est l'outil magique fourni avec le kit. Au lieu de fabriquer une nouvelle brique à la main, vous tapez une commande comme `artisan make:brique` et l'outil la crée pour vous, parfaitement formée et au bon endroit.

---

#### Leçon

##### 1. Composer et Artisan

- **Composer :** Le gestionnaire de dépendances pour PHP. Il lit un fichier `composer.json` (l'équivalent de `package.json`) et télécharge les librairies nécessaires dans un dossier `vendor/`. Laragon l'inclut par défaut.
- **Artisan :** L'interface en ligne de commande de Laravel. C'est votre meilleur ami. Il vous permet de créer des contrôleurs, des modèles, de gérer les migrations de base de données, et bien plus. On l'utilise avec `php artisan <commande>`.

##### 2. Installation d'un Projet Laravel avec Laragon

Le terminal de Laragon est déjà configuré avec PHP et Composer.
1.  Ouvrez le terminal de Laragon (clic sur le bouton "Terminal").
2.  Assurez-vous d'être dans le dossier `www` (`cd C:\laragon\www`).
3.  Lancez la commande d'installation de Composer :
    `composer create-project laravel/laravel mon-premier-projet`
4.  Attendez que Composer télécharge et installe tout.
5.  Laragon détecte automatiquement le nouveau dossier et crée la "jolie URL" pour vous : `http://mon-premier-projet.test`.

##### 3. Structure d'un Projet Laravel

- `app/` : Le cœur de votre application (Modèles, Contrôleurs...).
- `routes/` : Contient la définition de toutes les URL de votre site.
- `resources/` : Contient les "vues" (votre HTML, avec Blade), les fichiers CSS/JS non compilés.
- `public/` : Le seul dossier accessible publiquement. C'est le point d'entrée de toutes les requêtes.
- `.env` : Fichier de configuration crucial pour votre environnement (connexion à la base de données, clés secrètes...).

---

#### Mise en Pratique

1.  Lancez Laragon et ouvrez son terminal.
2.  Utilisez la commande `composer create-project` pour créer un nouveau projet nommé `blog-laravel`.
3.  Une fois l'installation terminée, ouvrez le dossier `C:\laragon\www\blog-laravel` avec VS Code.
4.  Ouvrez votre navigateur et allez sur `http://blog-laravel.test`. Vous devriez voir la page d'accueil par défaut de Laravel.
5.  Dans le terminal, naviguez dans le dossier de votre projet (`cd blog-laravel`) et lancez `php artisan list` pour voir la liste impressionnante de toutes les commandes disponibles.

#### Mini-Exercice du Jour

Modifiez le fichier `.env` pour changer le nom de l'application : `APP_NAME="Mon Super Blog"`. Même si cela n'a pas d'effet visible immédiat, c'est une première étape pour vous familiariser avec ce fichier crucial.

#### Synthèse

Vous avez franchi le pas le plus important : passer d'un simple fichier `.php` à un framework professionnel structuré. Vous avez installé un projet Laravel et commencé à comprendre comment il est organisé. Demain, nous allons voir comment définir les URL de notre site grâce au système de routage de Laravel.

---

### J2 : Définir les Chemins - Le Routage

**Objectif(s) du Jour :**
- Comprendre comment Laravel gère les requêtes entrantes.
- Découvrir le fichier `routes/web.php`.
- Créer ses premières routes avec la syntaxe `Route::get()`.
- Renvoyer une chaîne de caractères ou une vue simple depuis une route.

**Notion Clé : Le GPS de l'Application**
Oubliez la gestion manuelle des URL avec des `if` sur `$_GET['page']`. Le fichier `routes/web.php` est le **GPS central** de votre application Laravel. Il contient une liste d'adresses (les URL) et la destination exacte pour chacune d'entre elles.
- `Route::get('/', ...)` : "Quand une requête `GET` arrive à la racine du site, va à cette destination."
- `Route::get('/a-propos', ...)` : "Quand une requête `GET` arrive sur `/a-propos`, va à cette autre destination."
C'est propre, déclaratif et incroyablement facile à lire.

---

#### Leçon

##### 1. Le Fichier `routes/web.php`

C'est ici que vous définirez toutes les routes pour votre application web (celles accessibles par un navigateur).

##### 2. Définir une Route Simple

La méthode `Route::get()` prend deux arguments : l'URI (le chemin de l'URL) et une fonction "callback" (une closure) qui définit ce qu'il faut faire.

- **Exemple de Code (routes/web.php) :**
  ```php
  use Illuminate\Support\Facades\Route;

  // Route pour la page d'accueil
  // Retourne la vue 'welcome.blade.php' qui se trouve dans resources/views
  Route::get('/', function () {
      return view('welcome'); 
  });

  // Route pour une page "À propos"
  Route::get('/a-propos', function () {
      return '<h1>Ceci est la page À Propos</h1>'; 
  });
  
  // Route pour une page "Contact"
  Route::get('/contact', function () {
      // Le helper view() cherche un fichier dans `resources/views`
      return view('contact'); // On suppose qu'un fichier 'contact.blade.php' existe
  });
  ```
- `view('nom-de-la-vue')` est une fonction helper de Laravel qui cherche et rend un fichier de vue.

---

#### Mise en Pratique

1.  Dans votre projet `blog-laravel`, ouvrez le fichier `routes/web.php`.
2.  Ajoutez la route `/a-propos` de l'exemple ci-dessus.
3.  Allez sur `http://blog-laravel.test/a-propos` dans votre navigateur. Vous devriez voir le message s'afficher.
4.  Créez un nouveau fichier `contact.blade.php` dans `resources/views/`. Mettez-y un simple `<h1>Page de Contact</h1>`.
5.  Ajoutez la route `/contact` qui retourne `view('contact')`.
6.  Testez `http://blog-laravel.test/contact`.

#### Mini-Exercice du Jour

Créez une route `/salutation/{nom}` qui accepte un paramètre dynamique. La fonction de la route doit retourner "Bonjour, [nom] !". (Indice : `Route::get('/salutation/{nom}', function ($nom) { ... });`).

#### Synthèse

Vous savez maintenant comment intercepter une URL et y répondre. C'est la base de toute application web. Cependant, retourner du HTML brut dans les routes n'est pas pratique. Demain, nous allons explorer le puissant moteur de template de Laravel, Blade, pour créer des vues HTML propres et dynamiques.

---

### J3 : Créer les Interfaces - Vues et Moteur de Template Blade

**Objectif(s) du Jour :**
- Comprendre le rôle du moteur de template Blade.
- Utiliser la syntaxe Blade pour afficher des variables (`{{ }}`) et utiliser des structures de contrôle (`@if`, `@foreach`).
- Créer un layout de base réutilisable avec `@yield` et `@extends`.
- Passer des données depuis une route vers une vue.

**Notion Clé : L'HTML sous Stéroïdes**
Blade est un moteur de template qui vous permet d'écrire du PHP dans vos vues, mais de manière beaucoup plus propre et lisible que `<?php echo ... ?>`. C'est comme avoir des **stencils intelligents** pour votre HTML.
- **`{{ $variable }}` :** Le stencil pour "écrire ici". Il est intelligent car il échappe automatiquement les données (sécurité !).
- **`@if / @endif` :** Le stencil pour les conditions.
- **`@extends` et `@yield` :** C'est le système de stencils le plus puissant. `@extends('layout')` dit "Prends le grand stencil 'layout'". `@section('content')` dit "Voici le contenu que je veux mettre dans la zone 'content' du grand stencil". `@yield('content')` dans le layout est l'emplacement où le contenu sera inséré. Fini les `require 'header.php'` !

---

#### Leçon

##### 1. Syntaxe de Base de Blade

- Afficher une variable : `{{ $nom }}`
- Structures de contrôle : `@if($condition)...@else...@endif`, `@foreach($items as $item)...@endforeach`

##### 2. Passer des Données à une Vue

La fonction `view()` peut prendre un second argument : un tableau associatif de données.

```php
// routes/web.php
Route::get('/', function () {
    $nom = "Alice";
    $taches = ["Apprendre Blade", "Boire un café"];
    return view('accueil', ['name' => $nom, 'tasks' => $taches]);
});
```
```blade
// resources/views/accueil.blade.php
<h1>Bonjour, {{ $name }}</h1>
<ul>
    @foreach($tasks as $task)
        <li>{{ $task }}</li>
    @endforeach
</ul>
```

##### 3. Layouts Blade

```blade
// resources/views/layouts/app.blade.php (le layout principal)
<html>
<head><title>@yield('title', 'Mon Site')</title></head>
<body>
    <header>...</header>
    <main>
        @yield('content')
    </main>
    <footer>...</footer>
</body>
</html>

// resources/views/about.blade.php (une page qui utilise le layout)
@extends('layouts.app')

@section('title', 'Page À Propos')

@section('content')
    <h1>À propos de nous</h1>
    <p>Contenu de la page à propos...</p>
@endsection
```

---

#### Mise en Pratique

1.  Créez un dossier `layouts` dans `resources/views` et, à l'intérieur, un fichier `app.blade.php` avec la structure de base d'un layout.
2.  Modifiez vos vues `welcome.blade.php` et `contact.blade.php` pour qu'elles `@extends` ce nouveau layout.
3.  Dans votre route `/`, passez un tableau de noms à votre vue et affichez-les avec une boucle `@foreach`.

#### Mini-Exercice du Jour

Créez une vue `equipe.blade.php` et la route correspondante. Dans la route, créez un tableau de membres de l'équipe. Utilisez `@foreach` et `@if` dans la vue pour afficher chaque membre, en ajoutant un badge "(Admin)" à côté du nom si le membre a une propriété `isAdmin: true`.

#### Synthèse

Vous savez maintenant créer des pages HTML dynamiques et maintenables de manière professionnelle. La séparation entre la logique (route) et la présentation (vue) est claire. Demain, nous allons introduire la dernière pièce du puzzle MVC : les contrôleurs, pour mieux organiser notre logique.

---

### J4 : Organiser la Logique - Les Contrôleurs

**Objectif(s) du Jour :**
- Comprendre le rôle d'un contrôleur pour organiser la logique de l'application.
- Générer un nouveau contrôleur en utilisant Artisan.
- Déplacer la logique des routes (closures) vers des méthodes de contrôleur.
- Mettre à jour les routes pour qu'elles pointent vers les méthodes de contrôleur.

**Notion Clé : Le Chef de Service**
Jusqu'à présent, le GPS (`routes/web.php`) donnait directement les instructions de travail. Si le travail est complexe, le fichier GPS devient illisible.
Un **Contrôleur**, c'est un **chef de service**. Le GPS se contente désormais de dire : "Pour toute demande concernant la facturation (`/factures`), adressez-vous au service Facturation (`BillingController`)". C'est le `BillingController` qui contient toutes les méthodes spécifiques : `afficherFactures()`, `creerFacture()`, etc. Les routes restent propres et lisibles, et la logique métier est bien rangée dans son propre service.

---

#### Leçon

##### 1. Créer un Contrôleur

On utilise Artisan, notre outil magique.
`php artisan make:controller PageController`
Cette commande crée un fichier `PageController.php` dans `app/Http/Controllers/`.

##### 2. Déplacer la Logique

```php
// app/Http/Controllers/PageController.php
namespace App\Http\Controllers;

use Illuminate\Http\Request;

class PageController extends Controller
{
    // Une méthode pour chaque page
    public function home()
    {
        return view('welcome');
    }

    public function about()
    {
        return view('about');
    }
}
```

##### 3. Mettre à Jour les Routes

On modifie `routes/web.php` pour utiliser la nouvelle syntaxe.

```php
// routes/web.php
use App\Http\Controllers\PageController; // Ne pas oublier d'importer la classe

Route::get('/', [PageController::class, 'home']);
Route::get('/a-propos', [PageController::class, 'about']);
```

---

#### Mise en Pratique

1.  Dans le terminal de votre projet, lancez `php artisan make:controller SiteController`.
2.  Ouvrez le nouveau fichier et créez des méthodes pour vos pages "Accueil", "À Propos" et "Contact".
3.  Déplacez la logique qui renvoie les vues de votre fichier `routes/web.php` vers ces nouvelles méthodes.
4.  Mettez à jour votre fichier de routes pour qu'il appelle les méthodes de votre `SiteController`.
5.  Testez toutes vos pages pour vous assurer que tout fonctionne comme avant.

#### Mini-Exercice du Jour

Générez un contrôleur ressource avec `php artisan make:controller PostController --resource`. Ouvrez le fichier généré. Vous verrez que Laravel a déjà créé des méthodes vides pour toutes les actions CRUD (`index`, `create`, `store`, `show`, `edit`, `update`, `destroy`). C'est un gain de temps énorme !

#### Synthèse

Votre application respecte maintenant pleinement le pattern MVC. Les responsabilités sont clairement séparées : les routes dirigent, les contrôleurs orchestrent, et les vues affichent. C'est une architecture propre, scalable et professionnelle. Vous êtes prêt pour le projet de la semaine.

---

### J5 : Projet de la Semaine - Recréer le Site Dynamique avec Laravel

**Objectif(s) du Jour :**
- Mettre en pratique toutes les notions de la semaine (Artisan, Routing, Blade, Contrôleurs).
- Recréer le projet de la semaine 17 en utilisant la structure et les outils de Laravel.
- Comprendre les gains de productivité et de clarté apportés par le framework.

**Notion Clé : Reconstruire avec des Outils Modernes**
La semaine dernière, vous avez construit une petite cabane avec un marteau et des clous (PHP vanilla). C'était fonctionnel, mais un peu artisanal. Cette semaine, vous avez reçu une visseuse électrique, une scie circulaire et des plans professionnels (Laravel). Votre mission est de reconstruire la même cabane. Vous constaterez que le résultat est non seulement plus rapide à construire, mais aussi beaucoup plus solide, mieux organisé et plus facile à agrandir plus tard.

---

#### PROJET DE LA SEMAINE : Site Dynamique Laravel

Votre mission est de recréer le site de 3 pages avec un formulaire de contact, mais cette fois-ci, en utilisant l'architecture Laravel.

**Structure et Fonctionnalités Obligatoires :**

1.  **Installation :** Un projet Laravel frais, installé avec Composer.

2.  **Layout Blade :**
    - Créez un layout principal `resources/views/layouts/app.blade.php` avec un header (contenant la navigation) et un footer.

3.  **Contrôleur :**
    - Créez un `ContactController` avec Artisan.
    - Il doit contenir une méthode `show()` pour afficher la page de contact, et une méthode `handle()` pour traiter la soumission du formulaire.

4.  **Routes :**
    - Dans `routes/web.php`, définissez les routes suivantes, toutes pointant vers des méthodes de votre contrôleur :
      - `GET /` (qui peut pointer vers une méthode `home` d'un `PageController`, par exemple).
      - `GET /contact` (qui pointe vers `ContactController@show`).
      - `POST /contact` (qui pointe vers `ContactController@handle`).

5.  **Vues :**
    - Créez les vues nécessaires (`home.blade.php`, `contact.blade.php`, `merci.blade.php`), toutes héritant de votre layout principal.
    - La vue `contact.blade.php` doit contenir un formulaire HTML avec la protection CSRF de Laravel (`@csrf`).
      ```blade
      <form action="/contact" method="POST">
          @csrf 
          ...
      </form>
      ```

6.  **Logique du Formulaire :**
    - Dans la méthode `handle(Request $request)` de votre `ContactController`, récupérez les données du formulaire avec `$request->input('nom_du_champ')`.
    - Pour l'instant, ne faites pas de validation complexe. Retournez simplement une vue de remerciement en lui passant les données soumises pour les afficher. `return view('merci', ['data' => $request->all()]);`

**Livrable :** Un dépôt GitHub contenant votre projet Laravel complet. Le `README.md` doit expliquer comment l'installer et le lancer.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez fait la transition de PHP procédural à un framework MVC moderne. Vous avez découvert une manière de travailler beaucoup plus structurée, sécurisée et productive. Vous maîtrisez les concepts de base du routage, des vues et des contrôleurs dans Laravel. La semaine prochaine, nous allons connecter notre application à une base de données SQL et découvrir la magie de l'ORM Eloquent.