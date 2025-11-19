## Semaine 13 : Introduction à Node.js et Express.js

### J1 : JavaScript Côté Serveur - Bonjour, Node.js !

**Objectif(s) du Jour :**
- Comprendre que Node.js permet d'exécuter du JavaScript en dehors du navigateur.
- Découvrir les cas d'usage de Node.js (serveurs web, outils de build, scripts...).
- Utiliser le module `fs` (File System) pour interagir avec les fichiers locaux.
- Créer et exécuter son premier script Node.js.

**Notion Clé : Le Couteau Suisse**
Jusqu'à présent, votre JavaScript était un poisson qui ne pouvait vivre que dans l'aquarium du navigateur (`<script>`). Il avait accès à l'environnement de l'aquarium (le DOM, les fenêtres...).
**Node.js**, c'est donner des poumons à ce poisson et le transformer en un animal amphibie. Il peut maintenant sortir de l'eau et vivre sur la terre ferme (votre ordinateur). Sur terre, il n'a plus accès au DOM, mais il a accès à de nouvelles choses incroyables : il peut lire et écrire des fichiers sur votre disque dur (`fs`), communiquer directement avec le réseau (`http`), et bien plus encore. C'est un couteau suisse qui vous permet d'utiliser JavaScript pour presque n'importe quelle tâche.

---

#### Leçon

##### 1. Qu'est-ce que Node.js ?

Node.js n'est PAS un langage de programmation. C'est un **environnement d'exécution** pour le langage JavaScript, construit sur le moteur V8 de Google Chrome. Il permet simplement de faire tourner du JS sur un serveur, sur votre machine, n'importe où.

##### 2. L'écosystème Node.js

- **REPL (Read-Eval-Print Loop) :** En tapant `node` dans votre terminal, vous ouvrez une console JavaScript interactive, comme celle du navigateur.
- **Exécution de fichiers :** La principale utilisation est de lancer des scripts.
  `node mon-script.js`
- **Modules Intégrés :** Node.js vient avec une bibliothèque de modules puissants, prêts à l'emploi. Le plus connu est `fs` pour le système de fichiers.

##### 3. Le Module `fs` (File System)

Le module `fs` permet de manipuler les fichiers. On l'importe avec la fonction `require()`.

- **Exemple de Code (Lecture et écriture de fichiers) :**
  ```javascript
  // On importe le module 'fs'
  const fs = require('fs');

  // Écrire dans un fichier (méthode synchrone pour la simplicité)
  // Crée le fichier 'message.txt' s'il n'existe pas, sinon l'écrase.
  fs.writeFileSync('message.txt', 'Bonjour, le monde de Node.js !');
  console.log('Le fichier a été écrit.');

  // Lire un fichier
  try {
    const data = fs.readFileSync('message.txt', 'utf8'); // 'utf8' pour lire le texte correctement
    console.log('Contenu du fichier :', data);
  } catch (err) {
    console.error('Erreur lors de la lecture du fichier:', err);
  }
  ```

---

#### Mise en Pratique

1.  Assurez-vous que Node.js est installé sur votre machine (`node -v`).
2.  Créez un nouveau dossier `bootcamp-node`.
3.  Créez un fichier `jour1.js`.
4.  Copiez-collez l'exemple de code ci-dessus dans ce fichier.
5.  Ouvrez un terminal dans le dossier `bootcamp-node` et exécutez la commande : `node jour1.js`.
6.  Observez la console et vérifiez que le fichier `message.txt` a bien été créé avec le bon contenu.

#### Mini-Exercice du Jour

Créez un script `copier.js` qui lit le contenu de `message.txt` et l'écrit dans un nouveau fichier nommé `copie_message.txt`.

#### Synthèse

Vous avez fait vos premiers pas en dehors du navigateur ! Vous savez maintenant que Node.js vous donne des super-pouvoirs pour automatiser des tâches et interagir avec votre système. Demain, nous utiliserons l'un des modules les plus puissants de Node.js, le module `http`, pour créer notre tout premier serveur web.

---

### J2 : Votre Premier Serveur Web - Le Module `http`

**Objectif(s) du Jour :**
- Comprendre le rôle d'un serveur HTTP.
- Utiliser le module `http` de Node.js pour créer un serveur de base.
- Gérer les requêtes entrantes et envoyer des réponses.
- Comprendre les limites du module `http` natif et le besoin d'un framework.

**Notion Clé : Le Standardiste Téléphonique**
Un serveur HTTP, c'est comme un standardiste dans une grande entreprise. Il est assis à son bureau (`localhost`), écoute en permanence sur une ligne téléphonique spécifique (un **port**, ex: `3000`).
Chaque fois qu'un appel arrive (une **requête HTTP**), il décroche. Il regarde le numéro de l'appelant et ce qu'il demande (l'**URL** de la requête). En fonction de la demande, il prépare une réponse (un bout de HTML, du JSON...) et la renvoie à l'appelant. Puis, il raccroche et attend le prochain appel. Notre mission aujourd'hui est de programmer ce standardiste de base.

---

#### Leçon

##### 1. Le Module `http`

C'est le module intégré à Node.js pour tout ce qui concerne le protocole HTTP.

##### 2. Créer un Serveur

- `http.createServer()` : Cette fonction crée un objet serveur. Elle prend en argument une fonction de rappel (callback) qui sera exécutée **à chaque requête entrante**.
- `server.listen()` : Cette méthode dit au serveur de commencer à écouter sur un port et une adresse IP spécifiques.

- **Exemple de Code (Un serveur "Hello World") :**
  ```javascript
  // 1. Importer le module http
  const http = require('http');

  // 2. Définir le port sur lequel le serveur écoutera
  const port = 3000;

  // 3. Créer le serveur
  // La fonction de callback prend deux arguments : la requête (req) et la réponse (res)
  const server = http.createServer((req, res) => {
    // On inspecte la requête pour savoir quoi faire
    console.log(`Requête reçue sur l'URL : ${req.url}`);

    // On prépare la réponse
    res.statusCode = 200; // Code de statut HTTP (200 = OK)
    res.setHeader('Content-Type', 'text/html; charset=utf-8'); // On dit au navigateur qu'on envoie du HTML
    
    // On écrit le corps de la réponse et on la termine
    res.end('<h1>Bonjour depuis mon serveur Node.js !</h1>');
  });

  // 4. Démarrer le serveur
  server.listen(port, () => {
    console.log(`Serveur démarré et à l'écoute sur http://localhost:${port}`);
  });
  ```

---

#### Mise en Pratique

1.  Créez un fichier `jour2.js` dans votre dossier de projet.
2.  Copiez-collez le code du serveur ci-dessus.
3.  Exécutez-le avec `node jour2.js` dans votre terminal.
4.  Ouvrez votre navigateur et allez à l'adresse `http://localhost:3000`. Vous devriez voir votre message.
5.  Regardez le terminal : vous verrez le log de la requête s'afficher.

#### Mini-Exercice du Jour

Modifiez le serveur pour qu'il affiche "Page d'accueil" si l'URL est `/` et "Page à propos" si l'URL est `/about`. Pour toute autre URL, il devrait afficher "Page non trouvée" et renvoyer un code de statut `404`. (Indice : utilisez des `if/else` sur `req.url`).

#### Synthèse

Vous avez créé votre premier serveur web fonctionnel ! C'est une étape immense. Cependant, vous avez sûrement remarqué que gérer les routes avec des `if/else` devient vite un cauchemar. C'est pourquoi des frameworks ont été créés. Demain, nous découvrirons le plus populaire d'entre eux : Express.js.

---

### J3 : Simplifier le Backend - Introduction à Express.js

**Objectif(s) du Jour :**
- Comprendre pourquoi Express.js est le framework de facto pour Node.js.
- Installer Express et créer un serveur équivalent à celui d'hier, mais plus simple.
- Découvrir le concept de "routing" avec Express.
- Créer plusieurs routes pour différentes URL et méthodes HTTP (GET, POST...).

**Notion Clé : Le Réseau Routier Organisé**
Si le module `http` de Node.js est un vaste champ vide où vous devez construire vous-même chaque route et chaque panneau de signalisation, **Express.js** est une ville déjà conçue avec un réseau routier intelligent.
- **Les Routes :** Vous n'avez plus besoin de `if (req.url === '/about')`. Vous déclarez simplement : `app.get('/about', ...)` (quand une requête `GET` arrive sur `/about`, fais ceci).
- **Les Panneaux :** Express gère pour vous une grande partie du travail fastidieux, comme le parsing des requêtes ou le paramétrage des en-têtes de réponse.

---

#### Leçon

##### 1. Installer Express

Express est un paquet NPM. On commence donc par initialiser un projet et l'installer.
- `npm init -y`
- `npm install express`

##### 2. Votre Premier Serveur Express

Le code est beaucoup plus concis et lisible.

- **Exemple de Code (Serveur "Hello World" avec Express) :**
  ```javascript
  // 1. Importer express
  const express = require('express');

  // 2. Créer une application express
  const app = express();
  const port = 3000;

  // 3. Définir une route pour la racine (/)
  // app.get(chemin, callback)
  app.get('/', (req, res) => {
    // Express gère les en-têtes. res.send() est plus intelligent.
    res.send('<h1>Bonjour avec Express !</h1>');
  });

  // 4. Démarrer le serveur
  app.listen(port, () => {
    console.log(`Serveur Express démarré sur http://localhost:${port}`);
  });
  ```

##### 3. Le Routing Express

Express fournit des méthodes pour chaque verbe HTTP : `app.get()`, `app.post()`, `app.put()`, `app.delete()`, etc.

```javascript
// Route pour la page "À propos"
app.get('/about', (req, res) => {
  res.send('Ceci est la page à propos.');
});

// Route pour la soumission d'un formulaire (simulé)
app.post('/contact', (req, res) => {
  res.send('Formulaire de contact reçu !');
});
```

---

#### Mise en Pratique

1.  Dans votre dossier de projet, créez un sous-dossier `jour3-express`.
2.  Dans ce dossier, initialisez un projet NPM et installez Express.
3.  Créez un fichier `server.js` et recréez le serveur "Hello World" avec Express.
4.  Lancez-le avec `node server.js` et vérifiez qu'il fonctionne.
5.  Ajoutez les routes `/about` et `/contact` (en `GET`) et testez-les dans votre navigateur.

#### Mini-Exercice du Jour

En utilisant une application comme Postman ou l'extension "Thunder Client" pour VS Code, testez la route `POST /contact` que vous avez créée. Vous ne pouvez pas le faire depuis la barre d'adresse du navigateur, qui ne fait que des requêtes `GET`.

#### Synthèse

Vous avez découvert la puissance et la simplicité d'Express. La gestion des routes est maintenant claire et organisée. Mais que se passe-t-il si on veut exécuter du code sur *plusieurs* routes, comme vérifier si un utilisateur est connecté ? C'est le rôle des **middlewares**, que nous verrons demain.

---

### J4 : La Chaîne de Montage - Les Middlewares

**Objectif(s) du Jour :**
- Comprendre le concept de middleware en tant que fonction intermédiaire.
- Créer et utiliser un middleware simple pour logger les requêtes.
- Comprendre l'importance de la fonction `next()`.
- Utiliser des middlewares intégrés à Express, comme `express.json()`.

**Notion Clé : La Chaîne de Contrôle à l'Aéroport**
Quand vous prenez l'avion, vous passez par une série de points de contrôle avant d'atteindre votre porte d'embarquement (la **route finale**).
1.  Contrôle 1 : Enregistrement des bagages.
2.  Contrôle 2 : Vérification du passeport.
3.  Contrôle 3 : Passage aux rayons X.
Chaque point de contrôle est un **middleware**. C'est une fonction qui reçoit la requête, fait quelque chose avec (vérifie, modifie, logue...), puis deux choix s'offrent à elle :
- Soit elle vous dit "C'est bon, passez au contrôle suivant" (en appelant `next()`).
- Soit elle trouve un problème et vous arrête (en envoyant une réponse d'erreur).
La requête passe à travers cette chaîne de middlewares jusqu'à atteindre le gestionnaire de route final.

---

#### Leçon

##### 1. Qu'est-ce qu'un Middleware ?

C'est une fonction qui a accès à l'objet requête (`req`), l'objet réponse (`res`), et à la fonction `next` qui permet de passer à la fonction suivante dans la chaîne.

##### 2. Créer un Middleware Personnalisé

- **Exemple de Code (Un logger de requêtes) :**
  ```javascript
  const express = require('express');
  const app = express();
  
  // Création d'un middleware simple
  const loggerMiddleware = (req, res, next) => {
    console.log(`[${new Date().toISOString()}] ${req.method} ${req.url}`);
    next(); // Très important ! Passe la main au middleware suivant ou à la route.
  };

  // On dit à Express d'utiliser ce middleware pour TOUTES les requêtes qui suivent
  app.use(loggerMiddleware);

  app.get('/', (req, res) => {
    res.send('Accueil');
  });

  app.get('/secret', (req, res) => {
    res.send('Page secrète');
  });

  app.listen(3000);
  ```

##### 3. Middlewares Intégrés

Express vient avec des middlewares très utiles.
- **`express.json()` :** Un middleware crucial. Il analyse le corps des requêtes entrantes au format JSON (ex: envoyées par une app Vue) et le rend disponible dans `req.body`.
  `app.use(express.json());`

---

#### Mise en Pratique

1.  Reprenez votre projet Express de la veille.
2.  Implémentez le `loggerMiddleware` de l'exemple ci-dessus.
3.  Lancez le serveur et faites quelques requêtes. Observez votre terminal : chaque requête est maintenant loguée.

#### Mini-Exercice du Jour

Créez un middleware `authMiddleware` qui sera appliqué uniquement à la route `/secret`. Ce middleware vérifiera si un en-tête de requête `Authorization` a la valeur `'motdepasse123'`. Si c'est le cas, il appelle `next()`. Sinon, il renvoie une erreur `403 Forbidden` avec `res.status(403).send('Accès non autorisé')`. (Indice : pour l'appliquer à une seule route, on le passe en argument avant le callback final : `app.get('/secret', authMiddleware, (req, res) => { ... })`).

#### Synthèse

Vous avez découvert le concept le plus puissant et le plus flexible d'Express. Les middlewares sont au cœur de tout ce que vous ferez ensuite : authentification, gestion d'erreurs, parsing de données... Vous êtes prêt à assembler tout cela.

---

### J5 : Projet de la Semaine - Serveur Express Simple

**Objectif(s) du Jour :**
- Mettre en pratique toutes les notions de la semaine (Node, Express, Routing, Middlewares).
- Construire un petit serveur web qui sert différentes réponses sur différentes routes.
- Établir une base de code serveur propre et organisée.

**Notion Clé : Le Standard Téléphonique Amélioré**
Vous reprenez votre rôle de standardiste, mais cette fois, vous êtes équipé d'outils modernes (Express). Votre mission est de construire un standard complet pour une petite entreprise. Il doit avoir :
- Un service d'accueil (`/`).
- Un service d'information (`/about`).
- Un service de réception de messages (`POST /messages`).
- Un système de surveillance qui note chaque appel entrant (un **middleware logger**).
- Un accès sécurisé à un bureau privé (`/admin`).

---

#### PROJET DE LA SEMAINE : Mon Premier Serveur API

Votre mission est de créer un serveur Express simple qui expose plusieurs routes et utilise un middleware.

**Structure et Fonctionnalités Obligatoires :**

1.  **Mise en Place :**
    - Un projet Node.js avec `package.json` et Express installé. Le fichier principal sera `server.js`.

2.  **Middleware :**
    - Implémentez un middleware global (utilisé par `app.use()`) qui logue la méthode HTTP et l'URL de chaque requête entrante dans la console.

3.  **Routes GET :**
    - `GET /` : Doit renvoyer un message de bienvenue simple en HTML (ex: `<h1>Bienvenue sur mon API</h1>`).
    - `GET /api/info` : Doit renvoyer un objet JSON avec des informations statiques, par exemple `{ "appName": "Mon API de Bootcamp", "version": "1.0.0" }`. (Indice : utilisez `res.json(...)`).
    - `GET /api/random` : Doit renvoyer un objet JSON avec un nombre aléatoire, ex: `{ "randomNumber": 42 }`. Le nombre doit être différent à chaque appel.

4.  **Route Protégée :**
    - `GET /api/secret` : Cette route doit être "protégée" par un middleware. Si la requête contient un en-tête `X-Secret-Key` avec la valeur `supersecret`, elle renvoie `{ "message": "Vous avez trouvé le secret !" }`. Sinon, elle renvoie une erreur 401 (Unauthorized) avec un message JSON `{ "error": "Clé secrète manquante ou invalide" }`.

5.  **(Bonus) Route POST :**
    - Ajoutez le middleware `app.use(express.json())`.
    - Créez une route `POST /api/messages`.
    - Quand vous envoyez un corps de requête JSON comme `{ "message": "Bonjour" }` à cette route (avec Postman/Thunder Client), le serveur doit répondre avec un écho, ex: `{ "received": "Bonjour" }`.

**Livrable :** Un dépôt GitHub contenant votre projet de serveur Express. Le `README.md` doit expliquer brièvement comment démarrer le serveur et comment tester chaque route (en précisant les en-têtes ou corps de requête nécessaires).

#### Synthèse Finale de la Semaine

Félicitations ! Vous êtes passé du monde du frontend à celui du backend. Vous avez appris à exécuter du JavaScript côté serveur, à créer un serveur web, à définir des routes et à intercepter des requêtes avec des middlewares. Vous avez construit la fondation sur laquelle reposera toute application full-stack. La semaine prochaine, nous rendrons ce serveur beaucoup plus utile en le connectant à une base de données pour stocker et récupérer des données de manière persistante.