## Semaine 8 : Outils et Bonnes Pratiques

### J1 : Le Coffre à Outils du Développeur - NPM

**Objectif(s) du Jour :**
- Comprendre le rôle d'un gestionnaire de paquets (NPM/Yarn).
- Savoir initialiser un nouveau projet Node.js avec `npm init`.
- Installer, utiliser et désinstaller des dépendances.
- Comprendre la différence entre dépendances de production et de développement.

**Notion Clé : La Grosse Boîte à Outils**
Imaginez que vous voulez construire une cabane. Vous n'allez pas forger votre propre marteau ou fabriquer vos propres vis. Vous allez au magasin de bricolage pour les acheter. **NPM (Node Package Manager)** est ce gigantesque magasin de bricolage pour les développeurs JavaScript. Il contient des millions d'outils (les "paquets" ou "librairies") créés par d'autres développeurs, que vous pouvez facilement ajouter à votre projet. Le fichier `package.json` est votre liste de courses, qui indique exactement quels outils vous avez choisis.

---

#### Leçon

##### 1. Qu'est-ce que NPM ?

- **NPM** est le gestionnaire de paquets par défaut qui est installé automatiquement avec Node.js.
- Il a deux rôles principaux :
  1.  Un **registre en ligne** (le "magasin") où sont publiés les paquets open-source.
  2.  Un **outil en ligne de commande** (le "chariot") pour installer et gérer ces paquets dans vos projets.

##### 2. Initialiser un Projet : `package.json`

Avant d'installer des paquets, il faut dire à NPM que notre dossier est un projet.
- **Commande : `npm init -y`**
  - `npm init` lance un assistant pour créer le fichier `package.json`.
  - L'option `-y` répond "oui" à toutes les questions et crée un fichier par défaut instantanément.
- Le fichier **`package.json`** est le cœur de votre projet. Il contient :
  - Le nom du projet, sa version, sa description...
  - La liste de toutes ses dépendances.

##### 3. Gérer les Dépendances

- **Installer un paquet : `npm install <nom-du-paquet>`**
  - Exemple : `npm install lodash`
  - Cette commande fait 3 choses :
    1.  Télécharge le paquet depuis le registre NPM.
    2.  Le place dans un dossier nommé `node_modules`.
    3.  Ajoute le paquet comme dépendance dans votre `package.json`.
- **Dépendances de Production vs. Développement (`--save-dev`)**
  - `npm install <paquet>` : Pour les paquets nécessaires au fonctionnement de l'application en production (ex: `vue`, `express`).
  - `npm install <paquet> --save-dev` : Pour les outils nécessaires uniquement pendant le développement (ex: un linter, un formateur, un outil de test). Ils ne seront pas inclus dans le build final.

---

#### Mise en Pratique

1.  Créez un nouveau dossier `bootcamp-outils`.
2.  Ouvrez un terminal dans ce dossier et exécutez la commande `npm init -y`.
3.  Observez le fichier `package.json` qui a été créé.
4.  Installez une librairie simple comme `lodash` : `npm install lodash`. Observez la création du dossier `node_modules` et la modification du `package.json` (section `dependencies`).
5.  Créez un fichier `index.js` et utilisez la librairie :
    ```javascript
    const _ = require('lodash'); // Ancienne syntaxe de module, on verra la nouvelle demain !
    
    const array = [1, 2, 3, 4];
    const shuffledArray = _.shuffle(array);
    
    console.log("Tableau mélangé :", shuffledArray);
    ```
6.  Exécutez le fichier avec Node : `node index.js`.

#### Mini-Exercice du Jour

Installez un autre paquet très simple nommé `cowsay` **en tant que dépendance de développement**. Créez un fichier `test.js` qui l'utilise pour afficher un message amusant dans la console. Regardez votre `package.json` pour vérifier que `cowsay` est bien dans la section `devDependencies`.

#### Synthèse

Vous avez ouvert la porte à un écosystème immense. Savoir gérer des paquets est une compétence non négociable pour un développeur moderne. Demain, nous allons voir comment organiser notre propre code en morceaux logiques et réutilisables grâce aux modules ES6.

---

### J2 : Organiser son Code - Les Modules ES6 (import/export)

**Objectif(s) du Jour :**
- Comprendre l'intérêt de séparer son code en plusieurs fichiers.
- Maîtriser la syntaxe `export` pour exposer des fonctions ou variables.
- Maîtriser la syntaxe `import` pour utiliser du code depuis d'autres fichiers.
- Différencier les exports par défaut des exports nommés.

**Notion Clé : La Bibliothèque de Livres**
Jusqu'à présent, vous avez écrit tout votre code dans un seul grand parchemin. Si le projet grossit, c'est le chaos. Les modules, c'est comme organiser vos connaissances dans une bibliothèque. Chaque livre (`fichier.js`) traite d'un sujet spécifique (gestion du DOM, appels API, calculs...).
- `export` : C'est comme mettre une étiquette "Consultable" sur un chapitre ou une définition précise dans un livre.
- `import` : C'est aller dans un livre pour citer ou utiliser ce chapitre spécifique dans votre propre travail.

---

#### Leçon

##### 1. Pourquoi des Modules ?

- **Organisation :** Chaque fichier a une responsabilité unique.
- **Réutilisabilité :** Une fonction utile (ex: `formatDate`) peut être importée dans plusieurs parties de l'application.
- **Maintenance :** Plus facile de trouver et de corriger un bug dans un petit fichier ciblé que dans un fichier de 2000 lignes.

##### 2. `export` : Rendre le code disponible

- **Export nommé :** Pour exporter plusieurs éléments d'un même fichier.
  ```javascript
  // Fichier: math.js
  export const PI = 3.14;
  export function addition(a, b) {
    return a + b;
  }
  ```
- **Export par défaut :** Il ne peut y en avoir qu'un seul par fichier. C'est l'export "principal".
  ```javascript
  // Fichier: salutation.js
  export default function direBonjour(nom) {
    return `Bonjour, ${nom}`;
  }
  ```

##### 3. `import` : Utiliser le code exporté

- **Importer un export nommé :** On doit utiliser le nom exact, entre accolades.
  ```javascript
  // Fichier: app.js
  import { PI, addition } from './math.js';
  
  console.log(PI); // 3.14
  console.log(addition(2, 3)); // 5
  ```
- **Importer un export par défaut :** On peut lui donner le nom que l'on veut.
  ```javascript
  // Fichier: app.js
  import maFonctionDeSalutation from './salutation.js'; // Le nom 'maFonctionDeSalutation' est arbitraire
  
  console.log(maFonctionDeSalutation('Monde')); // Bonjour, Monde
  ```
**Note importante :** Pour que le navigateur comprenne `import`/`export`, il faut ajouter `type="module"` à la balise script dans le HTML : `<script src="app.js" type="module"></script>`.

---

#### Mise en Pratique

1.  Créez un nouveau dossier pour l'exercice du jour.
2.  Créez trois fichiers : `index.html`, `utils.js` et `main.js`.
3.  Dans `utils.js`, créez et exportez (en export nommé) une fonction qui met la première lettre d'une chaîne en majuscule.
4.  Dans `main.js`, importez cette fonction et utilisez-la pour afficher un message dans la console.
5.  Dans `index.html`, liez votre fichier `main.js` en n'oubliant pas `type="module"`. Ouvrez la page dans le navigateur et vérifiez la console.

#### Mini-Exercice du Jour

Créez un fichier `config.js`. Exportez par défaut un objet contenant des informations de configuration (ex: `{ apiKey: 'ABC-123', siteName: 'Mon App' }`). Importez cet objet dans `main.js` et affichez le nom du site dans la console.

#### Synthèse

Vous venez d'acquérir une compétence fondamentale pour écrire du code JavaScript propre et scalable. Finis les fichiers monolithiques ! Demain, nous allons ajouter un gardien automatique à notre code pour nous assurer qu'il respecte les bonnes pratiques : le linter.

---

### J3 : Le Gardien du Code - Linters (ESLint)

**Objectif(s) du Jour :**
- Comprendre le rôle d'un linter pour la qualité du code.
- Installer et configurer ESLint dans un projet NPM.
- Interpréter les erreurs remontées par ESLint.
- Utiliser la commande de correction automatique.

**Notion Clé : Le Correcteur Orthographique et Grammatical**
Imaginez écrire un livre important. Vous utiliseriez un correcteur pour repérer les fautes de frappe, les erreurs de grammaire ou les phrases mal tournées. **ESLint** est ce correcteur pour votre code. Il analyse votre code sans l'exécuter ("analyse statique") et vous signale les problèmes potentiels, les bugs courants et les entorses aux conventions de style. Il est votre première ligne de défense contre les erreurs bêtes.

---

#### Leçon

##### 1. Qu'est-ce qu'un Linter ?

Un linter est un outil qui analyse le code source pour y détecter :
- **Erreurs potentielles :** Utiliser une variable qui n'a pas été déclarée.
- **Mauvaises pratiques :** Créer une variable qui n'est jamais utilisée.
- **Incohérences de style :** Utiliser des guillemets simples puis des doubles.

##### 2. Installation et Configuration d'ESLint

ESLint est un outil de développement, on l'installe donc avec `--save-dev`.
1.  **Installation :** `npm install eslint --save-dev`
2.  **Configuration :** `npx eslint --init`
    - `npx` est un outil qui exécute des paquets NPM sans les installer globalement.
    - L'assistant vous posera des questions pour générer un fichier de configuration (`.eslintrc.json`) :
      - *How would you like to use ESLint?* -> To check syntax, find problems, and enforce code style.
      - *What type of modules does your project use?* -> JavaScript modules (import/export).
      - *Which framework does your project use?* -> None of these.
      - *Does your project use TypeScript?* -> No.
      - *Where does your code run?* -> Browser.
      - *How would you like to define a style?* -> Use a popular style guide. (Choisir `Standard` ou `Airbnb` est un bon début).
      - *What format do you want your config file to be in?* -> JSON.
      - L'assistant proposera d'installer les dépendances nécessaires. Acceptez.

##### 3. Utilisation

- **Analyser les fichiers :** `npx eslint .` (le `.` signifie "tout le dossier courant").
- **Corriger automatiquement :** `npx eslint . --fix` (corrige tout ce qui peut l'être sans risque).

---

#### Mise en Pratique

1.  Reprenez le projet avec les modules du jour 2.
2.  Assurez-vous d'avoir un `package.json` (`npm init -y` si ce n'est pas fait).
3.  Suivez les étapes d'installation et de configuration d'ESLint ci-dessus.
4.  Exécutez `npx eslint .` sur votre projet. Il est probable qu'il trouve des erreurs (par exemple, si vous avez des `console.log`).
5.  Essayez de corriger une erreur manuellement, puis utilisez `npx eslint . --fix` pour voir la magie opérer.

#### Mini-Exercice du Jour

Créez un fichier `bad-code.js`. Écrivez-y volontairement du code qui enfreint les règles : utilisez `var`, déclarez une variable sans l'utiliser, mettez un point-virgule si votre guide de style les interdit (ou n'en mettez pas s'il les exige). Lancez ESLint sur ce fichier pour voir tous les avertissements.

#### Synthèse

Votre code n'est plus seulement organisé, il est maintenant surveillé par un gardien qui garantit sa qualité et sa cohérence. C'est un grand pas vers un développement professionnel. Mais qu'en est-il du formatage purement esthétique (espaces, retours à la ligne...) ? C'est le rôle de l'outil de demain : Prettier.

---

### J4 : L'Artiste du Code - Formateurs (Prettier)

**Objectif(s) du Jour :**
- Comprendre la différence entre un linter (qualité) et un formateur (style).
- Installer et configurer Prettier.
- L'intégrer avec ESLint pour éviter les conflits.
- Automatiser le formatage du code.

**Notion Clé : L'Architecte d'Intérieur**
Si ESLint est l'inspecteur en bâtiment qui vérifie que les murs sont solides et que l'électricité est aux normes, **Prettier** est l'architecte d'intérieur. Il ne se soucie pas de la *logique* de votre code, mais uniquement de son *apparence*. Il prend votre code et le réécrit pour qu'il suive un style unique et cohérent : la longueur des lignes, l'indentation, l'emplacement des virgules... Fini les débats sur "tabs vs spaces" dans l'équipe, Prettier décide pour tout le monde.

---

#### Leçon

##### 1. Linter vs. Formateur

- **ESLint (Linter) :** S'occupe de la **qualité** du code. Trouve les bugs. *Ex: "Cette variable n'est pas utilisée."*
- **Prettier (Formateur) :** S'occupe du **style** du code. Reformate le code. *Ex: "Cette ligne est trop longue, je la coupe en deux."*

##### 2. Installation et Configuration de Prettier

1.  **Installation :** C'est un outil de développement.
    `npm install prettier --save-dev --save-exact`
    (`--save-exact` est recommandé par Prettier pour éviter les changements de style entre les versions mineures).
2.  **Configuration (optionnel) :** Créez un fichier `.prettierrc.json` pour personnaliser les quelques options disponibles.
    ```json
    {
      "semi": true,
      "singleQuote": true,
      "tabWidth": 2,
      "trailingComma": "es5"
    }
    ```
3.  **Utilisation :**
    - Pour vérifier le formatage : `npx prettier --check .`
    - Pour formater les fichiers : `npx prettier --write .`

##### 3. Faire travailler ESLint et Prettier Ensemble

Ils peuvent entrer en conflit sur des règles de style. La solution est de dire à ESLint : "Ne t'occupe pas des règles de formatage, Prettier s'en charge".
1.  **Installation du paquet de configuration :**
    `npm install eslint-config-prettier --save-dev`
2.  **Mise à jour du fichier `.eslintrc.json` :** Ajoutez `prettier` à la fin du tableau `extends`.
    ```json
    {
      "extends": ["standard", "prettier"] // 'prettier' doit être le dernier
    }
    ```

---

#### Mise en Pratique

1.  Reprenez le projet de la veille, avec ESLint déjà configuré.
2.  Suivez les étapes pour installer Prettier.
3.  Créez un fichier `.prettierrc.json` avec vos préférences.
4.  Installez `eslint-config-prettier` et mettez à jour votre fichier `.eslintrc.json`.
5.  Déformatez volontairement un de vos fichiers JavaScript (ajoutez des espaces, des sauts de ligne...).
6.  Lancez la commande `npx prettier --write .` et admirez le résultat.

#### Mini-Exercice du Jour

Ajoutez des "scripts" à votre `package.json` pour simplifier les commandes.
```json
// dans package.json
"scripts": {
  "lint": "eslint .",
  "lint:fix": "eslint . --fix",
  "format": "prettier --write ."
},
```
Maintenant, vous pouvez simplement lancer `npm run lint` ou `npm run format`. C'est la manière professionnelle de faire.

#### Synthèse

Votre atelier de développement est maintenant complet ! Vous avez un gestionnaire de paquets, une structure de code modulaire, un gardien de la qualité et un artiste du formatage. Vous êtes prêt à travailler de manière propre, cohérente et professionnelle. Demain, nous mettons tout cela en pratique en modernisant un ancien projet.

---

### J5 : Projet de la Semaine - Refactorisation Professionnelle

**Objectif(s) du Jour :**
- Appliquer l'ensemble des outils de la semaine à un projet existant.
- Découper un projet monolithique en modules logiques.
- Mettre en place un workflow de qualité de code (linting, formatting).
- Consolider la compréhension des bonnes pratiques de développement.

**Notion Clé : La Rénovation de la Cuisine**
Vous avez une vieille cuisine (votre projet de la semaine 7) qui est fonctionnelle, mais où tout est en désordre dans un seul grand placard. La mission d'aujourd'hui est de la rénover. Vous allez installer des tiroirs et des placards dédiés (les **modules**), vérifier que toute l'installation électrique et la plomberie sont aux normes (le **linter**), et enfin, vous assurer que toutes les poignées de porte sont alignées et que la peinture est impeccable (le **formateur**). Le résultat sera une cuisine non seulement fonctionnelle, mais aussi propre, organisée et facile à entretenir.

---

#### PROJET DE LA SEMAINE : Refactoriser l'Application Météo

Votre mission est de prendre le code de votre application Météo de la semaine 7 et de le transformer en un projet moderne et professionnel en utilisant tous les outils que vous avez appris cette semaine.

**Étapes et Contraintes Obligatoires :**

1.  **Initialisation du projet :**
    - Créez un nouveau dossier pour le projet.
    - Copiez-y vos fichiers `index.html`, `style.css` et votre fichier JavaScript principal (renommez-le `main.js`).
    - Initialisez un projet NPM avec `npm init -y`.

2.  **Modularisation du Code :**
    - Votre fichier `main.js` doit devenir un simple "chef d'orchestre".
    - Créez au moins deux nouveaux modules :
      - `api.js` : Doit contenir la fonction `getWeatherData` qui fait l'appel `fetch`. Cette fonction doit être exportée.
      - `dom.js` : Doit contenir des fonctions pour interagir avec le DOM. Par exemple, une fonction `updateWeatherInfo(data)` qui prend les données météo et met à jour les éléments HTML. Exportez les fonctions nécessaires.
    - Votre `main.js` importera les fonctions de `api.js` et `dom.js` pour orchestrer la logique (ex: l'écouteur d'événement appellera la fonction de `api.js`, puis passera le résultat à la fonction de `dom.js`).
    - N'oubliez pas de mettre à jour votre balise `<script>` dans le HTML avec `type="module"`.

3.  **Mise en place des Outils :**
    - Installez et configurez **ESLint** avec un guide de style populaire.
    - Installez et configurez **Prettier**.
    - Assurez-vous qu'ESLint et Prettier fonctionnent ensemble sans conflit (`eslint-config-prettier`).
    - Ajoutez des **scripts NPM** (`lint`, `format`) à votre `package.json`.

4.  **Nettoyage Final :**
    - Lancez vos scripts `npm run lint` et `npm run format` pour vous assurer que l'ensemble de votre base de code est propre et cohérent.
    - Il ne doit rester aucune erreur ou avertissement de linter.

**Livrable :** Un dépôt GitHub contenant le projet refactorisé. Le `README.md` doit expliquer brièvement la nouvelle structure et comment utiliser les scripts NPM pour lancer les outils de qualité.

#### Synthèse Finale de la Semaine

Félicitations ! Vous avez fait un bond de géant en termes de professionnalisme. Vous ne savez plus seulement "faire fonctionner" le code, vous savez le faire de manière **propre, organisée, maintenable et collaborative**. Ces compétences sont aussi importantes que la connaissance des algorithmes ou des frameworks, car elles sont le fondement du travail en équipe. La semaine prochaine, vous appliquerez cette rigueur à la découverte de votre premier grand framework frontend : Vue.js.