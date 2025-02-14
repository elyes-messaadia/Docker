# Commandes de suppressions pour Docker

**1**

*Un conteneur spécifique* 

    docker rm <container_name>

![alt text](images/docker-rm.png)


**2**

*Plusieurs conteneurs*

    docker container rm

![alt text](images/docker-container-prune.png)


**3**

*Tous les conteneurs arrêtés*

    docker stop $(docker ps -q)

![alt text](<images/docker-stop-(docker ps -q).png>)


**4**

*Forcer la suppression d'un conteneur actif*

    docker container rm

![alt text](images/docker-container-rm.png)

**5**

*Une image spécifique*

    docker rmi <nomimage>

![alt text](images/docker-rmi.png)

**6**

*Plusieurs images*

    docker image rm

![alt text](images/docker-image-rm.png)

**7**

*Toutes les images inutilisées*

    docker image prune

![alt text](images/docker-image-prune.png)

**8**

*Toutes les images utilisées*

    docker image rm

![alt text](images/docker-rmi-f.png)

**9**

*Forcer la suppression d'une image*

    docker rmi -f IMAGE

**10**

*Quel erreur est présente dans les commandes données ci-dessus, donner la correction* 

    docker run -it --rm -p 8088:80 welcome-to-docker

![alt text](images/docker-error.png)






