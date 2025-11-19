# Programme Bootcamp Développeur Web Full-Stack (6 Mois)

## Philosophie Pédagogique

Ce programme est basé sur une approche "learning by doing". Chaque notion théorique est immédiatement mise en pratique à travers des exercices, des mini-projets, puis un projet de module plus conséquent. L'objectif est de construire un portfolio solide et de développer une réelle autonomie. L'accent est mis sur les bonnes pratiques (code propre, Git, tests) dès le début.

## Compétences Transversales (enseignées tout au long du bootcamp)

- **Git & GitHub :** Versioning, branches, pull requests, collaboration.
- **Ligne de commande :** Navigation, manipulation de fichiers, commandes de base.
- **Algorithmique :** Résolution de problèmes, structures de données.
- **Déploiement :** Mettre en ligne un site statique (GitHub Pages, Netlify) et une application full-stack (Heroku, Vercel, etc.).
- **Méthodologie Agile :** Introduction au Scrum (sprints, stand-ups), gestion de projet avec des outils comme Trello ou Jira.
- **Veille technologique :** Apprendre à lire une documentation, utiliser Stack Overflow, suivre les tendances.

---

## Module 1 : Les Fondations du Web - HTML5 & CSS3 (3 Semaines)

### Objectifs Pédagogiques
- Comprendre le fonctionnement d'un site web (client/serveur, HTTP).
- Structurer une page web de manière sémantique avec HTML5.
- Mettre en forme une page web avec CSS3.
- Créer des mises en page complexes et responsives (adaptées à tous les écrans).
- Intégrer une maquette graphique statique en page web.

### Découpage & Notions
- **Semaine 1 : Introduction et HTML5**
  - Notions : Anatomie d'une URL, requêtes HTTP, structure d'un document HTML, balises sémantiques (`<header>`, `<nav>`, `<main>`, `<footer>`, `<article>`, `<section>`), listes, tableaux, formulaires, liens, images.
  - Projet : Créer une page de type "CV en ligne" ou "page de recette" uniquement en HTML, en se concentrant sur la structure sémantique.

- **Semaine 2 : Les bases de CSS3**
  - Notions : Sélecteurs CSS (balise, classe, id), pseudo-classes, modèle de boîte (box model : `margin`, `padding`, `border`), couleurs, typographie (`font-family`, `font-size`), arrière-plans.
  - Projet : Mettre en forme le projet de la semaine 1 en utilisant les notions de base de CSS.

- **Semaine 3 : Mises en page avancées et Responsive Design**
  - Notions : `display` (block, inline, inline-block), Flexbox, CSS Grid, Media Queries, unités relatives (`rem`, `em`, `%`, `vw`/`vh`), transitions et animations simples.
  - Projet : Intégrer une maquette de landing page complexe (fournie au format Figma ou Adobe XD) pour qu'elle soit "pixel perfect" et responsive sur mobile, tablette et desktop.

### Livrables du Module
- Un dépôt GitHub contenant les 3 projets.
- Le projet final (landing page) déployé sur Netlify ou GitHub Pages.

---

## Module 2 : L'interactivité avec JavaScript (5 Semaines)

### Objectifs Pédagogiques
- Maîtriser les fondamentaux de l'algorithmique et du langage JavaScript.
- Manipuler le DOM pour rendre une page web dynamique et interactive.
- Gérer les événements utilisateur (clics, soumission de formulaire, etc.).
- Communiquer avec des serveurs distants via des APIs (Asynchrone, AJAX).
- Comprendre les concepts modernes de JS (ES6+).

### Découpage & Notions
- **Semaine 4 : Les bases de JavaScript**
  - Notions : Variables (`let`, `const`), types de données, opérateurs, conditions (`if/else`, `switch`), boucles (`for`, `while`).
  - Projet : Créer un petit jeu du "Plus ou Moins" dans la console.

- **Semaine 5 : Fonctions, Tableaux et Objets**
  - Notions : Déclaration de fonctions, portée (scope), tableaux (méthodes `map`, `filter`, `reduce`), objets littéraux.
  - Projet : Un gestionnaire de contacts simple en console (ajouter, lister, supprimer).

- **Semaine 6 : JavaScript dans le navigateur : le DOM**
  - Notions : Sélection d'éléments (`querySelector`, `getElementById`), modification du contenu et du style, création et suppression d'éléments, gestion des événements (`addEventListener`).
  - Projet : Une "To-Do List" interactive : ajouter, supprimer et marquer des tâches comme terminées.

- **Semaine 7 : JavaScript Asynchrone et APIs**
  - Notions : Callbacks, Promesses, `async/await`, l'API `fetch()` pour faire des requêtes HTTP, manipulation de données JSON.
  - Projet : Une application météo qui récupère et affiche les données d'une API publique (ex: OpenWeatherMap) en fonction de la ville saisie par l'utilisateur.

- **Semaine 8 : Outils et Bonnes Pratiques**
  - Notions : Introduction à NPM/Yarn, organisation du code en modules (import/export), utilisation de `linters` (ESLint) et de `formatters` (Prettier).
  - Projet : Refactoriser les projets précédents en modules et mettre en place les outils de qualité de code.

### Livrables du Module
- Les projets (To-Do List, App Météo) fonctionnels et déployés.
- Dépôts GitHub propres avec des commits clairs.

---

## Module 3 : Framework Frontend - Vue.js (4 Semaines)

### Objectifs Pédagogiques
- Comprendre les avantages d'un framework frontend (réactivité, composants).
- Construire des applications web monopages (SPA - Single Page Application).
- Maîtriser l'architecture à base de composants.
- Gérer l'état de l'application (state management).
- Gérer le routage côté client.

### Découpage & Notions
- **Semaine 9 : Les fondamentaux de Vue.js**
  - Notions : Instance Vue, directives (`v-if`, `v-for`, `v-bind`, `v-on`), données réactives, méthodes, propriétés calculées (computed properties).
  - Projet : Re-créer la "To-Do List" en utilisant Vue.js.

- **Semaine 10 : Les composants**
  - Notions : Architecture par composants, communication parent-enfant (props & events), slots pour la flexibilité.
  - Projet : Créer une bibliothèque de composants UI réutilisables (bouton, carte, modal).

- **Semaine 11 : Le Routage avec Vue Router**
  - Notions : Mise en place de Vue Router, définition des routes, navigation programmatique, paramètres de route.
  - Projet : Construire le squelette d'une application multi-pages (Accueil, À propos, Contact) avec un système de navigation.

- **Semaine 12 : State Management et API**
  - Notions : Gestion d'état centralisée avec Pinia (le standard actuel), interaction avec une API REST depuis une application Vue.js (ex: avec Axios).
  - Projet : Créer un frontend de blog qui récupère les articles depuis une fausse API (ex: JSONPlaceholder) et les affiche. Mettre en place une page de détail pour chaque article.

### Livrables du Module
- Une SPA (Single Page Application) complète et fonctionnelle, déployée sur Netlify/Vercel.
- Le code source de l'application sur GitHub, structuré en composants.

---

## Module 4 : Le Backend avec Node.js & Express (4 Semaines)

### Objectifs Pédagogiques
- Comprendre l'environnement d'exécution Node.js.
- Créer un serveur web et une API RESTful avec le framework Express.js.
- Se connecter à une base de données (NoSQL avec MongoDB).
- Mettre en place un système d'authentification et de gestion des utilisateurs.
- Sécuriser une API.

### Découpage & Notions
- **Semaine 13 : Introduction à Node.js et Express.js**
  - Notions : Écosystème Node.js, modules, NPM, création d'un serveur simple, introduction à Express, le principe du routing et des middlewares.
  - Projet : Créer un serveur "Hello World" avec Express et définir quelques routes simples.

- **Semaine 14 : API RESTful et Bases de Données NoSQL**
  - Notions : Principes REST, verbes HTTP, architecture MVC (Modèle-Vue-Contrôleur), introduction à MongoDB, schémas de données avec Mongoose.
  - Projet : Créer une API RESTful complète pour un blog (CRUD pour les articles).

- **Semaine 15 : Authentification et gestion des utilisateurs**
  - Notions : Hachage de mots de passe (bcrypt), création de comptes utilisateurs, système de connexion, authentification par jeton (JWT - JSON Web Token).
  - Projet : Ajouter la gestion des utilisateurs et la connexion à l'API du blog.

- **Semaine 16 : Sécurité et déploiement**
  - Notions : Protection des routes, validation des données d'entrée, gestion des erreurs, variables d'environnement (`.env`), déploiement de l'API (Heroku, Render).
  - Projet : **Connecter le frontend Vue.js (Module 3) à cette nouvelle API backend.** C'est le premier projet full-stack !

### Livrables du Module
- Une API RESTful documentée (avec Postman ou Swagger) et déployée.
- Un projet full-stack (MEVN : MongoDB, Express, Vue, Node) fonctionnel.

---

## Module 5 : Le Backend avec PHP & Laravel (4 Semaines)

### Objectifs Pédagogiques
- Apprendre les bases d'un second langage backend majeur : PHP.
- Comprendre le pattern MVC dans un contexte différent.
- Maîtriser un framework "tout-en-un" puissant : Laravel.
- Utiliser un ORM (Eloquent) pour interagir avec une base de données SQL (MySQL/PostgreSQL).
- Créer des applications web complètes avec rendu côté serveur (Blade).

### Découpage & Notions
- **Semaine 17 : Les fondamentaux de PHP**
  - Notions : Syntaxe, variables, tableaux, fonctions, superglobales (`$_GET`, `$_POST`, `$_SESSION`), introduction à la POO (Programmation Orientée Objet) en PHP.
  - Projet : Créer un petit site dynamique avec plusieurs pages (ex: un formulaire de contact qui envoie un email).

- **Semaine 18 : Introduction à Laravel**
  - Notions : Installation (Composer, Artisan CLI), structure d'un projet Laravel, routing, contrôleurs, vues avec le moteur de template Blade.
  - Projet : Recréer le site dynamique simple de la semaine 17 avec Laravel.

- **Semaine 19 : Bases de données avec Eloquent ORM**
  - Notions : Migrations de base de données, modèles Eloquent, relations (One-to-Many, Many-to-Many), opérations CRUD avec l'ORM.
  - Projet : Développer le backend d'un forum simple (utilisateurs, sujets, messages) avec gestion de la base de données.

- **Semaine 20 : Fonctionnalités avancées de Laravel**
  - Notions : Système d'authentification intégré (Breeze/Jetstream), middlewares, validation de formulaires, création d'API routes.
  - Projet : Finaliser le forum en ajoutant l'authentification et en créant quelques points d'API pour une future interaction avec un client riche.

### Livrables du Module
- Une application web complète développée avec Laravel et déployée.
- Un dépôt GitHub montrant la maîtrise du framework.

---

## Module 6 : Projet Final & Professionnalisation (4 Semaines)

### Objectifs Pédagogiques
- Synthétiser toutes les compétences acquises dans un projet d'envergure.
- Travailler en mode projet, en simulant des conditions d'entreprise (agilité, deadlines).
- Créer un projet "portfolio-killer" démontrant une expertise full-stack.
- Préparer sa recherche d'emploi.

### Découpage & Notions
- **Semaine 21 : Conception et planification**
  - Activités : Choix du projet final (e-commerce, réseau social, outil de gestion...), définition du MVP (Minimum Viable Product), création du backlog, conception de la base de données, choix de la stack technique (Vue/Node ou Vue/Laravel).

- **Semaines 22-23 : Développement en mode Sprint**
  - Activités : Développement intensif du projet. Mise en place de "daily stand-ups" pour suivre l'avancement. Sessions de "pair programming". Revues de code par les instructeurs.

- **Semaine 24 : Finalisation, Déploiement & Préparation à l'emploi**
  - Activités : Débogage, tests, déploiement de l'application finale.
  - Ateliers : Optimisation du CV et du profil LinkedIn, préparation aux entretiens techniques (tests d'algorithmique, questions sur les projets), simulation d'entretiens. Présentation finale des projets.

### Livrables du Module
- Une application full-stack complexe, live et fonctionnelle.
- Un README.md professionnel sur GitHub décrivant le projet, les choix techniques et comment l'installer.
- Un portfolio en ligne à jour.
- Un CV et un profil LinkedIn prêts pour la recherche d'emploi.

---

## Niveau Attendu à la fin de la Phase Bootcamp

À l'issue de ces 6 mois, l'étudiant sera un **Développeur Web Full-Stack Junior**. Il sera capable de :

- **Concevoir, développer et déployer** une application web complète de A à Z.
- **Maîtriser** à la fois un écosystème JavaScript (Vue.js/Node.js) et un écosystème PHP (Laravel), ce qui lui confère une grande polyvalence.
- **S'intégrer** dans une équipe de développement en comprenant les outils (Git) et les méthodes (Agile) de travail modernes.
- **Apprendre de nouvelles technologies** de manière autonome en s'appuyant sur ses solides fondamentaux.
- **Communiquer** efficacement sur des sujets techniques et justifier ses choix d'architecture.

Il sera prêt à postuler à des offres d'emploi pour des postes de Développeur Frontend, Backend ou Full-Stack Junior.