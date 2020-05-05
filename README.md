# docker-cheatsheet

### Lancement d'un container à partir d'une image

`docker container run [opt] (image:tag) [command] [args]`

-it : avec shell interactif. Ctrl+P + Ctrl+Q pour sortir d'un terminal.

-d : en arrière-plan

-p [hote:container] : mappe un port du container sur l'hôte

-P : mapping automatique des ports

-v [hote:container:ro] : relie un volume du container à l'hôte, ':ro' pour read-only. Ex : -v /var/path:/data/path:ro

--name : nomme le container

--memory : limite l'allocation mémoire. Ex : --memory 256m

--cpus : limite l'allocation cpu ; Décimal < 1 : pourcentage du nombre de cpus disponibles ; Entier >= 1 : nombre de cpus. Ex : --cpus 2, --cpus 0.5

--rm : supprime le filesystem du container une fois terminé

--user : spécifie l'utilisateur à utiliser

--restart=on-failure : redémarrage automatique du container

### Construction d'une image

`docker image build [opt] (path | url | -)`

-t (image:tag)

`docker image pull (image:tag)`

`docker image push (image:tag)`

`docker commit [opt] container (image:tag)`

### Administration des containers

`docker container ls [opt]`

-q : indique seulement les id

-a : liste aussi les containers arrêtés

`docker container logs [opt] (container)`

-f : avec suivi

`docker container inspect [opt] (container)`

-f [pattern] : Indique une part de l'arbre JSON via GoTemplate. Ex : -f '{{ .Name }}'

`docker container exec -it (container) /bin/sh` Lance un shell interactif dans le container

`docker container (start | stop | rm) [opt] (container)`

-f : force les container en cours d'exécution
container : id/nom d'un container, ou liste d'ids via $(docker container -q)

### Dockerfile

FROM image:tag [as alias]

COPY [--from=alias] : copie un fichier

ADD : copie un fichier, peut télécharger via une URL, désarchive automatiquement les .tar.gz

VOLUME : persiste un dossier sur l'hôte

USER :

HEALTHCHECK :
