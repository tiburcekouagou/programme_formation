## Semaine 14 : API RESTful et Bases de Données NoSQL

### J1 : Les Principes d'une API RESTful

**Objectif(s) du Jour :**
- Comprendre ce que signifie "REST" (REpresentational State Transfer).
- Maîtriser le mapping entre les opérations CRUD et les verbes HTTP.
- Concevoir des "endpoints" (URL) centrés sur les ressources.
- Structurer son code Express en séparant les routes de la logique métier (début de l'architecture MVC).

**Notion Clé : Le Catalogue de la Bibliothèque**
Une API REST, ce n'est pas juste une collection de routes au hasard. C'est un **système de catalogage standardisé** pour les ressources de votre application.
- **Ressources :** Ce sont les "noms" de votre catalogue (les livres, les auteurs, les utilisateurs...). Une ressource est identifiée par une URL, ex: `/livres`.
- **Verbes HTTP :** Ce sont les **actions** que vous pouvez faire sur ces noms.
  - `GET /livres` : **Lire** la liste de tous les livres.
  - `GET /livres/123` : **Lire** les informations du livre avec l'ID 123.
  - `POST /livres` : **Créer** un nouveau livre.
  - `PUT /livres/123` : **Mettre à jour** complètement le livre 123.
  - `DELETE /livres/123` : **Supprimer** le livre 123.
C'est une convention universelle. En regardant une URL et un verbe HTTP, n'importe quel développeur sait ce que l'API est censée faire.

---

#### Leçon

##### 1. Les 4 Opérations CRUD et les Verbes HTTP

- **C**reate -> `POST`
- **R**ead -> `GET`
- **U**pdate -> `PUT` / `PATCH` (`PUT` remplace tout, `PATCH` modifie une partie)
- **D**elete -> `DELETE`

##### 2. Concevoir les Endpoints

Les URL doivent être des **noms** au pluriel, pas des verbes.
- ✅ Bon : `GET /articles`, `DELETE /articles/42`
- ❌ Mauvais : `GET /getAllArticles`, `GET /deleteArticleById?id=42`

##### 3. L'Architecture MVC (Modèle-Vue-Contrôleur)

Pour ne pas tout mélanger dans `server.js`, on sépare les responsabilités :
- **Modèle :** La représentation des données et l'interaction avec la base de données (on verra ça plus tard).
- **Vue :** La représentation visuelle (dans notre cas, c'est la réponse JSON).
- **Contrôleur :** Le chef d'orchestre. Il reçoit la requête, demande au Modèle de faire le travail, et envoie la Vue.

Aujourd'hui, on se concentre sur la séparation **Routes / Contrôleurs**.
- **`routes/articles.js` :** Définit les URL et les verbes HTTP.
- **`controllers/articleController.js` :** Contient la logique (les fonctions) à exécuter pour chaque route.

- **Exemple de Code :**
  ```javascript
  // Fichier: controllers/articleController.js
  const getArticles = (req, res) => {
    res.json({ message: "Récupérer tous les articles" });
  };
  module.exports = { getArticles };

  // Fichier: routes/articles.js
  const express = require('express');
  const router = express.Router();
  const articleController = require('../controllers/articleController');
  router.get('/', articleController.getArticles);
  module.exports = router;

  // Fichier: server.js
  const express = require('express');
  const app = express();
  const articleRoutes = require('./routes/articles');
  app.use('/api/articles', articleRoutes); // On monte les routes
  app.listen(3000);
  ```

---

#### Mise en Pratique

1.  Créez un nouveau projet `blog-api`.
2.  Créez l'arborescence de dossiers : `controllers/` et `routes/`.
3.  Suivez l'exemple pour créer un contrôleur `articleController.js` et un fichier de routes `articles.js`.
4.  Dans `server.js`, importez et utilisez vos routes.
5.  Testez la route `GET /api/articles` avec votre navigateur ou Postman.

#### Mini-Exercice du Jour

Dans la même structure, ajoutez les routes et les fonctions de contrôleur (pour l'instant vides, renvoyant juste un message) pour les 5 opérations CRUD de base sur les articles.

#### Synthèse

Vous avez appris à concevoir une API de manière professionnelle et standardisée. Cette structure MVC est la clé pour que votre projet reste organisé et maintenable à mesure qu'il grandit. Pour l'instant, nos données sont fausses. Demain, nous allons introduire une vraie base de données pour les rendre persistantes : MongoDB.

---

### J2 : Persistance des Données - Introduction à MongoDB

**Objectif(s) du Jour :**
- Comprendre les concepts de base d'une base de données NoSQL et de MongoDB.
- Différencier une base de données SQL (tables, lignes) d'une NoSQL (collections, documents).
- Créer un compte sur MongoDB Atlas (le service cloud) et obtenir une chaîne de connexion.
- Installer et utiliser le driver natif MongoDB pour se connecter à la base de données.

**Notion Clé : Le Classeur vs. Le Tiroir à Dossiers**
- **Base de Données SQL (ex: MySQL) :** C'est un **classeur à anneaux** avec des tableaux très stricts. Chaque page (table) a des colonnes fixes (id, nom, prix). Chaque ligne doit respecter cette structure. C'est très organisé, mais rigide.
- **Base de Données NoSQL (MongoDB) :** C'est un **tiroir à dossiers**. Chaque dossier (document) contient des informations sur une seule chose (un utilisateur, un produit). Les dossiers sont regroupés dans des tiroirs (collections). L'avantage ? Chaque dossier peut avoir une structure légèrement différente. Un dossier "utilisateur" peut avoir un champ "deuxième_prénom", un autre non. C'est flexible et ressemble beaucoup aux objets JSON que nous utilisons déjà.

---

#### Leçon

##### 1. Concepts de MongoDB

- **Base de données :** Le conteneur de plus haut niveau.
- **Collection :** Un groupe de documents. Équivalent à une "table" en SQL.
- **Document :** Un enregistrement de données au format BSON (une version binaire de JSON). Équivalent à une "ligne" en SQL.

##### 2. MongoDB Atlas

C'est la solution la plus simple pour démarrer. C'est MongoDB hébergé dans le cloud.
1.  Créer un compte sur [MongoDB Atlas](https://www.mongodb.com/cloud/atlas).
2.  Créer un "cluster" gratuit.
3.  Créer un utilisateur de base de données (avec un nom et un mot de passe).
4.  Configurer l'accès réseau pour autoriser les connexions depuis n'importe où (`0.0.0.0/0`) pour le développement.
5.  Obtenir la **chaîne de connexion** (Connection String). Elle ressemblera à `mongodb+srv://<username>:<password>@cluster...`.

##### 3. Se Connecter avec le Driver Node.js

- `npm install mongodb`
- On utilise la chaîne de connexion pour établir le lien.

- **Exemple de Code (Connexion simple) :**
  ```javascript
  const { MongoClient } = require('mongodb');

  // Remplacez par votre propre chaîne de connexion !
  const uri = "mongodb+srv://user:password@cluster.mongodb.net/?retryWrites=true&w=majority";
  const client = new MongoClient(uri);

  async function run() {
    try {
      // Se connecter au serveur
      await client.connect();
      console.log("Connecté avec succès à MongoDB !");
    } finally {
      // S'assurer que le client se ferme quand on a fini ou en cas d'erreur
      await client.close();
    }
  }
  run().catch(console.dir);
  ```

---

#### Mise en Pratique

1.  Suivez les étapes pour créer votre compte et votre cluster sur MongoDB Atlas.
2.  Créez un nouveau fichier `jour2-test-db.js` dans votre projet.
3.  Installez le paquet `mongodb`.
4.  Copiez l'exemple de code et remplacez la chaîne de connexion par la vôtre (avec votre nom d'utilisateur et votre mot de passe).
5.  Exécutez `node jour2-test-db.js`. Si tout est bien configuré, vous devriez voir le message de succès.

#### Mini-Exercice du Jour

Modifiez le script `run()` pour insérer un document dans une collection. (Indice : `const db = client.db('testdb'); const collection = db.collection('testcollection'); await collection.insertOne({ name: 'test' });`).

#### Synthèse

Vous avez maintenant une base de données puissante et professionnelle à votre disposition. Le driver natif est fonctionnel, mais un peu verbeux. Demain, nous découvrirons un outil qui rend l'interaction avec MongoDB beaucoup plus simple et élégante : Mongoose.

---

### J3 : Modéliser les Données - Mongoose

**Objectif(s) du Jour :**
- Comprendre le rôle d'un ODM (Object-Document Mapper) comme Mongoose.
- Définir un "schéma" pour structurer ses données.
- Créer un "modèle" Mongoose à partir d'un schéma.
- Utiliser les méthodes du modèle pour effectuer des opérations CRUD.

**Notion Clé : Le Moule à Gâteaux**
Utiliser le driver MongoDB natif, c'est comme modeler chaque gâteau à la main. C'est possible, mais fastidieux et vous risquez des incohérences.
**Mongoose** vous donne un **moule à gâteaux** (un **Schéma**). Ce schéma définit la forme que vos gâteaux (documents) *doivent* avoir : "il doit y avoir un champ `nom` de type chaîne de caractères, un champ `prix` de type nombre, etc.".
À partir de ce moule, Mongoose crée une "usine à gâteaux" (un **Modèle**). Cette usine dispose de machines très simples à utiliser pour `Model.create()` (créer un gâteau), `Model.find()` (trouver des gâteaux), etc. C'est la couche d'abstraction qui manquait entre votre code et la base de données.

---

#### Leçon

##### 1. Installation et Connexion

- `npm install mongoose`
- La connexion est plus simple : `mongoose.connect(uri)`

##### 2. Schéma et Modèle

- `new mongoose.Schema()` : Définit la structure et les types de données de vos documents.
- `mongoose.model()` : Crée une classe (le modèle) à partir du schéma, qui sera utilisée pour interagir avec la collection correspondante.

- **Exemple de Code (Modèle d'Article) :**
  ```javascript
  const mongoose = require('mongoose');

  // 1. Définir le Schéma
  const articleSchema = new mongoose.Schema({
    title: {
      type: String,
      required: true // On peut ajouter des validations
    },
    content: String,
    author: String,
    createdAt: {
      type: Date,
      default: Date.now // Une valeur par défaut
    }
  });

  // 2. Créer le Modèle
  // Mongoose va automatiquement chercher/créer une collection nommée 'articles' (pluriel de 'Article')
  const Article = mongoose.model('Article', articleSchema);

  // 3. Exporter le modèle pour l'utiliser dans les contrôleurs
  module.exports = Article;
  ```

---

#### Mise en Pratique

1.  Reprenez votre projet `blog-api`. Installez `mongoose`.
2.  Créez un nouveau dossier `models/` et à l'intérieur, un fichier `articleModel.js`.
3.  Dans ce fichier, définissez le schéma et le modèle pour un article, comme dans l'exemple.
4.  Dans votre `server.js`, ajoutez le code pour vous connecter à votre base de données Atlas avec `mongoose.connect()`. Mettez votre chaîne de connexion dans une variable d'environnement (`.env`) pour de bonnes pratiques. (`npm install dotenv`).

#### Mini-Exercice du Jour

Créez un petit script `seed.js` séparé qui se connecte à la DB, utilise le modèle `Article` pour créer deux ou trois articles de test, puis se déconnecte. Cela vous permettra d'avoir des données pour travailler.

#### Synthèse

Votre API a maintenant une structure de données claire et validée. Vous avez un modèle puissant pour interagir avec la base de données. Il est temps d'assembler toutes les pièces : les routes, les contrôleurs et les modèles.

---

### J4 : Le CRUD Complet avec Mongoose

**Objectif(s) du Jour :**
- Implémenter les 5 fonctions du contrôleur pour le CRUD.
- Utiliser les méthodes `find`, `findById`, `create`, `findByIdAndUpdate`, `findByIdAndDelete` de Mongoose.
- Gérer les réponses (succès, erreur) et les codes de statut HTTP appropriés.

**Notion Clé : Activer l'Usine**
Vous avez le plan des routes et l'usine à gâteaux (le modèle Mongoose). Aujourd'hui, vous allez connecter les deux. Quand un camion (requête HTTP) arrive sur la route "Créer un nouveau gâteau" (`POST /articles`), le contrôleur va prendre la recette du camion (`req.body`) et dire à l'usine : `Article.create(recette)`. L'usine fabrique le gâteau, le met en base de données, et le renvoie au contrôleur, qui peut alors dire au camion "C'est bon, votre gâteau a été créé, le voici !".

---

#### Leçon

##### Logique du Contrôleur avec le Modèle Mongoose

```javascript
// Fichier: controllers/articleController.js
const Article = require('../models/articleModel');

// READ - Tous les articles
const getArticles = async (req, res) => {
  try {
    const articles = await Article.find({});
    res.status(200).json(articles);
  } catch (error) {
    res.status(500).json({ message: error.message });
  }
};

// CREATE - Un nouvel article
const createArticle = async (req, res) => {
  try {
    const article = await Article.create(req.body);
    res.status(201).json(article); // 201 = Created
  } catch (error) {
    res.status(400).json({ message: error.message }); // 400 = Bad Request
  }
};

// ... et ainsi de suite pour findById, findByIdAndUpdate, findByIdAndDelete

module.exports = { getArticles, createArticle, /* ... */ };
```

---

#### Mise en Pratique

1.  Dans votre `articleController.js`, importez votre modèle `Article`.
2.  Implémentez la logique pour les 5 routes CRUD, en vous inspirant de l'exemple ci-dessus.
    - `GET /api/articles` -> `Article.find({})`
    - `GET /api/articles/:id` -> `Article.findById(req.params.id)`
    - `POST /api/articles` -> `Article.create(req.body)`
    - `PUT /api/articles/:id` -> `Article.findByIdAndUpdate(req.params.id, req.body, { new: true })`
    - `DELETE /api/articles/:id` -> `Article.findByIdAndDelete(req.params.id)`
3.  N'oubliez pas d'utiliser `try...catch` pour chaque fonction asynchrone afin de gérer les erreurs.

#### Mini-Exercice du Jour

Utilisez Postman ou Thunder Client pour tester **chaque endpoint** de votre API. Vérifiez que vous pouvez créer un article, le lister, le voir en détail, le mettre à jour et le supprimer.

#### Synthèse

Votre API est maintenant complète, fonctionnelle et persistante. C'est une API RESTful professionnelle que n'importe quel client (une application Vue, une application mobile...) pourrait consommer.

---

### J5 : Projet de la Semaine - API RESTful pour un Blog

**Objectif(s) du Jour :**
- Consolider toutes les connaissances de la semaine en un projet complet.
- Assurer que le code est bien structuré (MVC).
- Créer une API documentée (implicitement via la structure REST).
- Disposer d'un backend solide prêt à être connecté à un frontend.

**Notion Clé : L'Inauguration de la Bibliothèque**
Vous avez passé la semaine à construire une bibliothèque : vous avez défini son catalogue (les principes REST), construit le bâtiment (le serveur Express), installé les étagères (la base de données MongoDB) et créé un système de gestion des livres (le modèle Mongoose). Aujourd'hui, c'est l'inauguration. Vous allez vérifier que chaque service fonctionne parfaitement : emprunter un livre, en ajouter un nouveau, consulter sa fiche... Votre projet final est cette bibliothèque entièrement fonctionnelle.

---

#### PROJET DE LA SEMAINE : API Complète pour un Blog

Votre mission est de finaliser et de peaufiner l'API pour un blog que vous avez construite tout au long de la semaine.

**Structure et Fonctionnalités Obligatoires :**

1.  **Structure du Projet :**
    - `server.js` : Point d'entrée, connexion à la DB, montage des middlewares et des routes.
    - `models/articleModel.js` : Schéma et Modèle Mongoose pour les articles.
    - `routes/articleRoutes.js` : Définition des 5 endpoints RESTful pour le CRUD des articles.
    - `controllers/articleController.js` : Logique de chaque route, interaction avec le modèle.
    - `.env` : Fichier pour stocker les variables d'environnement comme la chaîne de connexion à la base de données.

2.  **Modèle `Article` :**
    - Doit contenir au minimum : `title` (String, requis), `content` (String, requis), `author` (String).
    - Doit inclure un champ `createdAt` qui se remplit automatiquement avec la date de création.

3.  **API Endpoints :**
    - `GET /api/articles` : Renvoie un tableau de tous les articles.
    - `GET /api/articles/:id` : Renvoie un seul article par son ID. Doit gérer le cas où l'ID n'existe pas (Mongoose renvoie `null`, votre API doit renvoyer un 404).
    - `POST /api/articles` : Crée un nouvel article à partir du `req.body`. Doit renvoyer un statut 201 et l'article créé.
    - `PUT /api/articles/:id` : Met à jour un article existant.
    - `DELETE /api/articles/:id` : Supprime un article existant.

4.  **Gestion d'Erreurs :**
    - Chaque fonction de contrôleur doit être enveloppée dans un bloc `try...catch` pour répondre avec un code d'erreur 500 (Internal Server Error) si quelque chose se passe mal côté serveur.
    - Les routes de création et de mise à jour doivent renvoyer un code 400 (Bad Request) si les données envoyées sont invalides (ex: un titre manquant, Mongoose lèvera une erreur de validation).

**Livrable :** Un dépôt GitHub contenant votre projet d'API complet. Le `README.md` doit être particulièrement soigné et servir de mini-documentation : il doit lister chaque endpoint, son verbe HTTP, ce qu'il fait, et un exemple de corps de requête (pour POST/PUT) et de réponse.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez construit une véritable API RESTful de A à Z. Vous avez appris à structurer votre code, à modéliser des données et à les rendre persistantes dans une base de données NoSQL moderne. Vous disposez maintenant d'un backend robuste, prêt à être consommé par le frontend Vue que vous avez créé précédemment. La semaine prochaine, nous aborderons un sujet crucial : comment sécuriser cette API en gérant les utilisateurs et l'authentification.