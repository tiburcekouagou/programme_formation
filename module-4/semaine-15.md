## Semaine 15 : Authentification et Gestion des Utilisateurs

### J1 : Stocker les Utilisateurs en Toute Sécurité - Modèle et Hachage

**Objectif(s) du Jour :**
- Créer un modèle Mongoose pour les utilisateurs.
- Comprendre pourquoi il ne faut JAMAIS stocker les mots de passe en clair.
- Utiliser la librairie `bcrypt` pour hacher les mots de passe avant de les sauvegarder.
- Créer une première route pour enregistrer un nouvel utilisateur (`register`).

**Notion Clé : Le Secret du Coffre-Fort**
Stocker un mot de passe en clair dans votre base de données, c'est comme écrire le code de votre coffre-fort sur un Post-it collé dessus. Si un voleur (un hacker) accède à votre base de données, il a accès à tout.
Le **hachage**, c'est un processus à sens unique qui transforme votre mot de passe ("`password123`") en une chaîne de caractères longue et incompréhensible ("`$2b$10$AbC...`"). Il est quasi impossible de retrouver le mot de passe original à partir du hash.
Quand un utilisateur se connecte, il vous redonne son mot de passe. Vous ne comparez pas les mots de passe, vous **hachez celui qu'il vient de vous donner et vous comparez les deux hashes**. C'est comme avoir deux clés : vous ne les comparez pas visuellement, vous essayez les deux dans la serrure pour voir si elles ouvrent.

---

#### Leçon

##### 1. Le Modèle Utilisateur

On crée un modèle Mongoose `userModel.js` avec au minimum un email (unique) et un mot de passe.

```javascript
// models/userModel.js
const mongoose = require('mongoose');

const userSchema = new mongoose.Schema({
  email: {
    type: String,
    required: [true, 'Veuillez entrer un email'],
    unique: true, // L'email doit être unique
    lowercase: true,
  },
  password: {
    type: String,
    required: [true, 'Veuillez entrer un mot de passe'],
  },
});

module.exports = mongoose.model('User', userSchema);
```

##### 2. Hachage avec `bcrypt`

- `npm install bcrypt`
- `bcrypt.hash(motDePasseEnClair, salt)` : Crée le hash. Le `salt` est un nombre de "tours" de hachage (généralement 10).
- `bcrypt.compare(motDePasseEnClair, motDePasseHache)` : Compare un mot de passe fourni avec un hash stocké. Retourne `true` ou `false`.

##### 3. Route d'Enregistrement

- **Exemple de Code (Contrôleur d'enregistrement) :**
  ```javascript
  // controllers/authController.js
  const User = require('../models/userModel');
  const bcrypt = require('bcrypt');

  const registerUser = async (req, res) => {
    try {
      const { email, password } = req.body;
      
      // 1. Hacher le mot de passe
      const salt = await bcrypt.genSalt(10);
      const hashedPassword = await bcrypt.hash(password, salt);
      
      // 2. Créer l'utilisateur avec le mot de passe haché
      const user = await User.create({ email, password: hashedPassword });
      
      res.status(201).json({ id: user._id, email: user.email });
    } catch (error) {
      res.status(400).json({ message: 'Erreur lors de la création du compte', error: error.message });
    }
  };
  
  module.exports = { registerUser };
  ```

---

#### Mise en Pratique

1.  Dans votre projet `blog-api`, installez `bcrypt`.
2.  Créez le fichier `models/userModel.js` avec le schéma utilisateur.
3.  Créez une nouvelle structure de routes/contrôleurs pour l'authentification : `routes/authRoutes.js` et `controllers/authController.js`.
4.  Implémentez la route `POST /api/auth/register` et la fonction `registerUser` correspondante.
5.  Utilisez Postman pour créer un nouvel utilisateur. Vérifiez dans votre base de données MongoDB Atlas que le mot de passe stocké est bien une longue chaîne de caractères hachée.

#### Mini-Exercice du Jour

Ajoutez une validation simple dans votre contrôleur `registerUser` pour vérifier que l'email et le mot de passe ne sont pas vides avant de continuer.

#### Synthèse

Vous avez mis en place la première et la plus cruciale étape de l'authentification : un stockage sécurisé des informations d'identification. Vous savez maintenant enregistrer des utilisateurs. Demain, nous verrons comment ils peuvent se connecter.

---

### J2 : Connexion des Utilisateurs - La Stratégie

**Objectif(s) du Jour :**
- Créer une route de connexion (`login`).
- Vérifier les informations d'identification fournies par l'utilisateur.
- Utiliser `bcrypt.compare` pour valider le mot de passe.
- Comprendre le besoin d'une "preuve" de connexion à renvoyer au client.

**Notion Clé : Le Badge d'Accès**
Quand vous vous connectez à un service en ligne, vous ne rentrez pas votre mot de passe à chaque nouvelle page que vous visitez. Ce serait infernal.
Le processus de connexion (`login`), c'est comme se présenter au bureau de la sécurité d'un immeuble.
1.  Vous donnez votre nom (`email`) et votre mot secret (`password`).
2.  L'agent de sécurité (`le serveur`) vérifie dans son registre si votre nom existe et si votre mot secret correspond à celui qu'il a (en utilisant `bcrypt.compare`).
3.  Si tout est bon, il ne vous dit pas simplement "OK, vous pouvez entrer". Il vous donne un **badge d'accès temporaire**.
Dorénavant, pour entrer dans n'importe quel bureau de l'immeuble, vous n'avez plus besoin de redonner votre mot secret, il vous suffit de présenter votre badge. Demain, nous verrons comment fabriquer ce badge (le JWT), mais aujourd'hui, nous construisons le bureau de la sécurité.

---

#### Leçon

##### La Logique du Contrôleur de Connexion

1.  **Trouver l'utilisateur :** Chercher dans la base de données un utilisateur avec l'email fourni. S'il n'existe pas, c'est une erreur.
2.  **Comparer les mots de passe :** Si l'utilisateur existe, utiliser `bcrypt.compare` pour vérifier si le mot de passe fourni correspond au hash stocké en base de données. Si ce n'est pas le cas, c'est une erreur.
3.  **Succès :** Si les deux étapes réussissent, l'utilisateur est authentifié.

- **Exemple de Code (Contrôleur de connexion) :**
  ```javascript
  // controllers/authController.js
  const loginUser = async (req, res) => {
    try {
      const { email, password } = req.body;

      // 1. Vérifier si l'utilisateur existe
      const user = await User.findOne({ email });
      if (!user) {
        return res.status(401).json({ message: 'Identifiants invalides' }); // 401 Unauthorized
      }

      // 2. Vérifier si le mot de passe correspond
      const isMatch = await bcrypt.compare(password, user.password);
      if (!isMatch) {
        return res.status(401).json({ message: 'Identifiants invalides' });
      }
      
      // 3. Si tout est bon, l'utilisateur est connecté !
      // Pour l'instant, on envoie juste un message de succès.
      res.status(200).json({ message: 'Connexion réussie !' });
      
    } catch (error) {
      res.status(500).json({ message: 'Erreur serveur', error: error.message });
    }
  };
  ```

---

#### Mise en Pratique

1.  Dans votre `authController.js`, ajoutez la fonction `loginUser`.
2.  Dans `authRoutes.js`, ajoutez la route `POST /api/auth/login`.
3.  Utilisez Postman pour tester la connexion avec un utilisateur que vous avez créé la veille.
4.  Testez les cas d'erreur : un mauvais email, un mauvais mot de passe. Assurez-vous de recevoir les messages et les codes de statut appropriés.

#### Mini-Exercice du Jour

Refactorisez le message d'erreur. Au lieu de dire "Utilisateur non trouvé" ou "Mot de passe incorrect", renvoyez un message générique comme "Email ou mot de passe incorrect" dans les deux cas. C'est une meilleure pratique de sécurité pour ne pas donner d'indices à un attaquant (ne pas lui dire si c'est l'email ou le mot de passe qui est faux).

#### Synthèse

Vous avez maintenant un système d'enregistrement et de connexion fonctionnel et sécurisé. L'utilisateur peut prouver son identité, mais le serveur l'oublie immédiatement. Demain, nous allons résoudre ce problème en générant un "badge d'accès" numérique infalsifiable : le JSON Web Token (JWT).

---

### J3 : Le Badge d'Accès Numérique - JSON Web Token (JWT)

**Objectif(s) du Jour :**
- Comprendre la structure et le rôle d'un JWT.
- Installer et utiliser la librairie `jsonwebtoken`.
- Générer un token lors d'une connexion réussie.
- Inclure des informations utiles (le "payload") dans le token.

**Notion Clé : Le Billet de Festival**
Un JWT est comme un billet de festival.
1.  **Header (En-tête) :** Le type de billet et l'algorithme de signature. C'est l'équivalent de "Billet VIP, imprimé par TicketMaster".
2.  **Payload (Charge utile) :** Les informations sur vous. Votre nom (`name: 'Alice'`), votre ID (`id: 123`), et surtout, une date d'expiration (`exp`). Ce ne sont pas des informations secrètes, juste des informations utiles.
3.  **Signature :** C'est la partie la plus importante. C'est l'hologramme de sécurité sur le billet. Le serveur prend le Header, le Payload, y ajoute une **clé secrète** que lui seul connaît, et crée une signature unique.
Si un fraudeur essaie de modifier le Payload (par exemple, changer son nom pour accéder à la zone VIP), la signature ne correspondra plus. L'agent de sécurité (le serveur) verra que l'hologramme est faux et refusera l'accès.

---

#### Leçon

##### 1. Installation et Configuration

- `npm install jsonwebtoken`
- Définir une clé secrète dans votre fichier `.env` (ex: `JWT_SECRET=unelonguechainealeatoiretresecrete`).

##### 2. Générer un Token

On utilise `jwt.sign(payload, secret, options)`.

- **Exemple de Code (Mise à jour du contrôleur de connexion) :**
  ```javascript
  const jwt = require('jsonwebtoken');

  const loginUser = async (req, res) => {
    // ... (vérification de l'email et du mot de passe comme hier)

    // Si la connexion est réussie:
    // 1. Créer le payload du token
    const payload = {
      id: user._id,
      email: user.email,
      // On peut ajouter d'autres infos, comme un rôle
    };

    // 2. Signer le token
    const token = jwt.sign(
      payload,
      process.env.JWT_SECRET, // Récupère le secret depuis les variables d'environnement
      { expiresIn: '1h' } // Le token expirera dans 1 heure
    );
    
    // 3. Envoyer le token au client
    res.status(200).json({
      message: 'Connexion réussie !',
      token: token
    });
  };
  ```

---

#### Mise en Pratique

1.  Installez `jsonwebtoken` et `dotenv` (`npm install dotenv`).
2.  Créez un fichier `.env` à la racine de votre projet et ajoutez-y `JWT_SECRET=VOTRE_SECRET_ICI`.
3.  Au début de votre `server.js`, ajoutez `require('dotenv').config();`.
4.  Modifiez votre fonction `loginUser` pour générer et renvoyer un JWT en cas de succès, comme dans l'exemple.
5.  Testez à nouveau votre route de connexion avec Postman. Vous devriez maintenant recevoir un token dans la réponse. Copiez ce token, vous en aurez besoin demain.

#### Mini-Exercice du Jour

Rendez-vous sur le site [jwt.io](https://jwt.io/). Collez le token que vous avez généré dans la partie "Encoded". Vous verrez que le site est capable de décoder le Header et le Payload (prouvant qu'ils ne sont pas secrets), mais il signalera la signature comme étant invalide car il ne connaît pas votre `JWT_SECRET`.

#### Synthèse

Vous savez maintenant comment créer une preuve d'authentification sécurisée et standardisée. Le client peut stocker ce token et le présenter à chaque requête pour prouver son identité. Demain, nous allons créer le middleware qui vérifiera la validité de ce token sur les routes protégées.

---

### J4 : Protéger les Routes - Le Middleware d'Authentification

**Objectif(s) du Jour :**
- Créer un middleware `protect` pour vérifier la validité d'un JWT.
- Utiliser `jwt.verify` pour décoder et valider le token.
- Extraire les informations de l'utilisateur depuis le token et les attacher à l'objet `req`.
- Appliquer ce middleware aux routes qui nécessitent une authentification.

**Notion Clé : L'Agent de Sécurité à l'Entrée du Bureau**
Maintenant que le client a son badge d'accès (le JWT), il veut entrer dans un bureau sécurisé (une **route protégée**, ex: `POST /api/articles`).
À l'entrée de ce bureau se trouve un agent de sécurité (le **middleware `protect`**).
1.  Le client présente son badge. Par convention, il le met dans l'en-tête `Authorization` de sa requête, sous la forme `Bearer <token>`.
2.  L'agent (`protect`) prend le badge, vérifie l'hologramme (`jwt.verify`) en utilisant sa lampe à UV secrète (la `JWT_SECRET`).
3.  Si le badge est valide et non expiré, l'agent lit le nom sur le badge et l'attache au dossier du client (`req.user = decodedPayload`), puis lui dit "Passez" (`next()`).
4.  Si le badge est invalide, faux ou expiré, l'agent refuse l'accès (`res.status(401)`).

---

#### Leçon

##### Le Middleware `protect`

```javascript
// middleware/authMiddleware.js
const jwt = require('jsonwebtoken');
const User = require('../models/userModel');

const protect = async (req, res, next) => {
  let token;
  // On vérifie si l'en-tête Authorization existe et commence par 'Bearer'
  if (req.headers.authorization && req.headers.authorization.startsWith('Bearer')) {
    try {
      // 1. Extraire le token (sans le 'Bearer ')
      token = req.headers.authorization.split(' ')[1];

      // 2. Vérifier le token
      const decoded = jwt.verify(token, process.env.JWT_SECRET);
      
      // 3. Attacher l'utilisateur à la requête (sans le mot de passe)
      req.user = await User.findById(decoded.id).select('-password');
      
      next(); // Passer au prochain middleware ou à la route
    } catch (error) {
      res.status(401).json({ message: 'Non autorisé, token invalide' });
    }
  }

  if (!token) {
    res.status(401).json({ message: 'Non autorisé, pas de token' });
  }
};

module.exports = { protect };
```
##### Appliquer le Middleware

On l'importe dans notre fichier de routes et on le place avant les contrôleurs des routes à protéger.

```javascript
// routes/articleRoutes.js
const { protect } = require('../middleware/authMiddleware');

// Cette route est publique
router.get('/', getArticles);

// Ces routes sont maintenant protégées
router.post('/', protect, createArticle);
router.put('/:id', protect, updateArticle);
router.delete('/:id', protect, deleteArticle);
```

---

#### Mise en Pratique

1.  Créez le dossier `middleware/` et le fichier `authMiddleware.js`.
2.  Implémentez le middleware `protect`.
3.  Dans votre `articleRoutes.js`, importez et appliquez le middleware `protect` aux routes de création, mise à jour et suppression d'articles.
4.  Avec Postman, essayez d'accéder à `POST /api/articles` **sans** le token. Vous devriez recevoir une erreur 401.
5.  Maintenant, ajoutez un en-tête `Authorization` avec la valeur `Bearer VOTRE_TOKEN_COPIÉ_HIER`. Réessayez : la requête devrait passer.

#### Mini-Exercice du Jour

Dans votre contrôleur `createArticle`, modifiez-le pour que l'auteur de l'article soit automatiquement l'ID de l'utilisateur connecté. (Indice : `const article = await Article.create({ ..., author: req.user.id })`).

#### Synthèse

Votre API est maintenant capable de faire la distinction entre les utilisateurs anonymes et les utilisateurs connectés. Vous avez mis en place le mécanisme de protection standard pour les API REST. Vous êtes prêt à finaliser le projet.

---

### J5 : Projet de la Semaine - API de Blog avec Authentification

**Objectif(s) du Jour :**
- Intégrer toutes les notions de la semaine en un système d'authentification complet.
- Assurer que les routes sensibles sont bien protégées.
- Lier la création de ressources (articles) à l'utilisateur authentifié.
- Disposer d'une API backend complète, prête pour un projet full-stack.

**Notion Clé : La Bibliothèque avec Espace Membre**
Vous reprenez votre projet de bibliothèque de la semaine dernière, mais vous y ajoutez un **espace membre**.
- Tout le monde peut venir et consulter la liste des livres (`GET /api/articles`).
- Mais pour proposer un nouveau livre (`POST /api/articles`) ou en modifier un (`PUT`), il faut être un membre enregistré et connecté.
Votre mission est de finaliser ce système : la borne d'inscription (`/register`), le bureau d'accueil pour se connecter et obtenir son badge (`/login`), et les agents de sécurité à l'entrée des zones réservées (le middleware `protect`).

---

#### PROJET DE LA SEMAINE : Finaliser l'API avec Authentification

Votre mission est d'intégrer un système d'authentification complet et fonctionnel à votre API de blog.

**Structure et Fonctionnalités Obligatoires :**

1.  **Modèles :**
    - Un `userModel` avec email (unique) et mot de passe.
    - Un `articleModel` qui inclut maintenant une référence à l'auteur : `author: { type: mongoose.Schema.Types.ObjectId, required: true, ref: 'User' }`.

2.  **Routes d'Authentification (`/api/auth`) :**
    - `POST /register` : Crée un nouvel utilisateur en hachant son mot de passe.
    - `POST /login` : Vérifie les identifiants, et si corrects, renvoie un JWT valide pour 1 heure.

3.  **Middleware d'Authentification :**
    - Un middleware `protect` qui vérifie la présence et la validité d'un token JWT dans l'en-tête `Authorization: Bearer`.
    - S'il est valide, il attache les données de l'utilisateur à `req.user`.
    - Sinon, il renvoie une erreur 401.

4.  **Routes d'Articles Protégées (`/api/articles`) :**
    - Les routes `GET` (lister tous les articles et voir un détail) restent publiques.
    - Les routes `POST`, `PUT`, `DELETE` doivent être protégées par le middleware `protect`.
    - La route `POST /api/articles` doit automatiquement assigner l'ID de l'utilisateur connecté (`req.user.id`) comme auteur de l'article créé.
    - (Bonus) Les routes `PUT` et `DELETE` doivent vérifier que l'utilisateur qui fait la demande est bien l'auteur de l'article avant de procéder.

**Livrable :** Un dépôt GitHub contenant votre API complète. Le `README.md` doit être mis à jour pour inclure la documentation des routes d'authentification et préciser quelles routes d'articles sont maintenant protégées et comment s'authentifier pour les utiliser (en passant le token).

#### Synthèse Finale de la Semaine

Félicitations ! Votre API est passée d'un simple service de données public à une application backend sécurisée et multi-utilisateurs. Vous avez maîtrisé les concepts fondamentaux de l'authentification par token, une compétence absolument essentielle pour tout développeur backend. La semaine prochaine, vous peaufinerez cette API en ajoutant des fonctionnalités avancées comme la validation des données d'entrée et le déploiement.