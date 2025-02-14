### Introduction
Ce document guide à travers les étapes nécessaires pour configurer, construire et lancer une application web de Tic Tac Toe utilisant Docker. Le projet utilise Nginx et PHP pour servir le jeu et enregistrer les résultats des parties.

## Prérequis

Docker installé sur votre machine
Connaissances de base en utilisation de Docker et en configuration de Docker Compose
Configuration du Projet

## Étape 1: Création des Fichiers du Jeu
Créez les fichiers suivants dans votre répertoire de travail:

index.html : Interface utilisateur du jeu.
index.php : Fichier backend pour le traitement côté serveur.
save.php : Script pour sauvegarder les résultats du jeu dans results.json.
results.json : Fichier pour stocker les résultats du jeu.

## Étape 2: Création du Dockerfile
Structurez le Dockerfile pour utiliser Nginx avec PHP :

dockerfile

# Utilisation de l'image Nginx avec support PHP
FROM nginx:alpine

# Installation de PHP et des extensions nécessaires
RUN apk add --no-cache php8 php8-fpm php8-json

# Copie des fichiers du jeu dans le répertoire de Nginx
COPY index.html index.php save.php results.json /usr/share/nginx/html/

# Ajout de la configuration Nginx pour PHP
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

# Exposition du port 80
EXPOSE 80

# Commande pour démarrer Nginx avec gestion de PHP
CMD ["nginx", "-g", "daemon off;"]

## Étape 3: Utilisation de Docker Compose
Configurez docker-compose.yml pour simplifier le déploiement et la gestion du service:

version: '3.8'
services:
  web:
    build: .
    ports:
      - "8080:80"
    volumes:
      - ./html:/usr/share/nginx/html
      - game-results:/usr/share/nginx/html/results.json
volumes:
  game-results:

## Étape 4: Construction de l'Image Docker
Construisez l'image Docker à partir du Dockerfile :

    docker build -t tic-tac-toe-game .

## Étape 5: Lancement du Conteneur
Démarrez le conteneur avec le volume pour la persistance des résultats :

    docker run -d -p 8080:80 --name tic-tac-toe-container -v game-results:/usr/share/nginx/html/results.json tic-tac-toe-game

## Étape 6: Vérification et Manipulation
Vérification du Volume :

    docker volume ls

Affichage du Contenu du Volume :

    docker run --rm -v game-results:/data alpine cat /data/results.json

## Étape 7: Jouer et Générer des Résultats

Accédez à http://localhost:8080 pour jouer au jeu. Les résultats seront automatiquement enregistrés dans results.json.

## Étape 8: Arrêt et Nettoyage

Arrêtez le conteneur lorsque vous avez terminé :

    docker stop tic-tac-toe-container