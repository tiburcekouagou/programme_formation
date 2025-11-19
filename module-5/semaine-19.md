## Semaine 19 : Bases de Données avec Eloquent ORM

### J1 : Versionner sa Base de Données - Les Migrations

**Objectif(s) du Jour :**
- Configurer la connexion à la base de données dans le fichier `.env`.
- Comprendre le concept de "migration" comme un système de contrôle de version pour la base de données.
- Utiliser Artisan pour créer un fichier de migration.
- Définir la structure d'une table (colonnes, types de données) dans un fichier de migration.
- Exécuter et annuler des migrations.

**Notion Clé : Le Plan d'Architecte Évolutif**
Imaginez que vous construisiez un immeuble (votre base de données). Vous pourriez construire les fondations et les étages à la main, sans plan. Mais si vous travaillez en équipe, ou si vous devez modifier une partie de la structure plus tard, c'est le chaos.
Les **migrations** sont les **plans d'architecte** de votre base de données, versionnés dans le temps.
- **`php artisan make:migration` :** C'est comme dire "Je vais dessiner le plan pour le nouvel étage 'articles'".
- **Le fichier de migration :** C'est le plan détaillé. Il décrit précisément chaque poutre, chaque mur (chaque colonne de la table, son type, ses contraintes...).
- **`php artisan migrate` :** C'est l'ordre donné aux ouvriers de construire l'immeuble en suivant tous les plans dans l'ordre.
- **`php artisan migrate:rollback` :** C'est l'ordre de démolir le dernier étage construit, en suivant le plan à l'envers.
C'est un système propre, reproductible et qui permet à toute une équipe de travailler sur la même structure de base de données.

---

#### Leçon

##### 1. Configuration de la Base de Données

Laragon crée automatiquement une base de données pour chaque projet. Pour un projet nommé `forum-laravel`, la base de données s'appellera `forum-laravel`.
- Ouvrez le fichier `.env` de votre projet.
- Modifiez les lignes `DB_*` pour qu'elles correspondent à votre configuration Laragon :
  ```env
  DB_CONNECTION=mysql
  DB_HOST=127.0.0.1
  DB_PORT=3306
  DB_DATABASE=forum-laravel  // Le nom de votre projet
  DB_USERNAME=root
  DB_PASSWORD=             // Laissez vide par défaut avec Laragon
  ```

##### 2. Créer une Migration

Artisan est notre ami.
`php artisan make:migration create_posts_table`
Cette commande crée un nouveau fichier dans `database/migrations/`.

##### 3. Définir la Structure de la Table

Le fichier de migration contient une méthode `up()` (pour construire) et `down()` (pour démolir).

- **Exemple de Code (migration pour une table `posts`) :**
  ```php
  // database/migrations/xxxx_xx_xx_xxxxxx_create_posts_table.php
  use Illuminate\Database\Migrations\Migration;
  use Illuminate\Database\Schema\Blueprint;
  use Illuminate\Support\Facades\Schema;

  return new class extends Migration
  {
      public function up(): void
      {
          Schema::create('posts', function (Blueprint $table) {
              $table->id(); // Raccourci pour un auto-increment BigInt 'id'
              $table->string('title'); // Crée une colonne VARCHAR
              $table->text('content'); // Crée une colonne TEXT
              $table->timestamps(); // Crée les colonnes `created_at` et `updated_at`
          });
      }

      public function down(): void
      {
          Schema::dropIfExists('posts');
      }
  };
  ```

##### 4. Exécuter les Migrations

- `php artisan migrate` : Exécute toutes les migrations qui n'ont pas encore été jouées.
- `php artisan migrate:rollback` : Annule le dernier lot de migrations.
- `php artisan migrate:fresh` : Supprime toutes les tables et rejoue toutes les migrations. Très utile en développement !

---

#### Mise en Pratique

1.  Créez un nouveau projet Laravel `forum-laravel` avec Laragon.
2.  Configurez votre fichier `.env` pour la base de données.
3.  Lancez `php artisan make:migration create_threads_table` pour créer la table des sujets de forum.
4.  Modifiez le fichier de migration pour y ajouter une colonne `title` (string) et une colonne `body` (text).
5.  Lancez `php artisan migrate`.
6.  Utilisez le bouton "Database" de Laragon pour ouvrir un client SQL (HeidiSQL) et vérifiez que votre table `threads` a bien été créée avec les bonnes colonnes.

#### Mini-Exercice du Jour

Créez une autre migration pour une table `replies` (réponses). Elle devra contenir une colonne `body` (text) et une colonne `thread_id` (unsigned Big Integer, qui servira de clé étrangère plus tard). Lancez `php artisan migrate` à nouveau.

#### Synthèse

Vous avez appris à gérer la structure de votre base de données de manière professionnelle. Fini les modifications manuelles dans phpMyAdmin ! Vous pouvez maintenant construire, détruire et reconstruire votre base de données avec de simples commandes. Demain, nous allons voir comment interagir avec ces tables de manière élégante grâce aux modèles Eloquent.

---

### J2 : Parler à la Base de Données - Les Modèles Eloquent

**Objectif(s) du Jour :**
- Comprendre le concept d'ORM (Object-Relational Mapping) et le rôle d'Eloquent.
- Créer un modèle Eloquent avec Artisan.
- Utiliser les méthodes statiques de base d'Eloquent (`all`, `find`, `create`) pour le CRUD.
- Découvrir Tinker, la console interactive de Laravel, pour tester ses modèles.

**Notion Clé : L'Ambassadeur de la Table**
Écrire des requêtes SQL à la main (`SELECT * FROM posts WHERE ...`), c'est comme essayer de négocier avec un pays étranger dans sa langue natale. C'est possible, mais c'est complexe, sujet à erreurs, et vous devez apprendre chaque dialecte (MySQL, PostgreSQL...).
**Eloquent** est l'**ambassadeur** de votre table. C'est un objet PHP qui parle couramment le langage de votre base de données.
- Au lieu de `SELECT * FROM posts`, vous dites à votre ambassadeur `Post::all()`.
- Au lieu de `INSERT INTO posts (...)`, vous dites `Post::create([...])`.
- L'ambassadeur (`le Modèle`) sait à quelle table il est associé (la classe `Post` est associée à la table `posts`) et traduit vos ordres simples en requêtes SQL complexes et sécurisées. Vous interagissez avec des objets PHP, et Eloquent s'occupe du reste.

---

#### Leçon

##### 1. Créer un Modèle

`php artisan make:model Thread`
Cette commande crée un fichier `Thread.php` dans `app/Models/`. Par convention, un modèle nommé `Thread` au singulier sera automatiquement lié à une table `threads` au pluriel.

##### 2. Les Opérations CRUD de Base

- **READ (Lire) :**
  - `Thread::all()` : Récupère tous les enregistrements.
  - `Thread::find(1)` : Récupère l'enregistrement avec l'ID 1.
  - `Thread::where('title', 'Mon titre')->get()` : Recherche plus complexe.
- **CREATE (Créer) :**
  - Il faut d'abord définir les champs "remplissables" dans le modèle pour la sécurité.
    ```php
    // app/Models/Thread.php
    protected $fillable = ['title', 'body'];
    ```
  - `Thread::create(['title' => 'Nouveau sujet', 'body' => 'Contenu...']);`
- **UPDATE (Mettre à jour) :**
  - `$thread = Thread::find(1);`
  - `$thread->title = 'Nouveau titre';`
  - `$thread->save();`
- **DELETE (Supprimer) :**
  - `$thread = Thread::find(1);`
  - `$thread->delete();`
  - Ou `Thread::destroy(1);`

##### 3. Tinker : la Console Magique

`php artisan tinker`
Ouvre une console interactive où vous pouvez exécuter du code PHP et interagir directement avec vos modèles Eloquent. C'est l'outil parfait pour tester et manipuler vos données rapidement.

---

#### Mise en Pratique

1.  Dans votre projet `forum-laravel`, créez les modèles `Thread` et `Reply` avec Artisan.
2.  Ajoutez la propriété `$fillable` dans chaque modèle pour les champs que vous avez définis dans vos migrations.
3.  Lancez `php artisan tinker`.
4.  Dans Tinker, exécutez `use App\Models\Thread;`
5.  Créez un nouveau sujet : `Thread::create(['title' => 'Premier sujet !', 'body' => 'Ceci est mon premier sujet avec Eloquent.']);`
6.  Récupérez tous les sujets : `Thread::all();`. Vous devriez voir celui que vous venez de créer.

#### Mini-Exercice du Jour

Toujours dans Tinker, créez une réponse (un `Reply`) qui appartiendrait au premier sujet. Pour l'instant, mettez manuellement `thread_id` à 1. Ensuite, essayez de trouver ce `Reply` avec `Reply::find(1);`.

#### Synthèse

Vous ne parlez plus SQL, vous parlez Eloquent. Vous avez appris à manipuler les données de vos tables en utilisant des objets PHP simples et élégants. Mais comment lier une réponse à son sujet ? C'est le pouvoir des relations, que nous verrons demain.

---

### J3 : Créer des Liens - Les Relations Eloquent

**Objectif(s) du Jour :**
- Comprendre les types de relations principaux (One-to-One, One-to-Many, Many-to-Many).
- Définir une relation `One-to-Many` (un sujet a plusieurs réponses).
- Définir la relation inverse `BelongsTo` (une réponse appartient à un sujet).
- Utiliser ces relations pour récupérer facilement les données liées.

**Notion Clé : L'Arbre Généalogique**
Vos tables de base de données sont comme des personnes. Les **relations** Eloquent permettent de définir leur arbre généalogique.
- **Un Sujet (`Thread`) peut avoir plusieurs Réponses (`Reply`) :** C'est une relation `One-to-Many`. Le sujet est le "parent", les réponses sont les "enfants". Dans le modèle `Thread`, on définit une méthode `replies()` qui dit "Je veux la liste de tous mes enfants".
- **Une Réponse (`Reply`) appartient à un seul Sujet (`Thread`) :** C'est la relation inverse, `BelongsTo`. La réponse est "l'enfant", le sujet est le "parent". Dans le modèle `Reply`, on définit une méthode `thread()` qui dit "Je veux savoir qui est mon parent".
Grâce à ces définitions, vous pouvez faire des choses magiques comme `$thread->replies` pour obtenir toutes les réponses d'un sujet, sans écrire de `JOIN` SQL complexe.

---

#### Leçon

##### 1. La Relation `hasMany` (Un-à-Plusieurs)

Dans le modèle "parent".
```php
// app/Models/Thread.php
public function replies()
{
    // Ce sujet "a plusieurs" réponses
    return $this->hasMany(Reply::class);
}
```

##### 2. La Relation `belongsTo` (Appartient à)

Dans le modèle "enfant".
```php
// app/Models/Reply.php
public function thread()
{
    // Cette réponse "appartient à" un sujet
    return $this->belongsTo(Thread::class);
}
```

##### 3. Utiliser les Relations

Eloquent vous permet d'accéder aux relations comme si elles étaient des propriétés du modèle.

```php
// Dans Tinker ou un contrôleur

// Récupérer un sujet et toutes ses réponses
$thread = Thread::find(1);
foreach ($thread->replies as $reply) {
    echo $reply->body;
}

// Récupérer une réponse et le titre de son sujet parent
$reply = Reply::find(1);
echo $reply->thread->title;
```
Pour que cela fonctionne, la table `replies` doit avoir une colonne `thread_id` (convention de nommage : `nomdumodeleparent_id`).

---

#### Mise en Pratique

1.  Assurez-vous que votre migration pour la table `replies` contient bien la colonne `thread_id`. Si ce n'est pas le cas, faites un `migrate:fresh` et recréez vos données. Une meilleure méthode serait de créer une nouvelle migration pour ajouter la colonne.
2.  Ouvrez vos modèles `Thread.php` et `Reply.php`.
3.  Définissez les relations `replies()` et `thread()` comme dans les exemples.
4.  Lancez `php artisan tinker`.
5.  Créez un sujet, puis créez deux réponses en leur assignant l'ID du sujet.
6.  Récupérez le sujet avec `Thread::find(1)` et essayez d'accéder à `$thread->replies`. Vous devriez voir une collection contenant vos deux réponses.

#### Mini-Exercice du Jour

Laravel inclut une table `users` par défaut. Définissez les relations pour qu'un utilisateur puisse avoir plusieurs sujets (`hasMany` dans `User.php`) et qu'un sujet appartienne à un utilisateur (`belongsTo` dans `Thread.php`). N'oubliez pas d'ajouter la colonne `user_id` à votre table `threads` via une nouvelle migration.

#### Synthèse

Vous avez débloqué la fonctionnalité la plus puissante d'Eloquent. Vous pouvez maintenant naviguer dans vos données de manière intuitive et naturelle, en pensant en termes d'objets et de relations plutôt qu'en termes de tables et de jointures SQL. Il est temps de mettre tout cela en pratique dans notre application.

---

### J4 : Le CRUD avec Contrôleurs et Vues

**Objectif(s) du Jour :**
- Créer un contrôleur ressource pour les sujets du forum.
- Implémenter la méthode `index()` pour afficher la liste de tous les sujets.
- Implémenter la méthode `show()` pour afficher un sujet et ses réponses.
- Créer les vues Blade correspondantes.

**Notion Clé : L'Exposition au Public**
Vous avez passé les derniers jours à organiser votre collection de livres et leur généalogie en coulisses (migrations, modèles, relations). Aujourd'hui, vous ouvrez les portes de la bibliothèque au public.
- La **route** est l'adresse de la salle d'exposition.
- Le **contrôleur** est le guide. Quand un visiteur demande à voir la salle "tous les sujets" (`/threads`), le guide (`ThreadController@index`) va chercher tous les livres (`Thread::all()`) et les dispose sur des étagères (`return view('threads.index', ...)`).
- Quand un visiteur veut voir un livre en particulier (`/threads/1`), le guide (`ThreadController@show`) va chercher ce livre et tous ses commentaires (`Thread::find(1)` et `$thread->replies`) et les présente sur un pupitre dédié (`return view('threads.show', ...)`).

---

#### Leçon

##### 1. Route Ressource

Dans `routes/web.php`, une seule ligne peut créer les 7 routes CRUD pour un contrôleur.
`Route::resource('threads', ThreadController::class);`

##### 2. Logique du Contrôleur

```php
// app/Http/Controllers/ThreadController.php
use App\Models\Thread;

class ThreadController extends Controller
{
    // Affiche la liste de toutes les ressources
    public function index()
    {
        $threads = Thread::latest()->get(); // Récupère tous les sujets, les plus récents d'abord
        return view('threads.index', ['threads' => $threads]);
    }

    // Affiche une ressource spécifique
    public function show(Thread $thread) // Laravel fait le find() pour nous, c'est le "Route Model Binding"
    {
        // On peut charger les réponses avec le sujet
        // $thread->load('replies'); // Optionnel, pour optimiser
        return view('threads.show', ['thread' => $thread]);
    }
}
```

##### 3. Vues Blade

```blade
// resources/views/threads/index.blade.php
@foreach ($threads as $thread)
    <h2><a href="/threads/{{ $thread->id }}">{{ $thread->title }}</a></h2>
@endforeach

// resources/views/threads/show.blade.php
<h1>{{ $thread->title }}</h1>
<p>{{ $thread->body }}</p>
<hr>
<h3>Réponses :</h3>
@foreach ($thread->replies as $reply)
    <p>{{ $reply->body }}</p>
@endforeach
```

---

#### Mise en Pratique

1.  Créez un `ThreadController` ressource avec Artisan.
2.  Ajoutez `Route::resource('threads', ThreadController::class);` dans votre fichier de routes.
3.  Implémentez les méthodes `index()` et `show()` dans votre contrôleur.
4.  Créez le dossier `threads` dans `resources/views` et les vues `index.blade.php` et `show.blade.php`.
5.  Utilisez Tinker pour créer quelques données de test.
6.  Naviguez sur `http://forum-laravel.test/threads` et cliquez sur un lien pour voir la page de détail.

#### Mini-Exercice du Jour

Dans la vue `show.blade.php`, affichez également le nom de l'auteur du sujet et l'auteur de chaque réponse (en supposant que vous avez fait l'exercice de la veille sur la relation avec les utilisateurs).

#### Synthèse

Vous avez connecté toutes les couches de l'architecture MVC pour lire des données et les afficher. Le flux `Route -> Controller -> Model -> View` est maintenant clair et concret. Demain, nous allons fermer la boucle en permettant à l'utilisateur de créer ses propres données.

---

### J5 : Projet de la Semaine - Backend de Forum Simple

**Objectif(s) du Jour :**
- Mettre en pratique toutes les notions de la semaine (migrations, modèles, relations, CRUD).
- Implémenter la logique de création d'un nouveau sujet (`create` et `store`).
- Développer un backend de forum simple mais complet.

**Notion Clé : Permettre aux Visiteurs d'Écrire leurs Propres Livres**
La bibliothèque est ouverte, les visiteurs peuvent lire les livres et leurs commentaires. La dernière étape est de mettre en place un bureau où un visiteur peut soumettre son propre manuscrit pour qu'il soit ajouté à la collection. Cela implique un formulaire (`create`), une validation et une logique de sauvegarde (`store`).

---

#### PROJET DE LA SEMAINE : Backend d'un Forum

Votre mission est de développer la logique backend complète pour un forum simple, en se concentrant sur la création et l'affichage des sujets et des réponses.

**Structure et Fonctionnalités Obligatoires :**

1.  **Migrations et Modèles :**
    - Un modèle `User` (fourni par défaut).
    - Un modèle `Thread` avec `title`, `body`, et une relation `belongsTo(User::class)`.
    - Un modèle `Reply` avec `body`, et des relations `belongsTo(User::class)` et `belongsTo(Thread::class)`.
    - Toutes les migrations nécessaires pour créer ces tables et leurs clés étrangères.

2.  **Seeding (Peuplement de la base) :**
    - (Bonus) Créez un "Seeder" (`php artisan make:seeder`) pour peupler votre base de données avec de faux utilisateurs, sujets et réponses. C'est plus propre que Tinker pour des données de test réutilisables.

3.  **Contrôleurs et Routes :**
    - Un `ThreadController` ressource (`Route::resource('threads', ...)`).
    - Implémentez les méthodes `index` et `show` pour l'affichage.
    - **`create()` :** Cette méthode doit simplement retourner la vue `threads.create` qui contient le formulaire pour créer un nouveau sujet.
    - **`store(Request $request)` :** Cette méthode, cible du formulaire, doit :
        - Valider la requête (au minimum, s'assurer que `title` et `body` sont présents).
        - Créer le nouveau sujet dans la base de données : `Thread::create([...])`.
        - Rediriger l'utilisateur vers la page du sujet nouvellement créé (`redirect()->route('threads.show', $newThread)`) ou vers la liste des sujets.

4.  **Vues Blade :**
    - Les vues `index` et `show` pour l'affichage.
    - Une vue `create.blade.php` contenant le formulaire de création de sujet (`<form method="POST" action="{{ route('threads.store') }}">`). N'oubliez pas `@csrf`.

**Livrable :** Un dépôt GitHub contenant votre projet de forum Laravel. Le `README.md` doit expliquer comment cloner le projet, installer les dépendances, configurer le `.env`, et lancer les migrations (`php artisan migrate --seed` si vous avez fait le seeder) pour que l'application soit fonctionnelle.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez maîtrisé Eloquent, l'un des ORM les plus puissants et élégants qui existent. Vous savez comment structurer une base de données avec des migrations, comment interagir avec elle de manière intuitive avec des modèles, et comment lier des données entre elles avec des relations. Vous avez construit un backend d'application web complet, dynamique et basé sur des données. La semaine prochaine, vous y ajouterez la couche finale de professionnalisme : l'authentification et les fonctionnalités avancées de Laravel.