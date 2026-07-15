# TaskFlow

TaskFlow est une application Spring Boot de gestion de tâches. Elle permet de créer et lister des tâches via une API REST, avec une base PostgreSQL pour le stockage persistant.

## Sommaire

- [Présentation du projet](#présentation-du-projet)
- [Prérequis](#prérequis)
- [Démarrage rapide](#démarrage-rapide)
- [API](#api)
- [Tests](#tests)
- [Structure du projet](#structure-du-projet)
- [Configuration](#configuration)
- [Gestion des branches Git](#gestion-des-branches-git)
- [Workflow recommandé](#workflow-recommandé)
- [Dépannage](#dépannage)

## Présentation du projet

Le projet est structuré autour d’une architecture Spring Boot simple :

- `controller` : expose les endpoints REST
- `service` : contient la logique métier
- `repository` : gère l’accès aux données avec Spring Data JPA
- `entity` : définit les modèles JPA
- `resources` : contient la configuration de l’application et les ressources statiques

## Prérequis

Avant de lancer le projet, assure-toi d’avoir installé :

- Java 21
- Maven (ou utiliser le wrapper `./mvnw`)
- Docker et Docker Compose

## Démarrage rapide

### 1. Démarrer la base de données PostgreSQL

```bash
docker compose up -d
```

Cette commande lance un conteneur PostgreSQL sur le port `5432` avec les variables suivantes :

- base : `taskflow`
- utilisateur : `taskflow`
- mot de passe : `taskflow`

### 2. Lancer l’application

```bash
./mvnw spring-boot:run
```

L’application sera disponible sur :

- http://localhost:8080/

## API

### Endpoints disponibles

- `GET /` : affiche la page d’accueil
- `GET /tasks` : liste toutes les tâches
- `POST /tasks` : crée une nouvelle tâche

### Exemples de requêtes

Lister les tâches :

```bash
curl http://localhost:8080/tasks
```

Créer une tâche :

```bash
curl -X POST http://localhost:8080/tasks \
  -H "Content-Type: application/json" \
  -d '{"title":"Apprendre Spring Boot","description":"Comprendre les bases"}'
```

## Tests

Exécuter la suite de tests :

```bash
./mvnw clean test
```

## Structure du projet

```text
src/
  main/
    java/
      com/taskflow/taskflow/
        controller/
        entity/
        repository/
        service/
        TaskflowApplication.java
        HomeController.java
    resources/
      application.yml
      static/
        index.html
  test/
    java/
      com/taskflow/taskflow/
        TaskflowApplicationTests.java
    resources/
      application.properties
``` 

## Configuration

La configuration principale se trouve dans :

- `src/main/resources/application.yml`

Elle définit :

- le nom de l’application
- la connexion à PostgreSQL
- le port du serveur `8080`
- le mode de mise à jour du schéma JPA

## Gestion des branches Git

Le projet suit une logique simple de branches :

- `main` : branche principale
- `develop` : branche de développement
- `feature/*` : branches de fonctionnalités

### Créer une nouvelle branche

```bash
git checkout -b feature/nom-de-la-branche
```

### Voir les branches

```bash
git branch -a
```

### Pousser une branche sur GitHub

```bash
git push -u origin feature/nom-de-la-branche
```

### Fusionner une branche

Depuis la branche cible :

```bash
git merge feature/nom-de-la-branche
```

### Ouvrir une Pull Request

Une Pull Request permet de proposer des changements issus d’une branche vers une autre branche, généralement `main` ou `develop`, avant leur intégration.

## Workflow recommandé

1. Créer une branche dédiée à la fonctionnalité
2. Développer et tester localement
3. Pousser la branche sur GitHub
4. Ouvrir une Pull Request
5. Valider puis fusionner

## Commandes utiles

```bash
# vérifier l’état du dépôt
git status

# récupérer les dernières modifications

git pull origin main

# voir l’historique
git log --oneline --decorate --graph --all
```

## Dépannage

Si l’application ne démarre pas :

1. Vérifier que Docker est bien lancé :
   ```bash
   docker compose ps
   ```
2. Vérifier que PostgreSQL est accessible :
   ```bash
   docker compose logs postgres
   ```
3. Relancer l’application :
   ```bash
   ./mvnw spring-boot:run
   ```
4. Si les tests échouent, relancer :
   ```bash
   ./mvnw clean test
   ```

## Notes

Le projet contient déjà :

- un endpoint REST `/tasks`
- une page d’accueil à l’URL `/`
- une configuration Docker pour PostgreSQL
- une configuration de test avec H2
