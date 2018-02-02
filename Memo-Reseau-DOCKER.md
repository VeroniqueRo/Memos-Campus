# Memo Commandes DOCKER
## *Campus Numérique 2018 - Véronique ROUAULT*
#
## Ressources en ligne
* [Documentation Docker](https://docs.docker.com/).
* [Tuto vidéo : Dockerfile](https://www.grafikart.fr/tutoriels/docker/dockerfile-636).
## Qu’est-ce que Docker
Docker est un outil qui peut empaqueter une application et ses dépendances dans un conteneur virtuel, qui pourra être exécuté sur n’importe quel serveur Linux.
## Pourquoi l’utiliser 
Pour éviter les problèmes des dépendances lorqu’on installe un projet. Versions de PHP, librairies particulières... 
Pour éviter de faire tourner plusieurs systèmes d’exploitation gourmants en ressources. 
C’est portable et donc facile à déployer chez un hebergeur.
## Comment ça marche
Ne fonctionne que sur Linux.
Il est donc nécessaire d’utiliser une machine virtuelle propre : `Boot2Docker`

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
Pour créer un container portant le nom `chocapic` et lance une image d’un bash de debian avec le nom choisi
(conterner créé : root@49d756a0f7c2:/#)
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




