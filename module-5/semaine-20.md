## Semaine 20 : Fonctionnalités Avancées de Laravel

### J1 : Authentification en 5 Minutes - Laravel Breeze

**Objectif(s) du Jour :**
- Comprendre ce qu'est un "starter kit" d'authentification.
- Installer et configurer Laravel Breeze.
- Découvrir l'ensemble des routes, contrôleurs et vues générés automatiquement pour l'inscription, la connexion, la réinitialisation de mot de passe, etc.
- Tester le flux d'authentification complet.

**Notion Clé : Le Kit de Sécurité Pré-assemblé**
La semaine dernière, avec Node.js, vous avez construit votre système de sécurité (authentification) pièce par pièce : le hachage des mots de passe, la création de tokens, le middleware de protection... C'était formateur, mais long.
**Laravel Breeze** est un **kit de sécurité complet et pré-assemblé**. C'est comme si, en achetant votre maison, le constructeur vous disait : "J'ai déjà installé pour vous une porte blindée, un système d'alarme, des serrures sur toutes les fenêtres, et un interphone". En une seule commande, Laravel va :
- Créer toutes les tables de base de données nécessaires.
- Créer toutes les routes (`/login`, `/register`, `/logout`...).
- Créer tous les contrôleurs qui gèrent la logique.
- Créer toutes les vues (les formulaires de connexion, d'inscription...).
Votre travail n'est plus de construire le système, mais de l'intégrer et de l'utiliser.

---

#### Leçon

##### 1. Qu'est-ce que Laravel Breeze ?

Breeze est le "starter kit" d'authentification le plus simple de Laravel. Il fournit une implémentation minimale et élégante de toutes les fonctionnalités d'authentification, basée sur des vues Blade et le framework CSS Tailwind.

##### 2. Installation de Breeze

L'installation se fait en quelques commandes Artisan, après avoir créé un projet Laravel frais.
1.  `composer require laravel/breeze --dev`
2.  `php artisan breeze:install`
    - L'assistant vous demandera quel "stack" vous préférez. Choisissez `Blade` (ou `0`).
    - Il vous demandera si vous voulez le mode sombre, le support de TypeScript... Dites "no" pour rester simple pour l'instant.
3.  `php artisan migrate` (Breeze ajoute ses propres migrations pour les utilisateurs).
4.  `npm install && npm run dev` (Breeze utilise Vite pour compiler les assets CSS/JS).

##### 3. Qu'est-ce qui a été créé ?

- **Routes :** Un nouveau fichier `routes/auth.php` contient toutes les routes d'authentification.
- **Vues :** Un dossier `resources/views/auth/` contient les formulaires. Un dossier `resources/views/layouts/` contient de nouveaux layouts.
- **Contrôleurs :** Un dossier `app/Http/Controllers/Auth/` contient toute la logique.
- **Barre de navigation :** Le layout principal a maintenant des liens "Login" et "Register", qui se transforment en menu déroulant avec le nom de l'utilisateur et un lien "Logout" une fois connecté.

---

#### Mise en Pratique

1.  Créez un nouveau projet Laravel `forum-auth` avec Laragon.
2.  Configurez votre fichier `.env` pour la base de données.
3.  Suivez les 4 étapes d'installation de Breeze. Laissez la commande `npm run dev` tourner dans un terminal.
4.  Ouvrez `http://forum-auth.test` dans votre navigateur. Vous devriez voir la page d'accueil de Laravel avec les liens "Log in" et "Register" en haut à droite.
5.  Cliquez sur "Register", créez un compte. Vous serez automatiquement connecté et redirigé vers une page `/dashboard`.
6.  Cliquez sur votre nom, puis sur "Log Out". Testez la page de connexion.

#### Mini-Exercice du Jour

Explorez les fichiers créés par Breeze. Ouvrez `routes/auth.php` et `app/Http/Controllers/Auth/AuthenticatedSessionController.php` pour voir comment Laravel structure la logique que vous avez dû écrire à la main en Node.js.

#### Synthèse

En quelques minutes, vous avez mis en place un système d'authentification complet, sécurisé et de qualité production. C'est un exemple frappant de la puissance et de la productivité d'un framework "batteries included" comme Laravel. Demain, nous verrons comment protéger nos propres routes avec les middlewares fournis.

---

### J2 : Protéger les Zones - Les Middlewares d'Authentification

**Objectif(s) du Jour :**
- Comprendre le rôle des middlewares dans Laravel.
- Utiliser le middleware `auth` pour protéger des routes.
- Appliquer un middleware à une route unique ou à un groupe de routes.
- Accéder aux informations de l'utilisateur authentifié.

**Notion Clé : Le Badge d'Accès de l'Employé**
Le concept est exactement le même qu'avec Express.js, mais la syntaxe de Laravel est encore plus élégante. Le système d'authentification de Breeze a déjà configuré un gardien (`le middleware 'auth'`).
Votre travail est simplement de placer ce gardien devant les portes des bureaux que vous voulez protéger.
- **Protéger un bureau :** Vous ajoutez `->middleware('auth')` à la fin de la définition de votre route. C'est comme mettre un panneau "Accès réservé aux employés" sur une porte.
- **Protéger tout un étage :** Vous créez un `Route::group()` et vous y appliquez le middleware. C'est comme mettre un seul gardien à l'entrée de l'étage plutôt qu'un devant chaque porte.
Si un visiteur sans badge (un utilisateur non connecté) essaie d'entrer, le gardien le redirige automatiquement vers le bureau d'accueil (la page de connexion).

---

#### Leçon

##### 1. Le Middleware `auth`

C'est le middleware fourni par défaut par Laravel pour vérifier si un utilisateur est connecté.

##### 2. Appliquer un Middleware

- **Sur une route unique :**
  ```php
  Route::get('/profil', [ProfileController::class, 'show'])->middleware('auth');
  ```
- **Sur un groupe de routes (méthode recommandée) :**
  ```php
  Route::middleware('auth')->group(function () {
      Route::get('/dashboard', ...);
      Route::resource('/threads', ThreadController::class)->except(['index', 'show']);
  });
  ```
  L'exemple ci-dessus protège toutes les routes de `ThreadController` sauf `index` et `show`.

##### 3. Accéder à l'Utilisateur Connecté

Partout dans votre application (contrôleurs, vues...), vous pouvez accéder à l'objet de l'utilisateur connecté de plusieurs manières :
- `auth()->user()`
- `request()->user()`
- Dans une vue Blade : `@auth ... @endauth` pour afficher du contenu conditionnel.

---

#### Mise en Pratique

1.  Reprenez votre projet `forum-auth`.
2.  Ajoutez un `ThreadController` et les routes ressources (`Route::resource('threads', ...)`).
3.  Protégez les routes de création, modification et suppression de sujets. Un utilisateur non connecté doit pouvoir voir la liste des sujets et un sujet en particulier, mais pas les créer.
    ```php
    Route::resource('threads', ThreadController::class)->only(['index', 'show']);
    Route::resource('threads', ThreadController::class)->except(['index', 'show'])->middleware('auth');
    ```
4.  Essayez d'accéder à `http://forum-auth.test/threads/create` sans être connecté. Vous devriez être redirigé vers la page de connexion.
5.  Connectez-vous et réessayez. Vous devriez maintenant y avoir accès.

#### Mini-Exercice du Jour

Dans le layout de votre application, utilisez les directives `@auth` et `@guest` de Blade pour afficher le lien "Créer un sujet" uniquement si l'utilisateur est connecté (`@auth`), et les liens "Login" / "Register" uniquement s'il est un invité (`@guest`).

#### Synthèse

Vous savez maintenant sécuriser votre application en séparant les zones publiques des zones privées. La gestion des middlewares est un concept central de Laravel pour construire des applications robustes. Demain, nous allons nous pencher sur la validation des données envoyées par l'utilisateur.

---

### J3 : Valider les Formulaires Comme un Pro

**Objectif(s) du Jour :**
- Utiliser le système de validation intégré de Laravel.
- Définir des règles de validation simples (`required`, `min`, `max`, `email`...).
- Afficher les messages d'erreur de validation dans les vues Blade.
- Comprendre comment Laravel gère la redirection et la persistance des anciennes données (`old()`).

**Notion Clé : Le Formulaire Intelligent**
Oubliez la validation manuelle avec des `if`. Le validateur de Laravel est un **formulaire intelligent**.
1.  **Les Règles :** Dans votre contrôleur, vous donnez une liste de règles au formulaire : "Le champ `title` est requis et doit faire au moins 3 caractères. Le champ `body` est requis."
2.  **La Soumission :** Quand l'utilisateur soumet le formulaire, Laravel vérifie automatiquement chaque champ par rapport à ses règles.
3.  **L'Échec :** Si une règle n'est pas respectée, Laravel fait plusieurs choses magiques, **automatiquement** :
    - Il arrête l'exécution du code.
    - Il redirige l'utilisateur vers la page du formulaire.
    - Il met les messages d'erreur dans une variable spéciale (`$errors`).
    - Il remet les anciennes valeurs que l'utilisateur avait tapées dans les champs (`old('title')`).
4.  **Le Succès :** Si toutes les règles sont respectées, l'exécution du code continue normalement.

---

#### Leçon

##### 1. La Méthode `validate`

Dans votre contrôleur, la méthode `validate()` de l'objet `Request` est le moyen le plus simple.
```php
// ThreadController@store
public function store(Request $request)
{
    // Si la validation échoue, Laravel s'occupe de tout.
    $validatedData = $request->validate([
        'title' => 'required|max:255|min:3',
        'body' => ['required', 'min:10'], // Syntaxe alternative
    ]);

    // Si on arrive ici, c'est que la validation a réussi.
    // On peut utiliser $validatedData pour créer le sujet.
    //...
}
```

##### 2. Afficher les Erreurs dans Blade

Laravel fournit une variable `$errors` à toutes les vues.
```blade
// resources/views/threads/create.blade.php
<form ...>
    @csrf
    <div>
        <label for="title">Titre</label>
        <input type="text" name="title" value="{{ old('title') }}">
        @error('title')
            <div class="alert alert-danger">{{ $message }}</div>
        @enderror
    </div>
    ...
</form>
```
- `old('title')` : Réaffiche l'ancienne valeur du champ `title` en cas d'erreur.
- `@error('title') ... @enderror` : Bloc qui ne s'affiche que s'il y a une erreur pour le champ `title`.
- `$message` : Variable magique contenant le message d'erreur.

---

#### Mise en Pratique

1.  Implémentez les méthodes `create` (pour afficher la vue) et `store` (pour traiter les données) dans votre `ThreadController`.
2.  Dans la méthode `store`, ajoutez la validation pour les champs `title` et `body`.
3.  Créez la vue `create.blade.php` avec un formulaire.
4.  Dans cette vue, ajoutez l'affichage des erreurs de validation et la fonction `old()` pour chaque champ.
5.  Testez votre formulaire : essayez de le soumettre vide, avec un titre trop court, etc. Observez le comportement magique de Laravel.

#### Mini-Exercice du Jour

Créez une "Form Request" avec `php artisan make:request StoreThreadRequest`. Déplacez vos règles de validation du contrôleur vers le fichier `StoreThreadRequest`. Ensuite, dans votre contrôler, remplacez `Request $request` par `StoreThreadRequest $request`. C'est la manière la plus propre et réutilisable de gérer la validation pour des applications complexes.

#### Synthèse

Vous maîtrisez maintenant l'un des aspects les plus appréciés de Laravel : un système de validation puissant, élégant et qui vous fait gagner un temps fou. Vos formulaires sont maintenant robustes et l'expérience utilisateur est grandement améliorée. Il est temps de voir comment Laravel peut aussi servir une API.

---

### J4 : Laravel en Mode API - API Routes

**Objectif(s) du Jour :**
- Comprendre la différence entre `routes/web.php` et `routes/api.php`.
- Créer ses premières routes d'API.
- Utiliser Postman/Thunder Client pour tester les endpoints de l'API.
- Comprendre que les API routes de Laravel sont "stateless" par défaut.

**Notion Clé : L'Entrée de Service**
Votre application Laravel a deux portes d'entrée :
- **`routes/web.php` :** C'est l'**entrée principale** du bâtiment, pour les visiteurs humains. Elle est équipée de tout le confort : gestion des sessions, protection CSRF, cookies... C'est pour les applications web traditionnelles.
- **`routes/api.php` :** C'est l'**entrée de service** à l'arrière, pour les livraisons et les robots (applications frontend, mobiles...). Elle est beaucoup plus directe et dépouillée. Par défaut, il n'y a pas de sessions, pas de cookies. Chaque requête est indépendante ("stateless"). Pour se faire identifier, le livreur doit présenter un badge (un token d'API) à chaque passage.

---

#### Leçon

##### 1. Le Fichier `routes/api.php`

- Les routes définies ici sont automatiquement préfixées par `/api`. Donc, `Route::get('/threads', ...)` sera accessible via `http://mon-site.test/api/threads`.
- Ces routes n'utilisent pas le middleware de session, ce qui les rend plus rapides et "stateless".

##### 2. Créer une API Ressource

De la même manière que pour les routes web, on peut utiliser des contrôleurs.
```php
// Crée un contrôleur spécifique pour l'API
// php artisan make:controller Api/V1/ThreadController --api
// L'option --api génère un contrôleur sans les méthodes create et edit, inutiles pour une API.

// routes/api.php
use App\Http\Controllers\Api\V1\ThreadController;

Route::apiResource('threads', ThreadController::class);
```
`apiResource` est l'équivalent de `resource` mais pour les API (il omet les routes `create` et `edit`).

##### 3. Retourner du JSON

Dans un contrôleur d'API, on ne retourne pas de vues. Laravel convertit automatiquement les tableaux et les modèles Eloquent en JSON.

```php
// app/Http/Controllers/Api/V1/ThreadController.php
public function index()
{
    return Thread::all(); // Laravel transforme ça en JSON automatiquement
}
```

---

#### Mise en Pratique

1.  Créez un `Api/V1/ThreadController` avec l'option `--api`.
2.  Dans `routes/api.php`, ajoutez une `Route::apiResource` pour vos sujets.
3.  Implémentez la méthode `index()` dans votre nouveau contrôleur pour qu'elle retourne `Thread::all()`.
4.  Avec Postman, faites une requête `GET` sur `http://forum-auth.test/api/threads`. Vous devriez recevoir la liste de vos sujets au format JSON.

#### Mini-Exercice du Jour

Implémentez la méthode `show(Thread $thread)` dans votre contrôleur d'API. Testez l'endpoint `GET /api/threads/{id}`.

#### Synthèse

Votre application Laravel est maintenant hybride : elle peut servir une application web traditionnelle avec des vues Blade ET exposer une API JSON pour des clients externes. Demain, nous allons combiner tout cela pour le projet final du module.

---

### J5 : Projet de la Semaine - Finaliser le Forum et Exposer une API

**Objectif(s) du Jour :**
- Intégrer l'authentification Breeze dans l'application de forum.
- Protéger les actions de création/modification de sujets.
- Implémenter une API RESTful de base pour les sujets du forum.
- Avoir une application Laravel complète, sécurisée et hybride.

**Notion Clé : Le Bâtiment à Double Accès**
Votre projet final est un bâtiment moderne et complet.
- La **façade principale** (rendu côté serveur avec Blade) est accueillante pour les visiteurs humains. Ils peuvent s'inscrire, se connecter, naviguer, et interagir via des formulaires sécurisés. L'accès aux zones privées est gardé par le personnel de sécurité (`middleware auth`).
- L'**entrée de service** (`/api`) permet à des programmes externes (comme une future application mobile ou un frontend Vue.js) d'accéder aux données brutes (en JSON). Pour l'instant, cet accès est public, mais vous avez les connaissances (semaine 15) pour y ajouter une authentification par token (avec Laravel Sanctum ou Passport, par exemple) plus tard.

---

#### PROJET DE LA SEMAINE : Forum Complet avec API

Votre mission est de prendre le projet de forum de la semaine 19 et d'y intégrer les fonctionnalités avancées vues cette semaine.

**Structure et Fonctionnalités Obligatoires :**

1.  **Authentification :**
    - Intégrez Laravel Breeze à votre projet.
    - Le layout de votre application doit afficher les liens de navigation appropriés (`Login`/`Register` pour les invités, `Dashboard`/`Logout` pour les connectés).

2.  **Protection des Routes Web :**
    - Seuls les utilisateurs connectés doivent pouvoir accéder aux pages de création (`/threads/create`) et de soumission de formulaire (`POST /threads`).
    - Appliquez le middleware `auth` à ces routes.
    - Dans la méthode `store` du `ThreadController`, l'auteur du nouveau sujet doit être l'utilisateur actuellement authentifié (`auth()->id()`).

3.  **Validation :**
    - Mettez en place une validation robuste pour le formulaire de création de sujet en utilisant la méthode `validate()` de Laravel.

4.  **API Publique :**
    - Créez un dossier `Api/V1` dans vos contrôleurs.
    - Créez un `ThreadController` pour l'API (`--api`).
    - Dans `routes/api.php`, exposez les routes `index` et `show` pour les sujets.
    - Ces routes doivent renvoyer les données des sujets au format JSON.

**Livrable :** Un dépôt GitHub contenant votre projet de forum Laravel complet. Le `README.md` doit être mis à jour et doit inclure :
- Les instructions d'installation complètes (y compris `breeze:install` et `npm install`).
- Une description du fonctionnement de l'application.
- Une mini-documentation de l'API publique (`GET /api/threads` et `GET /api/threads/{id}`).

#### Synthèse Finale de la Semaine et du Module

**Immenses félicitations !** Vous avez non seulement appris un deuxième langage backend majeur, mais vous avez aussi maîtrisé les bases d'un des frameworks les plus puissants et les plus demandés sur le marché. Vous avez vu comment Laravel accélère le développement en fournissant des solutions élégantes à des problèmes complexes comme l'authentification, la validation et l'interaction avec la base de données. Vous êtes maintenant un développeur beaucoup plus polyvalent, capable de choisir le bon outil pour le bon travail, que ce soit dans l'écosystème JavaScript avec Node.js ou dans l'écosystème PHP avec Laravel. Le dernier module vous préparera à transformer ces compétences techniques en une carrière réussie.