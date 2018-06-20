# CR - Conférence Technique - ALGORITHMES ET SOCIETE
## *Campus Numérique 2018 - Véronique*
#
## Informations sur la conférence
* **Date** : `25 Janvier 2018`
* **Lieu** : `Totem de la French Tech In The Alps (Festival Transfo)`
* **Titre de la Conférence** : `Algorithmes et Société`
* **Conférencier** : [Patrick Loiseau](https://scholar.google.fr/citations?user=q98gB0AAAAAJ&hl=fr&oi=ao) (Titulaire d'une chaire d'excellence à l'Université Grenoble Alpes)

## Ressources en ligne
* [Site développé par l'auteur](https://adanalyst.mpi-sws.org/)
* [Publication](http://proceedings.mlr.press/v81/speicher18a/speicher18a.pdf)

## Introduction
Le réseau social `Facebook` qui revendique plus de 2 milliards d’utilisateurs mensuels se finance essentiellement grâce à la publicité.

Il permet aux annonceurs de cibler leur publicité pour que celle-ci soit efficace.
C'est pourquoi le réseau social a développé un moyen de récupérer les données personnelles de ses utilisateurs.

Cependant, ce fonctionnement pose un problème au niveau des libertés individuelles.

## Comment ça marche
Pour créer une publicité en ligne sur Facebook, il suffit d'utiliser `Create Add` et n'importe qui peut le faire.
* Le `detail targeting` permet de choisir le pannel que l'on veut atteindre avec des carractéristiques plus ou moins personnelles.

En effet, Facebook référence et conserve 614 attributs sur chaque utlisateurs.

### Comment le réseau récupère-t-il ces attributs ?

* `En enregistrant les actions` de l'utilisateur (clics, avis, like...) sur son compte. 
* En suivant les liens vers les sites visités hors du réseau pendant que l'utilisateur est connecté à son compte.
* En utilisant les données vendues par les `Data Brokers`

	Les Data Brokers sont des entreprise dont l’activité principale est la récupération et la revente de données à des annonceurs ou des prestataires marketing. C'est récupération de données se font par exemple via les cartes de fidélité magasin.

Tout cela constitue les `PII` (Personally Identifiable Information). Les informations d'identification personnelles de chaque individu et pose un problème d'atteinte aux libertés individuelles.

## Les risques majeurs de cette pratique

1. Respect de la vie privée
	
	Facebook donne le `Potential Audience` de chaque utilisateur
	* Le numéro de téléphone d'une personne peut être récupéré avec la connaissance de sa date de naissance.
	* Les Facebook Pixels sont des marqueurs invisibles sur les sites web
	* Facebook donne aux annonceurs le `Potentiel Reach`, c'est à dire le nombre d’utilisateurs qui seront impactés par la campagne de pub. Cela leur permet de savoir qui a un compte Facebook et d'identifier l'utilisateur.

2. Lutter contre la discrimination

Bien que le réseau social ait, depuis 2016, pris la décision de ne plus faire de ciblage par ethnie, le problème n’est pas totalement résolu.
En effet ils peuvent encore filtrer les annonces en fonction des pages que vous aimez : Pour ne pas cibler une ethnie, par exemple les afro-américains, ils sortent de leur cible toutes les personnes qui aiment le gospel (entre autre) et pour ne pas être pris en faute, ils ouvrent leur ciblage à l’ethnie afro-américaine mais en dehors de la zone de prospection.

Exemple concret : une agence immobilière basée à Grenoble ne veut cibler que des personnes blanches dans son annonce. FB peut le faire bien que la loi française l’interdise en excluant de leur cible toutes les personnes qui aiment le gospel à Grenoble et pour ne pas être pris en faute, ils envoient la même annonce à des cibles à Paris mais cette fois en intégrant les personnes qui aiment le gospel.
Ainsi l’annonce de l’agence immobilière ne sera vue que par des blancs dans sa zone de chalandise mais respectera quand même la loi puisqu’elle aura envoyée son annonce à des personnes noires mais à Paris.
III – Transparence :

FB et Twitter ouvrent un peu la porte mais…
Lorsque l’on consulte notre profil FB, par exemple, lorsque l’on voit une annonce, on peut regarder pourquoi nous sommes ciblés.
Transparence mais pas tant que cela. En effet, FB ne communique qu’un seul critère et qui est le plus large possible.
Par exemple : L’annonceur cherche à atteindre des personnes de plus de 25 ans. Très large comme critère.
Les chercheurs ont vu qu’il y avait des critères plus restrictifs mais FB ne le communique que quand il ne peut pas en donner un plus large.
Il ne les communique que quand il ne peut  pas en annoncer d’autres.

En conclusion, les réseaux sociaux veulent passer comme message que les utilisateurs sont maîtres de leurs données mais dans la réalité, nous ne les maîtrisons pas et nous sommes souvent dépassés par les autorisations qu nous donnons aux applications que nous installons sur nos smartphones et aux sites que nous visitons (régulièrement ou pas).