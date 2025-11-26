# Lab 4 : Version Control, Build Systems, and Automated Testing (DevOps Data for SWE)

Ce dépôt contient l'implémentation du Lab 4, un exercice pratique visant à consolider les compétences fondamentales en matière de gestion de version, de systèmes de build automatisés, et de tests intégrés dans un pipeline DevOps.

## Objectifs du Laboratoire

Les principaux objectifs de ce lab étaient de maîtriser les outils et pratiques suivants :

* **Version Control & Collaboration :** Utilisation avancée de Git (branching, merging) et collaboration via GitHub (Pull Requests, gestion des remotes).
* **Build System (NPM) :** Configuration de scripts NPM pour automatiser les tâches courantes (démarrage, conteneurisation).
* **Containerization :** Création d'un Dockerfile pour conteneuriser une application Node.js.
* **Automated Testing :** Implémentation de tests unitaires et d'intégration (Jest/SuperTest) pour l'application, et de tests d'infrastructure (OpenTofu) pour valider le code IaC.

## 🛠️ Stack Technique

| Catégorie | Outil / Technologie | Rôle |
| :--- | :--- | :--- |
| **Version Control** | Git, GitHub | Gestion du code source et collaboration. |
| **Backend** | Node.js, Express.js | API REST simple pour l'application. |
| **Build / Automation** | NPM | Système de gestion de dépendances et d'exécution de scripts. |
| **Conteneurisation** | Docker | Packaging et isolation de l'application. |
| **Tests Applicatifs** | Jest, SuperTest | Framework de test et bibliothèque de requêtes HTTP. |
| **Tests Infrastructure** | OpenTofu | Validation du comportement de l'infrastructure déployée. |

## Structure du Projet Clé

Le projet est principalement structuré autour du dossier de l'application Node.js et des configurations de l'infrastructure :

. ├── td4/ │ ├── scripts/ │ │ ├── sample-app/ # Contient l'application Node.js (app.js, server.js) │ │ │ ├── app.js # Logique d'application (exports l'instance Express) │ │ │ ├── server.js # Point d'entrée pour démarrer le serveur │ │ │ ├── app.test.js # Tests d'intégration (Jest/SuperTest) │ │ │ ├── package.json # Scripts NPM et dépendances │ │ │ └── Dockerfile │ │ └── tofu/ # Contient les configurations OpenTofu │ │ ├── live/ # Environnements de déploiement (e.g., lambda-sample) │ │ │ └── lambda-sample/ │ │ │ └── deploy.tftest.hcl # Fichier de test d'infrastructure │ │ └── modules/ │ │ └── test-endpoint # Module OpenTofu pour effectuer des requêtes HTTP └── README.md


## Commandes d'Exécution et d'Automatisation

Les scripts NPM ont été définis pour simplifier le flux de travail.

### Application Locale

1.  **Installation des dépendances :**
    ```bash
    npm install
    ```
2.  **Démarrer l'application (en local) :**
    ```bash
    npm start
    # Accès à http://localhost:8080
    ```

### Tests Automatisés

1.  **Exécuter les tests applicatifs (Jest/SuperTest) :**
    ```bash
    npm test
    ```

2.  **Construire et Tagger l'image Docker :**
    Cette commande exécute le script `build-docker-image.sh`.
    ```bash
    npm run dockerize
    ```

3.  **Exécuter les tests d'infrastructure (OpenTofu) :**
    (Nécessite une configuration AWS et l'initialisation du backend OpenTofu dans le dossier `lambda-sample`)
    ```bash
    cd td4/scripts/tofu/live/lambda-sample
    tofu test
    ```

---

## 📝 Points Clés Retenus

* **Testabilité :** La séparation du code applicatif (`app.js`) et du serveur (`server.js`) est cruciale pour permettre des tests isolés et rapides, car SuperTest peut interroger directement l'instance Express.
* **Contrôle de Qualité IaC :** L'utilisation de `deploy.tftest.hcl` prouve que la validation du code ne s'arrête pas à l'application, mais doit garantir que l'infrastructure déployée répond aux attentes fonctionnelles (ex. : code de réponse HTTP 200).
* **Automatisation NPM :** NPM sert de point de contrôle unique pour toutes les opérations courantes, améliorant la cohérence et l'efficacité du développeur.
