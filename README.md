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

### Construction d'une image

`docker image build [opt] (path | url | -)`

-t (image:tag)

`docker image pull (image:tag)`

`docker image push (image:tag)`

`docker commit [opt] container (image:tag)`
