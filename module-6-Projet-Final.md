# Module 7 : Du Code à la Carrière - Projet Final & Professionnalisation

## 1. Objectifs Pédagogiques

À la fin de ce module, vous serez capable de :
- Gérer un projet de développement web complet, de l'idée initiale au déploiement.
- Appliquer une méthodologie de travail agile (sprints, backlog, MVP) de manière autonome.
- Synthétiser vos compétences full-stack (frontend et backend) dans un projet unique et personnel.
- Créer un "projet signature" qui deviendra la pièce maîtresse de votre portfolio.
- Rédiger une documentation technique claire et professionnelle (`README.md`).
- Préparer et optimiser tous vos outils de recherche d'emploi (CV, LinkedIn, portfolio).
- Présenter un projet technique de manière convaincante et vous préparer aux entretiens d'embauche.

## 2. Prérequis

- Avoir complété et validé **tous les modules précédents** (HTML, CSS, JS, Vue.js, Node.js, PHP/Laravel).
- Une maîtrise fonctionnelle des outils : Git, GitHub, un éditeur de code, la ligne de commande.
- Être prêt à faire des choix techniques et à les justifier.
- Une forte dose de motivation, d'autonomie et de discipline.

## 3. Résumé du Concept (De l'Apprentissage à la Création)

Jusqu'à présent, vous avez appris à cuisiner : vous savez préparer une sauce, cuire une viande, dresser une assiette. Ce module final n'est pas une nouvelle recette. C'est l'épreuve où **vous devenez le chef de votre propre restaurant**. Vous allez concevoir votre menu (le concept de votre projet), choisir vos meilleurs ingrédients (votre stack technique), gérer votre cuisine (la gestion de projet), et servir un plat mémorable à vos clients (les recruteurs).

Ce module est un pont entre le monde académique et le monde professionnel. Il ne s'agit plus de suivre des instructions, mais de **prendre des décisions**. Vous allez vivre un cycle de développement complet, en commettant des erreurs, en trouvant des solutions et en construisant quelque chose dont vous serez fier. L'objectif n'est pas la perfection, mais de livrer un produit fonctionnel (votre MVP) qui démontre concrètement l'étendue de vos compétences de développeur full-stack. C'est la réponse ultime à la question de l'entretien : "Montrez-moi ce que vous avez construit".

## 4. Plan d’Apprentissage (organisé par semaines)

*   **Semaine 1 : La Fondation - Idéation et Planification**
    *   Choisir un concept de projet
    *   Définir le Minimum Viable Product (MVP)
    *   Choisir sa stack technique (Vue/Node ou Vue/Laravel)
    *   Concevoir le schéma de la base de données
    *   Créer le backlog de fonctionnalités
*   **Semaine 2 : Le Sprint - Développement du Cœur de l'Application**
    *   Mettre en place la structure du projet (frontend et backend)
    *   Implémenter le système d'authentification
    *   Développer les fonctionnalités CRUD de base
    *   Adopter un flux de travail Git professionnel
*   **Semaine 3 : La Consolidation - Fonctionnalités Avancées et Polissage**
    *   Développer les fonctionnalités secondaires
    *   Traquer et corriger les bugs
    *   Améliorer l'interface utilisateur et l'expérience utilisateur (UI/UX)
    *   Commencer la rédaction de la documentation
*   **Semaine 4 : La Vitrine - Déploiement et Préparation à l'Emploi**
    *   Déployer le frontend et le backend
    *   Finaliser le `README.md`
    *   Mettre à jour le CV, le portfolio et le profil LinkedIn
    *   S'entraîner pour les entretiens techniques

## 5. Leçons (portant sur le processus)

### Leçon 1 : Concevoir un Produit Viable (Semaine 1)

Le plus grand piège est de vouloir tout faire. Le succès d'un projet réside dans sa capacité à définir un périmètre réaliste : le **MVP (Minimum Viable Product)**. C'est la version la plus simple de votre produit qui apporte tout de même de la valeur et qui fonctionne. On utilise des "user stories" pour décrire les fonctionnalités du point de vue de l'utilisateur.

- **Exemple de "leçon" simple (User Story) :**
  > En tant que **[type d'utilisateur]**, je veux **[réaliser une action]** afin de **[obtenir un bénéfice]**.
- **Exemple appliqué à un projet de blog :**
  > En tant que **visiteur**, je veux **voir la liste de tous les articles** afin de **choisir lequel lire**.
  > En tant qu'**auteur**, je veux **me connecter à mon compte** afin de **pouvoir écrire de nouveaux articles**.
  > En tant qu'**auteur**, je veux **créer un nouvel article avec un titre et un contenu** afin de **le publier sur le blog**.
  >
  > *Le MVP pourrait être juste ces trois user stories.*

### Leçon 2 : Travailler comme un Pro (Semaine 2)

Le code chaotique mène à l'échec. On adopte un flux de travail Git structuré (Git Flow simplifié). Chaque nouvelle fonctionnalité est développée sur une branche dédiée. Quand elle est terminée, on ouvre une "Pull Request" (PR) pour la fusionner dans la branche principale. Cela permet de garder un historique propre et facilite la collaboration (même avec soi-même !).

- **Exemple de "code" simple (Flux Git) :**
  ```bash
  # 1. Se mettre sur la branche principale et la mettre à jour
  git checkout main
  git pull origin main

  # 2. Créer une nouvelle branche pour la fonctionnalité
  git checkout -b feature/user-login

  # 3. Travailler, faire des commits...
  git add .
  git commit -m "feat: add login form"

  # 4. Pousser la branche sur GitHub
  git push origin feature/user-login

  # 5. Aller sur GitHub et créer une Pull Request
  ```
- **Exemple appliqué à un cas réel :**
  Pour votre projet, chaque tâche de votre backlog (Trello/Notion) correspondra à une branche. Par exemple, la tâche "Créer la page de connexion" se fera sur la branche `feature/login-page`.

### Leçon 3 : L'Art du Débogage (Semaine 3)

Un développeur passe plus de temps à déboguer qu'à écrire du code neuf. Il faut apprendre à lire les messages d'erreur, à utiliser les outils du navigateur (`console`, `network`, `debugger`), et à inspecter les logs du serveur. La méthode du "canard en caoutchouc" (expliquer son code ligne par ligne à un objet inanimé) est surprenamment efficace.

- **Exemple de "code" simple (débogage) :**
  *JavaScript (Frontend)*
  ```javascript
  // Ne pas faire ça : console.log("ça marche pas")
  // Faire ça :
  console.log('Données reçues de l'API :', data); 
  // Permet de voir la structure exacte de ce que vous recevez.
  ```
  *Node.js (Backend)*
  ```javascript
  console.log('Requête reçue sur /api/users avec le body :', req.body);
  // Permet de vérifier que les données envoyées par le client sont correctes.
  ```
- **Exemple appliqué à un cas réel :**
  Votre formulaire de connexion ne fonctionne pas.
  1.  **Frontend :** Vérifiez l'onglet `Network` pour voir si la requête part bien vers le serveur. Quel est le code de statut de la réponse (200, 400, 500) ?
  2.  **Backend :** Mettez un `console.log` au début de votre contrôleur de connexion pour voir si la requête arrive. Affichez le `req.body` pour vérifier les données reçues. Lisez les logs de votre serveur.

### Leçon 4 : Mettre en Ligne et se Mettre en Vente (Semaine 4)

Un projet qui tourne uniquement sur votre machine n'existe pas pour un recruteur. Le déploiement est l'étape finale. Le `README.md` est la porte d'entrée de votre projet pour les autres développeurs. Votre CV et votre profil LinkedIn sont votre porte d'entrée vers les entreprises.

- **Exemple de "code" simple (Structure d'un bon `README.md`) :**
  ```markdown
  # Titre du Projet
  
  Une courte description (1-2 phrases) de ce que fait le projet.
  
  ## Démo Live
  
  [Lien vers votre application déployée]
  
  ## Fonctionnalités
  
  - Inscription et connexion des utilisateurs
  - Création/Modification/Suppression de ...
  - ...
  
  ## Stack Technique
  
  **Frontend :** Vue.js, Pinia, Vue Router, ...
  **Backend :** Node.js, Express, MongoDB, ...
  
  ## Installation
  
  Instructions pour lancer le projet en local...
  ```
- **Exemple appliqué à un cas réel :**
  Mettez à jour la section "Projets" de votre CV. Au lieu de "Projet de bootcamp", écrivez : "**Nom de votre Projet** - Application web full-stack de [type d'application]. Conception et développement d'une API RESTful avec [backend] et d'une SPA avec [frontend]. Implémentation de [fonctionnalité clé 1] et [fonctionnalité clé 2]. Déploiement sur [plateforme]."

## 6. Exercices Pratiques (axés sur le processus)

- **Niveau Débutant : Le Pitch de Projet**
  Rédigez un paragraphe décrivant trois idées de projet final. Pour chacune, décrivez le concept, l'utilisateur cible et la fonctionnalité principale. Choisissez-en une et justifiez votre choix.

- **Niveau Intermédiaire : Le Backlog du MVP**
  Créez un tableau sur Trello, Notion ou GitHub Projects pour votre projet. Créez des cartes (tâches) pour chaque fonctionnalité de votre MVP, en utilisant le format "user story". Organisez-les en colonnes "À faire", "En cours", "Terminé".

- **Niveau Avancé : Le Test Technique Blanc**
  Enregistrez-vous en train d'expliquer une partie complexe de votre code pendant 5 minutes, comme si vous étiez en entretien. Regardez l'enregistrement : êtes-vous clair ? Précis ? Confiant ? C'est un excellent exercice pour préparer les entretiens.

## 7. Mini-projet Guidé : La Semaine 1 de votre Projet Final

Le "mini-projet guidé" de ce module est de vous accompagner pas à pas dans la phase la plus critique : la planification.

1.  **Étape 1 : Choisir votre idée.** Listez vos passions, vos problèmes quotidiens. Un bon projet résout un problème, même petit. (Ex: un gestionnaire de recettes, un tracker d'habitudes, un mini-clone de Twitter...).
2.  **Étape 2 : Définir le MVP.** Prenez votre idée et réduisez-la à son essence la plus pure. Qu'est-ce que l'application DOIT faire pour être utilisable ? Listez 3 à 5 fonctionnalités maximum.
3.  **Étape 3 : Choisir votre stack.** Backend en Node.js/Express ou en PHP/Laravel ? Vous avez appris les deux, choisissez celle avec laquelle vous vous sentez le plus à l'aise ou que vous souhaitez approfondir.
4.  **Étape 4 : Modéliser les données.** Prenez une feuille de papier ou un outil en ligne et dessinez les "boîtes" (vos modèles : User, Post, Comment...) et les flèches entre elles (les relations : un User a plusieurs Posts).
5.  **Étape 5 : Mettre en place l'environnement.** Créez votre dépôt sur GitHub. Initialisez vos projets frontend (Vite) et backend (Express/Laravel).

## 8. Projet Final Non Guidé : Votre Projet Signature

C'est votre épreuve de chef-d'œuvre. Vous avez 4 semaines pour transformer votre idée en une application web full-stack fonctionnelle et déployée.

**Livrables :**
1.  **Une application web full-stack déployée** et accessible via une URL publique.
2.  **Un dépôt GitHub professionnel** contenant le code source du frontend et du backend, avec un historique de commits clairs.
3.  **Un `README.md` exceptionnel** qui "vend" votre projet, explique ses fonctionnalités et comment l'installer.
4.  **Un portfolio personnel mis à jour** (ex: une page GitHub Pages ou Netlify) qui présente ce projet en premier.
5.  **Un CV et un profil LinkedIn actualisés** qui mettent en valeur ce projet et les compétences utilisées.

Le choix du sujet est libre, mais il doit être suffisamment complexe pour mettre en œuvre une authentification, des opérations CRUD, et des relations entre plusieurs modèles de données.

## 9. Critères d'Évaluation

- **Qualité Technique (40%) :** Le code est-il propre, sécurisé et performant ? L'architecture est-elle cohérente ? Le projet est-il sans bugs majeurs ?
- **Complétude et Fonctionnalité (30%) :** Le MVP défini est-il entièrement fonctionnel ? L'application est-elle déployée et accessible ?
- **Gestion de Projet et Qualité du Dépôt (15%) :** Le flux de travail Git a-t-il été respecté ? Le `README.md` est-il complet et professionnel ?
- **Présentation et Matériaux Professionnels (15%) :** La présentation orale du projet est-elle claire et convaincante ? Le CV et LinkedIn sont-ils prêts pour la recherche d'emploi ?

## 10. Ressources Complémentaires Fiables

- **Pour la gestion de projet :**
  - [Trello](https://trello.com/), [Notion](https://www.notion.so/), [GitHub Projects](https://github.com/features/project-management/)
- **Pour l'inspiration de design :**
  - [Dribbble](https://dribbble.com/), [Behance](https://www.behance.net/)
- **Pour le déploiement :**
  - Frontend : [Netlify](https://www.netlify.com/), [Vercel](https://vercel.com/)
  - Backend : [Render](https://render.com/), [Heroku](https://www.heroku.com/)
- **Pour la préparation aux entretiens :**
  - [The Tech Resume (Gergely Orosz)](https://www.thetechresume.com/) : Des conseils de haut niveau pour les CV tech.
  - [LeetCode](https://leetcode.com/) : Pour s'entraîner sur des problèmes d'algorithmique (à commencer doucement).
  - [Roadmap.sh](https://roadmap.sh/) : Pour avoir des vues d'ensemble sur les compétences attendues pour différents postes.