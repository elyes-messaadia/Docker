### Étapes

1. Créer les Fichiers du Jeu
Créez les fichiers index.html, index.php, save.php, et results.json dans un répertoire de votre choix.

2. Créer le Dockerfile
Créez un fichier nommé Dockerfile dans le même répertoire que les fichiers du jeu.

# Utiliser l'image officielle de Nginx avec PHP
FROM nginx:alpine

# Installer PHP
RUN apk add --no-cache php8 \
    && apk add --no-cache php8-fpm \
    && apk add --no-cache php8-json

# Copier les fichiers du jeu dans le répertoire web de Nginx
COPY index.html /usr/share/nginx/html/
COPY index.php /usr/share/nginx/html/
COPY save.php /usr/share/nginx/html/
COPY results.json /usr/share/nginx/html/

# Configurer Nginx pour gérer les fichiers PHP
COPY ./nginx.conf /etc/nginx/conf.d/default.conf

# Exposer le port 80
EXPOSE 80

# Commande pour démarrer Nginx
CMD ["nginx", "-g", "daemon off;"]

3. Créer le Fichier de Configuration Nginx
Créez un fichier nginx.conf pour configurer Nginx afin de gérer les fichiers PHP :

server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        index index.php index.html;
    }

    location ~ \.php$ {
        include fastcgi_params;
        fastcgi_pass 127.0.0.1:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
    }
}
4. Construire l'Image Docker
Ouvrez un terminal dans le répertoire contenant le Dockerfile et les fichiers du jeu.
Exécutez la commande suivante pour construire l'image Docker :

docker build -t tic-tac-toe-game .
5. Créer et Exécuter le Conteneur avec un Volume
Créez et exécutez un conteneur avec un volume nommé game-results pour stocker les résultats :

docker run -d -p 8080:80 --name tic-tac-toe-container -v game-results:/usr/share/nginx/html tic-tac-toe-game
6. Vérifier la Création du Volume
Utilisez la commande suivante pour vérifier que le volume a été créé :

docker volume ls
7. Afficher le Contenu du Conteneur et du Volume
Afficher le contenu du conteneur :

docker exec -it tic-tac-toe-container /bin/sh
Afficher le contenu du volume :

docker run --rm -v game-results:/data alpine ls /data
8. Afficher le Contenu de results.json
Avec une commande :

docker run --rm -v game-results:/data alpine cat /data/results.json
Avec Docker Desktop :
Allez dans l'onglet "Volumes" pour voir les volumes disponibles.
Sélectionnez le volume game-results pour voir son contenu.
9. Jouer au Jeu et Générer des Résultats
Accédez à http://localhost:8080 dans votre navigateur pour jouer au jeu.
Les résultats seront enregistrés dans results.json dans le volume game-results.
10. Arrêter le Conteneur
Utilisez la commande suivante pour arrêter le conteneur :

docker stop tic-tac-toe-container