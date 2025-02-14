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
