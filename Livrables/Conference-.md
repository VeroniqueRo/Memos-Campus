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
* Le [detailed targeting](https://www.facebook.com/business/help/633474486707199) pou `ciblage d'audience` permet de choisir le pannel que l'on veut atteindre avec des carractéristiques plus ou moins personnelles.

En effet, Facebook référence et conserve **614 attributs** sur chaque utlisateur.

### Comment le réseau récupère-t-il ces attributs ?

* `En enregistrant les actions` de l'utilisateur (clics, avis, like...) sur son compte. 
* En suivant les liens vers les sites visités hors du réseau pendant que l'utilisateur est connecté à son compte.
* En utilisant les données vendues par les [Data Brokers](https://atelier.bnpparibas/smart-city/article/data-brokers-commerce-donnees-personnelles) comme Acxiom, Epsilon, Experian Marketing Services, Oracle Data Cloud (Datalogix), Quantium…

	Les Data Brokers (les "Casseurs de Silo" !) sont des sociétés qui récupèrent et agrègent de très nombreuses données sur les personnes et revendent ces précieuses informations aux marques. Cette récupération de données se fait notamment via les cartes de fidélité magasin qui ont accès à nos achats, (fréquences et montants) ainsi qu'à nos coordonnées complètes.

Tout cela constitue les `PII` (Personally Identifiable Information). Les `informations d'identification personnelles` de chaque individu et pose un problème d'atteinte aux libertés individuelles.

*Nota* : Suite au scandale qui la touche, il semblerait que Facebook ait décidé de se passer des services de ces Big Brother du Big Data ! [Voir Article du 29/03/2018](https://www.blogdumoderateur.com/facebook-desactive-data-brokers/)

## Les risques majeurs de cette pratique

1. Atteinte à la vie privée
	
	Facebook donne la [Potential Audience](https://www.facebook.com/business/products/ads/ad-targeting) de chaque utilisateur
	* Le numéro de téléphone d'une personne peut être récupéré avec la connaissance de sa date de naissance.
	* Les [Pixels Facebook](https://fr-fr.facebook.com/business/help/742478679120153?helpref=page_content) sont des marqueurs invisibles lié à un outil d'analyse et placés sur les sites web des annonceurs. C'est un outil d'annalyse permettant d'assurer aux annonceurs que leurs publicités sont bien diffusées auprès des bonnes personnes.
	
	* Facebook donne aux annonceurs le [Potential Reach](https://www.facebook.com/business/help/624074880953806), c'est à dire le nombre d’utilisateurs qui seront impactés par la campagne de pub (*la portée potentielle du ciblage*). Cela leur permet d'identifier l'utilisateur d'un compte Facebook.

	Cependant le bug a été résolu le 22/12/2017. On ne peut plus faire de ciblage sur plusieurs PII.

2. La discrimination 

	Cela peut poser problème en cas de recrutement par exemple si l'on décidait de ne cibler que les hommes.
	Depuis 2016, le ciblage par ethnie n'est plus possible sur le réseau social.
	Cependant, en regroupant les informations de la `custum list` (pages visitées, likes...) on peut très facilement en déduire l'ethnie. C'est ce qu'on appelle les `attributs corrélés`.
	Par exemple, on pourrait cibler les afro-américains en lancant une recherche sur les personnes aimant le Gospel ou un type de cuisine.

3. Le manque de transparence

	Bien que les réseaux sociaux (notamment Facebook et Twitter) se disent vouloir être transparents sur le sujet et nous permettent de consulter la raison qui a permis à un annonceur de nous cibler, cela reste insuffisant.

	En effet, Facebook ne communique qu'un seul critère le plus large possible et les attributs sensibles sont volontairement masqués par celui-ci qui l'ai forcément moins.

## Conclusion

Les réseaux sociaux veulent nous faire croire que leurs utilisateurs sont maîtres de leurs données mais la réalité est tout autre.

Nous donnons à notre insu beaucoup de droit d'accès aux applications que nous installons notamment sur nos téléphones portables.
Il est donc important de garder un regard sur les autorisations d'accès que l'on donne aux applications mobiles et le cas échéants préférer ne pas les installer.

Il est  important également de se déconnecter des réseaux sociaux lorsque l'on surf sur le net pour des recherches ou des achats. 


Afin d'aider les internautes à comprendre les annonces qu'ils recoivent sur Facebook, `Patrick Loiseau` a mis en place un outil en ligne pour connaitre les données collectées par Facebook [**AdAnalyst** ](https://adanalyst.mpi-sws.org/)
où l'on peut, en s'inscrivant, savoir pourquoi on recoit telle ou telle publicité, Qui d'autre la recoit, ce que Facebook sait sur moi et quele annonceur nous cible.

Un moyen de faire progresser la transparence et de nous rendre un peu plus maître de nos données. 
Avec le [scandale international](http://www.cnetfrance.fr/news/scandale-facebook-ce-qu-il-faut-savoir-pour-comprendre-l-affaire-et-proteger-ses-donnees-39865776.htm) qui implique Facebook depuis quelques semaines (*Nota : Des consultants ayant travaillé pour la campagne présidentielle de Donald Trump ont exploité les données Facebook personnelles de millions de personnes...*), on peut espérer que les internautes les moins méfiants ouvriront enfin les yeux et que cela fera évoluer les choses... ou pas !