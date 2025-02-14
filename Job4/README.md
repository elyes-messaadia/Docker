1. Créer le Fichier index.php
Créer le Fichier :

Créez un fichier nommé index.php dans un répertoire de votre choix.

![alt text](images/indexphp.png)

Ajouter le Code PHP :

![alt text](images/phpcode.png)

Ajoutez le code suivant dans le fichier index.php pour afficher les informations du serveur Apache :

<?php phpinfo(); ?>

Cette commande PHP affiche les informations sur le serveur Apache.

2. Créer le Dockerfile

Créer le Fichier Dockerfile :
![alt text](images/dockerfile.png)

Dans le même répertoire que index.php, créez un fichier nommé Dockerfile.

Ajouter les Instructions Docker :
![alt text](images/dockerfile.png)
Ajoutez les instructions suivantes dans le Dockerfile pour configurer un environnement Apache :

# Utiliser l'image officielle de PHP avec Apache
FROM php:apache

# Copier le fichier index.php dans le répertoire du serveur web
COPY index.php /var/www/html/

# Exposer le port 80 du conteneur
EXPOSE 80

3. Construire l'Image Docker
Ouvrir un Terminal :

Ouvrez un terminal dans le répertoire contenant le Dockerfile et le fichier index.php.

Construire l'Image :

Utilisez la commande suivante pour construire l'image Docker :
![alt text](images/docker-build.png)
docker build -t apache-php-info .
Cette commande crée une image Docker nommée apache-php-info.
4. Créer et Lancer le Conteneur
Créer et Lancer le Conteneur :

Utilisez la commande suivante pour créer et lancer un conteneur à partir de l'image apache-php-info, en mappant le port 8080 de votre machine hôte au port 80 du conteneur :

![alt text](images/docker-run.png)

docker run -d -p 8080:80 apache-php-info
Accéder à l'Application :

![alt text](images/localhost.png)

Ouvrez votre navigateur et accédez à http://localhost:8080 pour voir les informations du serveur Apache.


5. Arrêter le Conteneur
Trouver l'ID du Conteneur : ![alt text](images/container-id.png)

Utilisez la commande suivante pour lister les conteneurs en cours d'exécution :

docker ps

![alt text](images/docker-ps.png)

Notez l'ID du conteneur que vous souhaitez arrêter.
Arrêter le Conteneur :
Utilisez la commande suivante pour arrêter le conteneur :

![alt text](images/docker-stop.png)

docker stop <container_id>
Remplacez <container_id> par l'ID du conteneur que vous avez noté.