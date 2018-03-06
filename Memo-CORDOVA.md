# Mémo - CORDOVA
## *Campus Numérique 2018 - Véronique ROUAULT*
#
## Ressources en ligne

* [Site officiel APACHE CORDOVA](https://cordova.apache.org/)

## Les commandes Cordova

* Création d’un nouveau projet Cordova comportant le chemin du dossier <path> et le nom choisi
    ```html
    cordova create <path>
    ```
* Création d’un projet selon son environnement : Android ou iOS (uniquement sur Apple) ou Browser pour une WebApp
    ```html
    cordova platform add <platform name>
    ```	
    Exemple pour ajouter un environnement Android
    ```html
    cordova platform add android 
    ```
* Exécute et compile le projet dans l’environnement choisi : soit Android pour le lancer dans le simulateur de téléphone

    ```html  
    cordova run <platform name>
    ```
* Ajoute un plugin aux .json des différentes plate-formes
    ```html
    cordova plugin add <plugin name>
    ```
	
## Structure d’un projet Cordova

| Nom du répertoire	| Contenu |
| ------------- |:------------- |
| “platforms”  | Dossier « android » créé avec le projet complet sous l’environnement Android ou dossier « browser » créé avec le projet complet pour une appli web classique | 
| “plugins”|	Des fichiers « android.json » et « browser.json » contenant les différents plugins installés pour chaque environnement|
|“www”|	Le projet complet avec son index.html et les fichiers associés css, images et js dans des dossiers séparés|
|“package.json”	|C’est la carte d’identité de notre application. Il contient au minimum le nom du projet, la version (majeure, mineure et patch) et le tableau listant les dépendances installées avec npm.|
|“config.xml”|	C’est le fichier de configuration global du projet. Il spécifie son nom, sa description, son auteur, les plugins et les paramètres spécifiques aux plate-formes|
|“www/index.html”|	C’est la page de démarrage du projet, celle qui sera affichée dans le navigateur ou dans le mobile.|
|||
