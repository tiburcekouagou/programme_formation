## Semaine 16 : Sécurité, Déploiement et Full-Stack

### J1 : Validation des Données d'Entrée

**Objectif(s) du Jour :**
- Comprendre pourquoi il est crucial de valider les données envoyées par le client.
- Utiliser une librairie de validation comme `express-validator`.
- Mettre en place des règles de validation pour les routes d'enregistrement et de création d'article.
- Renvoyer des messages d'erreur clairs en cas de validation échouée.

**Notion Clé : Le Videur à l'Entrée du Club**
Votre API est un club privé. Jusqu'à présent, vous laissiez entrer n'importe qui du moment qu'il disait être sur la liste, sans vérifier sa carte d'identité ou son état. C'est dangereux.
Un **validateur de données**, c'est le **videur** à l'entrée.
- "Pour t'inscrire (`/register`), tu dois me donner un `email` qui ressemble VRAIMENT à un email, et un `password` qui fait au moins 6 caractères."
- "Pour créer un article (`/articles`), le `title` ne doit pas être vide."
Si les données fournies par le client ne respectent pas ces règles, le videur le refoule immédiatement (`res.status(400)`) en lui disant pourquoi, sans même déranger le manager du club (le contrôleur). C'est votre première ligne de défense contre les données corrompues ou malveillantes.

---

#### Leçon

##### 1. Pourquoi Valider Côté Backend ?

Même si votre frontend a des validations, un utilisateur malveillant peut toujours appeler votre API directement (avec Postman, un script, etc.). La validation côté backend est la **seule source de vérité** et est non négociable.

##### 2. `express-validator`

- `npm install express-validator`
- C'est une collection de middlewares que l'on place dans la définition de nos routes.

- **Exemple de Code (Validation sur la route d'enregistrement) :**
  ```javascript
  // routes/authRoutes.js
  const { body, validationResult } = require('express-validator');

  router.post(
    '/register',
    // On place les middlewares de validation ici
    body('email').isEmail().withMessage('Veuillez fournir un email valide'),
    body('password').isLength({ min: 6 }).withMessage('Le mot de passe doit faire au moins 6 caractères'),
    (req, res, next) => { // Un middleware pour vérifier le résultat
      const errors = validationResult(req);
      if (!errors.isEmpty()) {
        return res.status(400).json({ errors: errors.array() });
      }
      next(); // Si pas d'erreurs, on passe au contrôleur
    },
    authController.registerUser // Le contrôleur n'est appelé que si la validation passe
  );
  ```

---

#### Mise en Pratique

1.  Installez `express-validator` dans votre projet `blog-api`.
2.  Modifiez votre `authRoutes.js` pour ajouter la validation sur la route `/register` comme dans l'exemple.
3.  Testez avec Postman : essayez de créer un compte avec un email invalide ou un mot de passe trop court. Vous devriez recevoir une erreur 400 avec la liste des problèmes.
4.  Ajoutez une validation sur votre route `POST /api/articles` pour vous assurer que les champs `title` et `content` ne sont pas vides (`.not().isEmpty()`).

#### Mini-Exercice du Jour

Créez un middleware de validation réutilisable. Au lieu de répéter la logique `validationResult` dans chaque route, créez une fonction `validate` qui fait ce travail et que vous pouvez importer et utiliser.

#### Synthèse

Votre API est maintenant beaucoup plus robuste. Elle refuse les données invalides à la source, ce qui prévient de nombreux bugs et problèmes de sécurité. Demain, nous allons améliorer la gestion globale des erreurs pour rendre notre code encore plus propre.

---

### J2 : Gestion Centralisée des Erreurs et CORS

**Objectif(s) du Jour :**
- Créer un middleware de gestion d'erreurs centralisé.
- Comprendre et utiliser le `try...catch` avec les fonctions `async` et `next`.
- Comprendre ce qu'est CORS (Cross-Origin Resource Sharing) et pourquoi c'est nécessaire.
- Mettre en place le middleware `cors`.

**Notion Clé : Le Service d'Urgence et le Laissez-passer**
- **Gestion des Erreurs :** Imaginez une usine. Si une machine tombe en panne, l'ouvrier (`try...catch`) ne essaie pas de la réparer lui-même. Il appuie sur un gros bouton rouge qui appelle le **service d'urgence** (`le middleware d'erreur`). Ce service centralisé sait exactement quoi faire : arrêter la chaîne, enregistrer l'incident, et afficher un message standard. Dans Express, on appelle `next(error)` pour déclencher ce service.
- **CORS :** Par défaut, les navigateurs interdisent à une page web hébergée sur `http://site-frontend.com` de faire des requêtes à une API sur `http://api-backend.com`. C'est une politique de sécurité. Le **middleware `cors`** est un **laissez-passer** que votre API donne au navigateur, en disant : "C'est bon, j'autorise `http://site-frontend.com` à me parler".

---

#### Leçon

##### 1. Middleware de Gestion d'Erreurs

C'est un middleware spécial qui prend 4 arguments (`err`, `req`, `res`, `next`). Il doit être placé **à la toute fin** de votre fichier `server.js`, après toutes les routes.

```javascript
// server.js
const errorHandler = (err, req, res, next) => {
  const statusCode = res.statusCode ? res.statusCode : 500;
  res.status(statusCode);
  res.json({
    message: err.message,
    stack: process.env.NODE_ENV === 'production' ? null : err.stack,
  });
};
// ...
app.use(errorHandler);
```
Dans vos contrôleurs, au lieu de `res.status(500)...`, vous pouvez simplement faire `next(new Error('Message'))` dans votre bloc `catch`.

##### 2. CORS (Cross-Origin Resource Sharing)

- `npm install cors`
- On l'utilise comme un middleware global au début du `server.js`.

```javascript
// server.js
const cors = require('cors');
// ...
app.use(cors()); // Autorise toutes les origines (simple pour le dev)
// Pour la production, on le configure :
// app.use(cors({ origin: 'http://mon-frontend.com' }));
```

---

#### Mise en Pratique

1.  Installez `cors`.
2.  Dans votre `server.js`, mettez en place le middleware `cors` au début, et le `errorHandler` à la fin.
3.  Refactorisez un de vos contrôleurs : dans le bloc `catch`, remplacez `res.status(500).json(...)` par `next(error)`.
4.  Pour tester, introduisez une erreur volontaire dans un contrôleur et vérifiez que votre `errorHandler` prend bien le relais.

#### Mini-Exercice du Jour

Installez `express-async-handler` (`npm install express-async-handler`). C'est un petit utilitaire qui enveloppe vos fonctions de contrôleur et gère automatiquement le `try...catch` et l'appel à `next(error)` pour vous, rendant votre code encore plus propre.

#### Synthèse

Votre API est maintenant prête à être consommée par une application externe, et sa gestion d'erreurs est plus robuste et centralisée. Il est temps de mettre votre API en ligne !

---

### J3 : Mettre en Ligne - Déploiement sur Render

**Objectif(s) du Jour :**
- Comprendre les principes du déploiement d'une application Node.js.
- Utiliser les variables d'environnement pour la configuration en production.
- Déployer son API sur un service d'hébergement comme Render (alternative moderne à Heroku).
- Tester son API en ligne.

**Notion Clé : Déménager dans un Vrai Bureau**
Jusqu'à présent, votre API tournait sur votre ordinateur portable (`localhost`), qui est comme un bureau à domicile. Si vous éteignez votre ordinateur, le service est coupé.
Le **déploiement**, c'est **déménager votre API dans un vrai bureau** dans un immeuble sécurisé et toujours alimenté en électricité (les serveurs de **Render**).
- Vous donnez vos instructions de construction (`package.json`).
- Vous leur donnez le code source (via GitHub).
- Vous leur donnez les clés secrètes (`les variables d'environnement` comme `MONGO_URI`, `JWT_SECRET`) via leur interface sécurisée, pas en les écrivant sur les cartons.
Render va alors construire et lancer votre application sur une adresse publique, accessible depuis n'importe où dans le monde.

---

#### Leçon

##### 1. Préparer le Déploiement

- **`process.env.PORT` :** Votre serveur ne doit pas écouter sur un port fixe comme `3000`. L'hébergeur vous en assignera un. `const port = process.env.PORT || 3000;`.
- **Scripts NPM :** Assurez-vous d'avoir un script `start` dans votre `package.json` : `"start": "node server.js"`.
- **Git :** Votre projet doit être un dépôt Git et poussé sur GitHub.

##### 2. Déploiement sur Render

1.  Créez un compte sur [Render.com](https://render.com/).
2.  Dans le tableau de bord, cliquez sur "New" -> "Web Service".
3.  Connectez votre compte GitHub et sélectionnez le dépôt de votre API.
4.  Render détecte automatiquement que c'est un projet Node.js.
    - **Build Command :** `npm install` (généralement auto-détecté)
    - **Start Command :** `npm start` (ou `node server.js`)
5.  Allez dans la section "Environment" et ajoutez vos variables d'environnement (`MONGO_URI`, `JWT_SECRET`, `NODE_ENV=production`). **Ne les mettez jamais en clair dans votre code !**
6.  Cliquez sur "Create Web Service". Render va builder et déployer votre application.
7.  Une fois terminé, Render vous donnera une URL publique (ex: `https://blog-api-xyz.onrender.com`).

---

#### Mise en Pratique

1.  Assurez-vous que votre projet est sur GitHub.
2.  Adaptez votre code pour utiliser `process.env.PORT`.
3.  Suivez les étapes pour déployer votre API sur Render.
4.  Une fois l'URL publique obtenue, utilisez Postman pour tester quelques routes de votre API en ligne (ex: `GET https://VOTRE_URL.onrender.com/api/articles`).

#### Mini-Exercice du Jour

Dans votre code, vérifiez la variable `process.env.NODE_ENV`. Si elle est égale à `'production'`, ne renvoyez pas la pile d'erreurs (`err.stack`) dans votre `errorHandler`.

#### Synthèse

Félicitations ! Votre API n'est plus un projet local, c'est un service web public et fonctionnel. C'est une étape majeure pour tout développeur. Maintenant que le backend est en ligne, il est temps de connecter le frontend.

---

### J4 & J5 : Le Grand Assemblage - Le Projet Full-Stack

**Objectif(s) du Jour :**
- Comprendre comment un frontend et un backend communiquent en production.
- Modifier le frontend Vue.js pour qu'il appelle la nouvelle API déployée au lieu d'une fausse API.
- Gérer l'envoi du JWT depuis le frontend pour les requêtes authentifiées.
- Finaliser et présenter une application Full-Stack complète et fonctionnelle.

**Notion Clé : Le Coup de Téléphone International**
Votre frontend Vue (Module 3) est un client à Paris. Votre backend Node (Module 4) est un bureau à New York, avec une adresse publique (votre URL Render).
1.  **Appel simple :** Pour afficher la liste des articles, le client parisien ne compose plus un numéro local (JSONPlaceholder), il compose le numéro international de votre bureau new-yorkais (`https://VOTRE_URL.onrender.com/api/articles`).
2.  **Appel sécurisé :** Pour créer un article, le client doit d'abord appeler le bureau de sécurité (`/api/auth/login`) pour obtenir un badge (le JWT). Ensuite, pour chaque requête sécurisée, il attache ce badge à son dossier (l'en-tête `Authorization: Bearer ...`). Le bureau de New York vérifiera le badge avant de traiter la demande.

---

#### PROJET DE LA SEMAINE : Connecter le Frontend Vue au Backend Node

Votre mission est de prendre votre projet de blog Vue.js (de la semaine 12) et de le faire communiquer avec l'API Node.js que vous venez de déployer.

**Étapes et Fonctionnalités Obligatoires :**

1.  **Modification du Frontend (Projet Vue) :**
    - **Variable d'environnement :** Créez une variable d'environnement dans votre projet Vue (`VUE_APP_API_URL` ou `VITE_API_URL`) qui contient l'URL de votre API déployée sur Render.
    - **Store Pinia (`postStore`) :** Modifiez les actions `fetchAllPosts` et `fetchPostById` pour qu'elles appellent les routes de votre propre API (`GET /api/articles` et `GET /api/articles/:id`) au lieu de JSONPlaceholder.
    - **Authentification :**
      - Créez un nouveau store Pinia, `authStore`, pour gérer la logique d'authentification.
      - Il doit avoir un `state` pour stocker le `token` et les informations de l'utilisateur.
      - Il doit avoir des `actions` `login(userData)` et `register(userData)` qui appellent les routes `/api/auth/login` et `/api/auth/register` de votre backend.
      - Après une connexion/inscription réussie, le `token` reçu doit être stocké dans le `state` et dans le `localStorage` du navigateur pour la persistance.
    - **Gestion du Token :**
      - Configurez votre client HTTP (Axios) dans le frontend pour qu'il ajoute automatiquement l'en-tête `Authorization: Bearer <token>` à chaque requête si un token est présent dans le `authStore`. C'est souvent fait avec des "intercepteurs" Axios.

2.  **Nouvelles Fonctionnalités Frontend :**
    - Créez des pages/composants pour l'**Inscription** et la **Connexion**.
    - Cachez les boutons "Créer un article", "Modifier", "Supprimer" si l'utilisateur n'est pas connecté.
    - Créez une page de formulaire pour **Créer un nouvel article**, qui ne sera accessible qu'aux utilisateurs connectés. La soumission du formulaire doit appeler votre route `POST /api/articles` avec le token.

3.  **Déploiement du Frontend :**
    - Déployez votre application frontend Vue.js sur un service comme Netlify ou Vercel.

**Livrable :**
- L'URL de votre API backend déployée (Render).
- L'URL de votre application frontend déployée (Netlify/Vercel).
- Un dépôt GitHub pour le frontend et un pour le backend, tous deux à jour.
- L'application doit être entièrement fonctionnelle : on doit pouvoir s'inscrire, se connecter, voir les articles, et en créer de nouveaux en tant qu'utilisateur connecté.

#### Synthèse Finale de la Semaine et du Module

**Félicitations monumentales !** Vous avez accompli ce qui définit un développeur Full-Stack : vous avez conçu, développé, sécurisé, déployé et connecté un backend et un frontend pour créer une application web complète. Vous avez traversé l'écosystème JavaScript, de la manipulation du DOM à la gestion d'une base de données en passant par la création d'API. Le projet de cette semaine est la pièce maîtresse de votre portfolio jusqu'à présent. Le prochain module vous ouvrira à un autre écosystème backend majeur, PHP et Laravel, faisant de vous un développeur encore plus polyvalent et recherché.