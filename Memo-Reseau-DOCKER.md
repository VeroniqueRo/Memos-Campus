# Memo Commandes DOCKER
## *Campus Numérique 2018 - Véronique ROUAULT*
#
## Ressources en ligne
* [Docker librairie sur Github](https://github.com/docker-library)
* [Documentation Docker](https://docs.docker.com/).
* [Tuto vidéo : Dockerfile](https://www.grafikart.fr/tutoriels/docker/dockerfile-636).
* [Introdution à Docker](http://putaindecode.io/fr/articles/docker/)
## Qu’est-ce que Docker
Docker est un outil qui peut empaqueter une application et ses dépendances dans un conteneur virtuel, qui pourra être exécuté sur n’importe quel serveur Linux.
Identique à ```vitual box``` mais 100 à 1000 fois plus rapide sous Linux.
## Pourquoi l’utiliser 
Pour éviter les problèmes des dépendances lorqu’on installe un projet. Versions de PHP, librairies particulières... 
Pour éviter de faire tourner plusieurs systèmes d’exploitation gourmants en ressources. 
C’est portable et donc facile à déployer chez un hebergeur.
## Comment ça marche
Ne fonctionne que sur Linux.
Il est donc nécessaire d’utiliser une machine virtuelle propre : `Boot2Docker` sous Windows.

Le conteneur est basé sur une image comme un template qui met les infos de base
## Accéder à l’entrepôt sur le seveur Hunter
```
veronique.rouault@PC-DG-CAMPUS-25 MINGW64 ~
$ ssh veronique.rouault@51.15.215.183
```
```
docker ps -a
```
Pour voir tous les contener créés même arrêtés
```
docker images
```
Pour créer un container portant le nom `chocapic` avec une machine vituelle utilisant l'image ```debian:jessie``` et lance le bash
(container créé : root@49d756a0f7c2:/#)
```
docker run --name=chocapic_coffee_machine -ti debian:jessie bash
```
Pour mettre en route un container arrêté
```
docker start chocapic
```
Pour entrer dans un container
```
docker attach chocapic
```
On trouve des images pour construire les machines virtuelles sur [Docker Hub](https://hub.docker.com/).

Docker permet de faire tourner les installations de PHP, Apache et MySql séparément sur plusieurs containers construits.
## Comment l'utiliser
### Le docker-compose
[Vidéo docker-compose en 12 minutes](https://www.youtube.com/watch?v=Qw9zlE3t8Ko)

Docker-compose est un outil pour définir et exécuter des applications Docker multi-conteneurs depuis la machine locale.

#### Commandes de docker-compose
```
$ docker-compose --help
Define and run multi-container applications with Docker.

Usage:
  docker-compose [-f <arg>...] [options] [COMMAND] [ARGS...]
  docker-compose -h|--help

Options:
  -f, --file FILE             Specify an alternate compose file (default: docker-compose.yml)
  -p, --project-name NAME     Specify an alternate project name (default: directory name)
  --verbose                   Show more output
  -v, --version               Print version and exit
  -H, --host HOST             Daemon socket to connect to

  --tls                       Use TLS; implied by --tlsverify
  --tlscacert CA_PATH         Trust certs signed only by this CA
  --tlscert CLIENT_CERT_PATH  Path to TLS certificate file
  --tlskey TLS_KEY_PATH       Path to TLS key file
  --tlsverify                 Use TLS and verify the remote
  --skip-hostname-check       Don't check the daemon's hostname against the name specified
                              in the client certificate (for example if your docker host
                              is an IP address)

Commands:
  build              Build or rebuild services
  bundle             Generate a Docker bundle from the Compose file
  config             Validate and view the compose file
  create             Create services
  down               Stop and remove containers, networks, images, and volumes
  events             Receive real time events from containers
  exec               Execute a command in a running container
  help               Get help on a command
  kill               Kill containers
  logs               View output from containers
  pause              Pause services
  port               Print the public port for a port binding
  ps                 List containers
  pull               Pulls service images
  push               Push service images
  restart            Restart services
  rm                 Remove stopped containers
  run                Run a one-off command
  scale              Set number of containers for a service
  start              Start services
  stop               Stop services
  unpause            Unpause services
  up                 Create and start containers
  version            Show the Docker-Compose version information
```
 [Tutoriel sur Github](https://github.com/xataz/Tutoriels/blob/master/Utilisation%20de%20Docker/12.%20Docker%20compose.md)

Example pour construire un container contenant mysql
(```stack.yml``` for mysql)
```php
# Use root/example as user/password credentials
version: '3.1'

services:

  db:
    image: mysql
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: example

  adminer:
    image: adminer
    restart: always
    ports:
      - 8080:8080
```
Pour notre projet, utiliser ```php:7.2-apache``` et ```mysql```

Pour lancer le docker-compose
```
docker-compose up
```
lorsqu'on utilise la commande ```build: .``` dans le docker-compose cela lui indique qu'il doit construire le container à partir d'une "recette" contenue dans le ```dockerfile```
```
build: .
```
### Le dockerfile
Les Dockerfiles sont des fichiers qui permettent de construire une image Docker adaptée à nos besoins, étape par étape comme une `recette`.

[Construire un dockerfile par l'exemple](http://putaindecode.io/fr/articles/docker/dockerfile/)

```
# Image de base
FROM debian:jessie

# Installation de curl avec apt-get
RUN apt-get update \
&& apt-get install -y curl \
&& rm -rf /var/lib/apt/lists/*

# Installation de Node.js à partir du site officiel
RUN curl -LO "https://nodejs.org/dist/v0.12.5/node-v0.12.5-linux-x64.tar.gz" \
&& tar -xzf node-v0.12.5-linux-x64.tar.gz -C /usr/local --strip-components=1 \
&& rm node-v0.12.5-linux-x64.tar.gz

# Ajout du fichier de dépendances package.json
ADD package.json /app/

# Changement du repertoire courant
WORKDIR /app

# Installation des dépendances
RUN npm install

# Ajout des sources
ADD . /app/

# On expose le port 3000
EXPOSE 3000

# On partage un dossier de log
VOLUME /app/log

# On lance le serveur quand on démarre le conteneur
CMD node server.js
```
Les images présentes sur ```docker hub``` sont des ```dokerfile```

Pour conserver les données en local, il est nécessaire de faire un partage avec un répertoire sur le localhost.
### construire une image

