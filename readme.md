# VitalSync – DevOps Project

## 📌 Description du projet

VitalSync est une application de suivi médical et sportif composée de trois services :
•	Un back-end en Node.js (API REST)
•	Un front-end statique servi par Nginx
•	Une base de données PostgreSQL

L’objectif du projet est de mettre en place une chaîne DevOps complète avec :
•	conteneurisation Docker
•	orchestration avec Docker Compose
•	pipeline CI/CD
•	début de configuration Kubernetes



## 🏗️ Architecture

L’architecture est basée sur des conteneurs :
•	Le front-end communique avec le back-end via /api
•	Le back-end communique avec la base PostgreSQL
•	Tous les services sont isolés dans un réseau Docker

## Schéma simplifié (Mermaid)
``` mermaid
graph TD
    User --> Frontend
    Frontend -->|/api| Backend
    Backend --> Database
```

## ⚙️ Prérequis

Pour lancer le projet en local :
•	Docker (>= 20.x)
•	Docker Compose
•	Node.js (>= 18) (optionnel pour tests locaux)
•	Git

▶️ Lancer le projet

Cloner le dépôt :
```bash
git clone https://github.com/elioott/vitalsync.git
cd vitalsync
```

Créer le fichier .env à partir de l’exemple :
```bash
cp .env.example .env
```

Lancer l’application :
```bash
docker compose up --build
```

Accès :
•	Front-end : http://localhost
•	Back-end : http://localhost:3000/health


## 🔁 Pipeline CI/CD

La pipeline est configurée avec GitHub Actions.

Elle contient 3 étapes principales :
1.	Tests et lint
•	Installation des dépendances
•	Exécution des tests Jest
•	Vérification du code avec ESLint
2.	Build Docker
•	Création des images backend et frontend
•	Tag avec le SHA du commit
•	Push vers Docker Hub
3.	Déploiement (staging)
•	Lancement avec docker-compose
•	Vérification via un health check sur /health

Si le health check échoue, la pipeline s’arrête.



## 🛠️ Choix techniques
•	Docker : permet d’isoler les services et simplifie le déploiement
•	Docker Compose : facile pour orchestrer plusieurs conteneurs en local
•	Node.js / Express : rapide pour créer une API simple
•	Nginx : performant pour servir le front-end
•	PostgreSQL : base de données relationnelle fiable
•	GitHub Actions : simple à configurer et intégré au repo
•	Docker Hub : utilisé comme registry pour les images

Ces choix ont été faits pour leur simplicité et leur compatibilité avec un environnement de développement étudiant.



## 🔐 Sécurité
•	Les variables sensibles sont stockées dans .env
•	Les secrets ne sont pas versionnés
•	Utilisation de Docker pour limiter l’exposition du système



## 📌 Remarques

Ce projet est une version simplifiée à but pédagogique.
Certaines optimisations (monitoring avancé, scaling réel) ne sont pas entièrement implémentées.