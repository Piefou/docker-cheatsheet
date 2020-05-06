# docker-cheatsheet

### Lancement d'un container à partir d'une image

`docker container run [opt] (image:tag) [command] [args]` Lance un container à partir d'une image

* `-it` avec shell interactif. Ctrl+P + Ctrl+Q pour sortir d'un terminal
* `-d` en arrière-plan
* `-p [hote:container]` mappe un port du container sur l'hôte
* `-P` mapping automatique des ports
* `-v [hote:container:ro]` relie un volume du container à l'hôte, ':ro' pour read-only. Ex : -v /var/path:/data/path:ro
* `--name` nomme le container
* `--memory` limite l'allocation mémoire. Ex : --memory 256m
* `--cpus` limite l'allocation cpu ; Décimal < 1 : pourcentage du nombre de cpus disponibles ; Entier >= 1 : nombre de cpus. Ex : --cpus 2, --cpus 0.5
* `--rm` supprime le filesystem du container une fois terminé
* `--user` spécifie l'utilisateur à utiliser
* `--restart=on-failure` redémarrage automatique du container
* `--network [reseau]` indique le réseau par défaut sur lequel se connecter

### Gestion des réseaux

`docker network ls` Liste les réseaux disponibles

`docker network create (reseau)` Créer un réseau

`docker network connect (reseau) (container)` Connecte un container à un réseau

### Construction d'une image

`docker image build [opt] (path | url | -)` Construit une image à partir d'un Dockerfile

* `-t (image:tag)` avec un tag spécifique

`docker image pull (image:tag)` Récupère une image du dépôt

`docker image push (image:tag)` Envoie une image sur le dépôt

`docker image ls` Liste les images récupérées

`docker image rm (image:tag)` Supprime une image en local

`docker commit [opt] container (image:tag)` Sauvegarde l'état actuel d'un container dans une image

`docker tag (image:tag) (repo/image:tag)` Créé un nouveau tag avec namespace pour déposer l'image sur le dépôt

`docker search (critere)` Recherche sur le dépôt une image à partir de mots-clés

### Administration des containers

`docker container ls [opt]` Liste les containers en cours d'exécution

* `-q` indique seulement les id
* `-a` liste aussi les containers arrêtés

`docker container logs [opt] (container)` Indique les logs d'un container

* `-f` avec suivi

`docker container inspect [opt] (container)` Affiche les caractéristiques d'un container (JSON)

* `-f [pattern]` Indique une part de l'arbre JSON via GoTemplate. Ex : -f '{{ .Name }}'

`docker container exec -it (container) /bin/sh` Lance un shell interactif dans le container

`docker container (start | stop | rm | kill) [opt] (container)`

* `-f` force les container en cours d'exécution
* container : id/nom d'un container, ou liste d'ids via $(docker container -q)

### Dockerfile

FROM image:tag [as alias]

COPY [--from=alias] : copie un fichier

ADD : copie un fichier, peut télécharger via une URL, désarchive automatiquement les .tar.gz

VOLUME : persiste un dossier sur l'hôte

USER :

HEALTHCHECK :

### Misc

`docker run --net=host --ipc=host --uts=host --pid=host -it --security-opt=seccomp=unconfined --privileged --rm -v /:/host alpine /bin/sh` Depuis Windows, pour se connecter à la VM hébergeant le daemon Docker
