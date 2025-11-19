# Module 5 : Le Cerveau de l'Application - Le Backend avec Node.js & Express

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Comprendre le rôle d'un serveur backend et d'une API RESTful.
- Écrire du JavaScript côté serveur avec l'environnement d'exécution Node.js.
- Créer un serveur web et définir des routes avec le framework Express.js.
- Concevoir et implémenter des opérations CRUD (Create, Read, Update, Delete).
- Modéliser des données et interagir avec une base de données NoSQL (MongoDB) grâce à un ODM (Mongoose).
- Mettre en place un système d'authentification utilisateur complet avec des mots de passe hachés et des JSON Web Tokens (JWT).
- Sécuriser une API en protégeant des routes et en gérant des variables d'environnement.

## 2. Prérequis

- Avoir complété les modules précédents, en particulier une **solide maîtrise de JavaScript (Module 3)**.
- Avoir **Node.js et NPM** installés sur votre machine.
- Avoir installé un client API comme **Postman** ou **Insomnia**. Cet outil est indispensable pour tester votre backend sans avoir besoin d'un frontend.

## 3. Résumé du Concept (Qu'est-ce qu'un Backend ?)

Jusqu'à présent, tout votre code s'exécutait dans le navigateur du client. Le backend, c'est l'envers du décor. C'est un programme qui tourne sur un serveur distant, une machine toujours allumée et accessible via internet. Son rôle n'est pas d'afficher des jolis boutons, mais de gérer la **logique métier** et les **données**.

Imaginez un restaurant. Le frontend (Vue.js) est la salle : le menu, les tables, la décoration. C'est ce que le client voit. Le backend (Node.js) est la cuisine : c'est là que les commandes sont reçues, que les plats sont préparés (la logique), que les ingrédients sont stockés et récupérés (la base de données).

Le frontend et le backend communiquent via un "pass" : c'est l'**API** (Application Programming Interface). Le frontend envoie des requêtes (ex: "Donne-moi la liste des plats") et le backend renvoie des réponses, généralement sous forme de données brutes (JSON). Votre mission est de construire cette cuisine et de définir les règles de communication.

## 4. Plan d’Apprentissage

*   **Chapitre 1 : Introduction à Node.js et Express**
    *   JavaScript en dehors du navigateur
    *   Initialiser un projet NPM
    *   Créer un premier serveur avec Express.js
*   **Chapitre 2 : Routage et Structure MVC**
    *   Les verbes HTTP (GET, POST, PUT, DELETE)
    *   Organiser son code : le pattern Modèle-Vue-Contrôleur (adapté pour une API)
*   **Chapitre 3 : Persistance des Données avec MongoDB et Mongoose**
    *   Pourquoi une base de données ?
    *   Créer un schéma de données avec Mongoose
    *   Se connecter à une base de données MongoDB (locale ou Atlas)
*   **Chapitre 4 : Implémenter le CRUD**
    *   Créer une ressource (POST)
    *   Lire des ressources (GET)
    *   Mettre à jour une ressource (PUT/PATCH)
    *   Supprimer une ressource (DELETE)
*   **Chapitre 5 : Authentification des Utilisateurs**
    *   Modèle Utilisateur et hachage de mot de passe (bcrypt)
    *   Créer les routes `register` et `login`
    *   Générer un JSON Web Token (JWT) à la connexion
*   **Chapitre 6 : Sécurisation et Middlewares**
    *   Les middlewares : le cœur d'Express
    *   Créer un middleware pour protéger des routes
    *   Gérer les variables d'environnement (`.env`)

## 5. Leçons

### Leçon 1 : Introduction à Node.js et Express

Node.js nous permet d'exécuter du JS sur un serveur. Express est un framework minimaliste qui nous simplifie énormément la création de serveurs web et d'API. On commence par le "Hello World" du backend.

- **Exemple de code simple (`index.js`) :**
  ```javascript
  // Importer le framework Express
  const express = require('express');
  
  // Créer une application Express
  const app = express();
  const port = 3000;

  // Définir une route pour la racine de l'URL
  app.get('/', (req, res) => {
    res.send('Hello, World!');
  });

  // Démarrer le serveur et écouter sur le port défini
  app.listen(port, () => {
    console.log(`Serveur démarré sur http://localhost:${port}`);
  });
  ```
- **Exemple de code appliqué (le squelette de notre future API de blog) :**
  *Après `npm init -y` et `npm install express`*
  ```javascript
  // index.js
  const express = require('express');
  const app = express();
  const PORT = process.env.PORT || 5000;

  // Middleware pour permettre à Express de lire le JSON dans les corps de requête
  app.use(express.json());

  app.get('/api/posts', (req, res) => {
    // Pour l'instant, on renvoie des données statiques
    res.json([{ title: 'Mon premier article', content: '...' }]);
  });

  app.listen(PORT, () => console.log(`Serveur démarré sur le port ${PORT}`));
  ```

### Leçon 2 : Routage et Structure MVC

Pour une API propre, on ne met pas toute la logique dans `index.js`. On sépare les routes (les URL) des contrôleurs (la logique à exécuter). C'est une adaptation du pattern MVC.

- **Exemple de code simple :**
  *Fichier `routes/users.js`*
  ```javascript
  const express = require('express');
  const router = express.Router();
  
  router.get('/', (req, res) => res.send('Liste des utilisateurs'));
  router.get('/:id', (req, res) => res.send(`Détail de l'utilisateur ${req.params.id}`));
  
  module.exports = router;
  ```
  *Fichier `index.js`*
  ```javascript
  // ...
  const userRoutes = require('./routes/users');
  app.use('/api/users', userRoutes); // Toutes les routes dans users.js seront préfixées par /api/users
  // ...
  ```
- **Exemple de code appliqué (structure pour les articles de blog) :**
  *Fichier `controllers/postController.js`*
  ```javascript
  // Logique pour récupérer tous les articles
  exports.getAllPosts = (req, res) => {
    // La logique de base de données viendra ici plus tard
    res.status(200).json({ message: 'Logique pour récupérer tous les articles' });
  };
  ```
  *Fichier `routes/posts.js`*
  ```javascript
  const express = require('express');
  const router = express.Router();
  const postController = require('../controllers/postController');

  router.get('/', postController.getAllPosts);
  
  module.exports = router;
  ```

### Leçon 3 : Persistance des Données avec MongoDB et Mongoose

Nos données disparaissent à chaque redémarrage du serveur. Il nous faut une base de données. Mongoose est un "Object Data Modeler" qui nous permet de définir la structure de nos données (un "schéma") et de communiquer très facilement avec MongoDB.

- **Exemple de code simple (définir un modèle) :**
  *Fichier `models/User.js`*
  ```javascript
  const mongoose = require('mongoose');

  const userSchema = new mongoose.Schema({
    name: String,
    email: { type: String, required: true, unique: true },
    createdAt: { type: Date, default: Date.now }
  });

  module.exports = mongoose.model('User', userSchema);
  ```
- **Exemple de code appliqué (le modèle pour nos articles de blog) :**
  *Fichier `models/Post.js`*
  ```javascript
  const mongoose = require('mongoose');

  const postSchema = new mongoose.Schema({
    title: { type: String, required: true },
    content: { type: String, required: true },
    author: { type: String, default: 'Anonyme' },
  });

  module.exports = mongoose.model('Post', postSchema);
  ```
  *Dans `index.js`, on ajoute la connexion à la BDD :*
  ```javascript
  mongoose.connect('mongodb://localhost:27017/mon_blog')
    .then(() => console.log('Connecté à MongoDB'))
    .catch(err => console.error('Erreur de connexion', err));
  ```

### Leçon 4 : Implémenter le CRUD

CRUD est l'acronyme pour les 4 opérations de base sur les données. C'est le cœur de la plupart des API. On va lier chaque opération à un verbe HTTP et à une route.

- **Exemple de code simple (dans `postController.js`) :**
  ```javascript
  const Post = require('../models/Post');

  // CREATE
  exports.createPost = async (req, res) => {
    const post = new Post({ title: req.body.title, content: req.body.content });
    await post.save();
    res.status(201).json(post);
  };

  // READ
  exports.getAllPosts = async (req, res) => {
    const posts = await Post.find();
    res.status(200).json(posts);
  };
  
  // UPDATE
  exports.updatePost = async (req, res) => { /* ... */ };
  
  // DELETE
  exports.deletePost = async (req, res) => { /* ... */ };
  ```
- **Exemple de code appliqué (routes correspondantes dans `routes/posts.js`) :**
  ```javascript
  router.post('/', postController.createPost); // POST /api/posts
  router.get('/', postController.getAllPosts); // GET /api/posts
  // router.put('/:id', postController.updatePost);
  // router.delete('/:id', postController.deletePost);
  ```

### Leçon 5 : Authentification des Utilisateurs

On ne peut pas laisser n'importe qui créer ou supprimer des articles. Il faut un système d'utilisateurs. On ne stocke **jamais** les mots de passe en clair, on les "hache". À la connexion, on donne à l'utilisateur un "jeton" (JWT) qu'il devra présenter pour accéder aux routes protégées.

- **Exemple de code simple (route de connexion) :**
  ```javascript
  // Dans un userController.js
  const User = require('../models/User');
  const bcrypt = require('bcryptjs');
  const jwt = require('jsonwebtoken');

  exports.login = async (req, res) => {
    const user = await User.findOne({ email: req.body.email });
    if (!user) return res.status(404).send('Utilisateur non trouvé.');

    const validPassword = await bcrypt.compare(req.body.password, user.password);
    if (!validPassword) return res.status(400).send('Mot de passe invalide.');
    
    // Créer et assigner un token
    const token = jwt.sign({ _id: user._id }, 'VOTRE_SECRET_JWT');
    res.header('auth-token', token).send(token);
  };
  ```
- **Exemple de code appliqué (route d'enregistrement avec hachage) :**
  ```javascript
  // Dans un userController.js
  exports.register = async (req, res) => {
    // Hacher le mot de passe
    const salt = await bcrypt.genSalt(10);
    const hashedPassword = await bcrypt.hash(req.body.password, salt);

    const user = new User({ name: req.body.name, email: req.body.email, password: hashedPassword });
    await user.save();
    res.status(201).send({ user: user._id });
  };
  ```

### Leçon 6 : Sécurisation et Middlewares

Un middleware est une fonction qui s'exécute entre la requête et la réponse. C'est parfait pour vérifier si un utilisateur est authentifié avant de le laisser accéder à une ressource. On externalise aussi les données sensibles (clés secrètes, URL de BDD) dans un fichier `.env`.

- **Exemple de code simple (middleware de vérification de token) :**
  *Fichier `middleware/auth.js`*
  ```javascript
  const jwt = require('jsonwebtoken');

  module.exports = function(req, res, next) {
    const token = req.header('auth-token');
    if (!token) return res.status(401).send('Accès refusé.');
    
    try {
      const verified = jwt.verify(token, 'VOTRE_SECRET_JWT');
      req.user = verified;
      next(); // Passe à la prochaine fonction (le contrôleur)
    } catch (err) {
      res.status(400).send('Token invalide.');
    }
  }
  ```
- **Exemple de code appliqué (protéger la création d'article) :**
  *Fichier `routes/posts.js`*
  ```javascript
  const authMiddleware = require('../middleware/auth');
  
  // Seuls les utilisateurs authentifiés peuvent créer un article
  router.post('/', authMiddleware, postController.createPost); 
  router.get('/', postController.getAllPosts); // Tout le monde peut voir les articles
  ```

## 6. Exercices Pratiques

- **Niveau Débutant : API "Citations"**
  Créez une API avec une seule route `GET /api/quote` qui renvoie une citation aléatoire à partir d'un tableau de citations que vous aurez défini en dur dans votre code.

- **Niveau Intermédiaire : API de "Notes"**
  Créez une API CRUD complète pour gérer des notes simples (titre, contenu). Les données seront stockées **en mémoire** dans un tableau (pas de base de données). Vous devez implémenter les 5 routes : `GET /notes`, `GET /notes/:id`, `POST /notes`, `PUT /notes/:id`, `DELETE /notes/:id`.

- **Niveau Avancé : API de "Livre de recettes"**
  Reprenez l'API de notes, mais cette fois-ci, connectez-la à une base de données MongoDB avec Mongoose. Le modèle `Recipe` aura un `title`, `ingredients` (un tableau de strings), et `instructions` (string). Implémentez le CRUD complet.

## 7. Mini-projet Guidé : API pour une To-Do List

On va construire le backend pour la To-Do List que vous avez faite en Vue.js.

1.  **Étape 1 : Initialisation**
    Créez un projet Node.js (`npm init`), installez `express`, `mongoose`, `dotenv`, `cors`. Structurez votre projet avec des dossiers `models`, `routes`, `controllers`.

2.  **Étape 2 : Modèle et Connexion BDD**
    Créez un modèle Mongoose `Task.js` avec un champ `text` (String, required) et `completed` (Boolean, default: false). Dans `index.js`, connectez-vous à votre base de données MongoDB.

3.  **Étape 3 : Contrôleurs et Routes CRUD**
    Créez un `taskController.js` et implémentez les 5 fonctions CRUD pour les tâches. Créez un `tasks.js` dans le dossier `routes` pour lier ces fonctions aux routes (`GET /api/tasks`, `POST /api/tasks`, etc.).

4.  **Étape 4 : Activer CORS**
    Dans `index.js`, ajoutez le middleware `cors` (`app.use(cors())`). C'est **crucial** pour permettre à votre frontend Vue.js (qui tourne sur un port différent) de communiquer avec votre API.

5.  **Étape 5 : Test avec Postman**
    Utilisez Postman pour tester chaque route de votre API une par une. Assurez-vous que vous pouvez créer une tâche, la voir dans la liste, la mettre à jour et la supprimer.

## 8. Projet Final Non Guidé : Backend pour l'Explorateur de Films

Le frontend de votre projet final précédent appelait une API externe. Vous allez maintenant créer **votre propre API** pour gérer une collection de films personnelle, avec des utilisateurs.

**Livrables :**
1.  Un dépôt GitHub contenant le code complet de votre API Node.js.
2.  Une documentation simple dans le `README.md` expliquant comment lancer le projet et quelles sont les routes disponibles (avec Postman, c'est encore mieux).
3.  **Bonus :** Connectez votre frontend Vue.js à cette nouvelle API !

**Fonctionnalités requises pour l'API :**
- **Gestion des utilisateurs :**
  - Route `POST /api/auth/register` pour créer un compte.
  - Route `POST /api/auth/login` pour se connecter et recevoir un token JWT.
- **Gestion d'une "Watchlist" personnelle :**
  - L'utilisateur doit être authentifié pour accéder à ces routes.
  - `GET /api/watchlist` : renvoie la liste des films de l'utilisateur connecté.
  - `POST /api/watchlist` : ajoute un film à la watchlist. Le corps de la requête contiendra les infos du film (ex: `movieId` de TMDb, `title`, `posterPath`).
  - `DELETE /api/watchlist/:movieId` : supprime un film de la watchlist.
- **Sécurité :**
  - Les mots de passe doivent être hachés.
  - Les routes de la watchlist doivent être protégées par un middleware d'authentification.
  - Les secrets (clé JWT, URL de BDD) doivent être dans un fichier `.env`.

## 9. Critères d'Évaluation

- **Fonctionnalité de l'API :** Les routes fonctionnent-elles comme attendu ? L'API est-elle testable via Postman ?
- **Structure du code :** Le code est-il bien organisé en suivant le pattern MVC (ou une variante) ?
- **Interaction avec la base de données :** Le schéma Mongoose est-il bien défini ? Les requêtes sont-elles logiques ?
- **Sécurité :** L'authentification est-elle fonctionnelle ? Les mots de passe sont-ils bien hachés ? Les secrets sont-ils exclus du versioning (via `.gitignore`) ?
- **Qualité du code :** Le code est-il lisible, asynchrone (`async/await`) et gère-t-il les erreurs de base (ex: via des blocs `try/catch`) ?

## 10. Ressources Complémentaires Fiables

- **Documentation Officielle de Node.js :** Pour comprendre les modules de base.
  - [nodejs.org/docs](https://nodejs.org/en/docs/)
- **Documentation Officielle d'Express.js :** Très claire et remplie d'exemples.
  - [expressjs.com](https://expressjs.com/fr/)
- **Documentation Officielle de Mongoose :** Votre référence pour tout ce qui concerne les schémas et les requêtes.
  - [mongoosejs.com/docs](https://mongoosejs.com/docs/guide.html)
- **jwt.io :** Permet de décoder et de vérifier des JWT, très utile pour le débogage.
  - [jwt.io](https://jwt.io/)
- **Postman Learning Center :** Pour apprendre à maîtriser votre client API.
  - [learning.postman.com](https://learning.postman.com/)