# Memo Commandes LINUX
## *Campus Numérique 2018 - Véronique ROUAULT*
#

## Ressources en ligne

* [wiki.linux-France.org](http://wiki.linux-france.org/wiki/Les_commandes_fondamentales_de_Linux#Chercher_un_fichier_ou_r.C3.A9pertoire_.28find.2C_locate.2C_which.29).

* [101-commandes-indispensables-sous-linux](https://buzut.fr/101-commandes-indispensables-sous-linux).

### Jeu de piste sous Linux (Debian)

Le système d’exploitation **UNIX/LINUX** est un système Open Source dont les diverses versions (Obuntu, Debian…) sont en évolutions permanentes parallèlement et sont distribuées gratuitement.

Un certains nombres de logiciels « du monde libre » fonctionnent aussi bien sous Windows que sous Linux. Pour les applications web toutes les applications fonctionnent sous les deux environnements.

Pour le jeu de piste, nous nous connectons en ssh sur un serveur Debian situé à Paris *Hunter* pour lequel la seule interaction se fait avec l’interface **Git Bash** en lignes de commandes Linux.

## Commandes de base

### Connexion à un serveur distant :

```
ssh identifiant@adresseIP
```
Exemple de code
```
veronique.rouault@PC-DG-CAMPUS-25 MINGW64 ~
$ ssh veronique.rouault@51.15.215.183
veronique.rouault@51.15.215.183's password:
```
Connection à une autre machine  
NB : Le mot de passe n’apparait pas quand on le saisi

## Navigation dans les fichiers

Copier les fichiers

- Syntaxe
```
cp fichieracopier.txt  fichierdedestination.txt
```
* Utilisation :
copie le fichier fichier1 vers le fichiers2  

Exemple de code
```
cp  fichieracopier.txt  fichierdedestination.txt
```