# Mémo - MOBILE
## *Campus Numérique 2018 - Véronique ROUAULT*
#
## Ressources en ligne

* [Mobizel](http://www.mobizel.com/2015/04/developpement-dune-application-mobile-native-13/)
* [Open Classrooms](https://openclassrooms.com/courses/des-applications-ultra-rapides-avec-node-js/les-modules-node-js-et-npm
)
* [Site officiel NPM](https://www.npmjs.com/)

## Glossaire

| Terme	| Définition |
| ------------- |:------------- |
| IDE  | Intégrated Development Environnement
| 
| `Sous iOS (Apple)`	| |
| Xcode  (IDE pour iOS)	| Est un environnement de développement pour le système d'exploitation macOS ainsi que pour IOS
| Objective-C (Langage pour iOS)	| Est un langage de programmation orienté objet réflexif extension du C. Il est principalement utilisé dans les systèmes d'exploitation d'Apple : macOS et son dérivé iOS
| 
| `Sous Android`	| |
| Android studio (IDE pour ANDROID)	| Est un environnement de développement pour le système d'exploitation Android
| Eclipse (IDE pour ANDROID)	| Eclipse est un projet, décliné et organisé en un ensemble de sous-projets de développements logiciels, de la fondation Eclipse visant à développer un environnement de production de logiciels libre qui soit extensible, universel et polyvalent, en s'appuyant principalement sur Java.
| Java (Langage pour ANDROID)	| Langage de développement pour Android
| 	
| SDK (propre à chaque système d'exploitation)	| Pour créer une application mobile, il faut “communiquer avec le SDK natif” via le code source. SDK (Software Development Kit) est l'ensemble des outils d'accès aux fonctionalités d'un mobile (géolocalisation, contact, médias, appareil photo…) pour permettre la programmation d’applications mobiles.
| 
| Application mobile native générée | application mobile qui n’a pas été développée avec la technologie et le langage natifs à son système d’exploitation mais via une autre technologie (Xamarin, Titanium, Qt, etc.) qui va utiliser du code partagé entre plusieurs plateformes et générer un logiciel exécutable sur chaque OS visé.
| Technologie cross-platform | technologie pouvant générer plusieurs logiciels à destination de systèmes d’exploitation différents à partir d’un code unique

## Développement d’une application mobile native

Une `application mobile native` est une application conçue spécifiquement pour un système d'exploitation (OS) avec un langage et une technologie appropriés.

![Natif](images/developpement-natif.png).

Tableau des langages et IDE* les plus courants pour chaque système d’exploitation

| Système d’exploitation  | Langage(s) | IDE (environnement de développement) |
| ------------- |:-------------:| -----:|
| iOS (Apple)	| Objective C et Swift	| Xcode |
| Android	| Java	| Android Studio ou Eclipse |
| Windows Phone | C# (se dit “C sharp”) | Visual Studio |

## La conception en trois étapes

1 – Rédaction du code source

Le code source de la future application est rédigé dans un langage approprié à l'OS.
Pour développer une application qui puisse exploiter les fonctionnalités natives du mobile (géolocalisation, contact, médias, appareil photo…) il faut “communiquer avec le SDK natif” via le code source. C’est-à-dire programmer des « ponts » qui vont aller chercher des morceaux de codes du SDK du système d’exploitation visé. Ces derniers vont permettre d’“appeler” des fonctionnalités natives pour les intégrer dans l’application mobile.

2 – Compilation du code source

La compilation a un rôle primordial car les logiciels fonctionnent avec du code binaire qui est trop complexe pour être conçu tel quel. Il faut donc rédiger un code plus simple “human readable” (le code source) qui va passer dans un compilateur et être transformé en code binaire “machine readable”. Les IDE contiennent un compilateur.

 
3 – Génération d’un code binaire natif

Le compilateur (Apache Cordova (Open Source) /PhoneGap (commercial) ) transforme le code source en code binaire et génère un fichier spécique à chaque système d'exploitation.
| Système d’exploitation  | Nom d’extension de fichier |
| ------------- |:-------------:| 
| iOS (Apple) |	.ipa |
| Android	| .apk |
| Windows Phone	| .appx |

Pour fonctionner, ce fichier peut être téléchargé (via les magasins d’applications "stores"), installé puis exécuté sur le téléphone.

## Développement d’une application mobile native générée
Les technologies `cross-platform` permettent de réaliser un code source unique qui sera transformé en plusieurs logiciels adaptés aux OS visés.

### Fonctionnement générique d’une technologie de développement mobile cross-platform
    Conception également en trois étapes : RÉDACTION => COMPILATION => GÉNÉRATION
    
## Développement d’une application mobile hybride

Définition

* Une application mobile hybride est développée à partir de langages web (HTML5, JavaScript, CSS…)
* Elle s’appuie aussi sur des technologies natives mobiles pour utiliser certaines fonctionnalités du smartphone.
* Elle sera téléchargée depuis les magasins d’applications (stores) et installée sur le mobile.

Différente de la `web app` qui n’est consultable que depuis un navigateur. LinkedIn est une application mobile hybride.

![Hybride](images/developpement-hybride.png)
 
## Différences entre une WebApp et une Application Mobile

![Différences](images/comparaison-webapp-application-mobile.png).

## Différences entre un Site Web et une Application Mobile

![Shema](images/shema-mobile.png)