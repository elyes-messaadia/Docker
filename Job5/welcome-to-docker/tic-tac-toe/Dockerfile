# Utiliser l'image officielle de Nginx
FROM nginx:alpine

# Installer PHP et les extensions nécessaires
RUN apk add --no-cache php82 php82-fpm php82-json

# Copier les fichiers du jeu dans le répertoire de Nginx
COPY index.html /usr/share/nginx/html/index.html
COPY save.php /usr/share/nginx/html/save.php
COPY results.json /usr/share/nginx/html/results.json

# Créer un volume pour stocker les résultats
VOLUME /usr/share/nginx/html

# Exposer le port 80
EXPOSE 80
