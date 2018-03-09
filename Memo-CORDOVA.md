# Mémo - CORDOVA
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

* [Site officiel APACHE CORDOVA](https://cordova.apache.org/)

## Les commandes Cordova

* Création d’un nouveau projet Cordova comportant le chemin du dossier <path> et le nom choisi
    ```html
    cordova create <path>
    ```
* Création d’une plateforme au projet : Android ou iOS (uniquement sur Apple) ou Browser pour une WebApp
    ```html
    cordova platform add <platform name>
    ```	
    Exemple pour ajouter un environnement Android
    ```html
    cordova platform add android 
    ```
* Exécute et compile (commande 'build') le projet dans l’environnement choisi : soit Android pour le lancer dans le simulateur de téléphone

    ```html  
    cordova run <platform name>
    ```
* Ajoute un plugin et met à jour le fichier .json des différentes plate-formes
    ```html
    cordova plugin add <plugin name>
    ```
	
## Structure d’un projet Cordova

| Nom du répertoire	| Contenu |
| ------------- |:------------- |
| “platforms”  | Dossier « android » créé avec le projet complet sous l’environnement Android ou dossier « browser » créé avec le projet complet pour une appli web classique | 
| “plugins”|	Des fichiers « android.json » et « browser.json » contenant les différents plugins installés pour chaque environnement|
|“www”|	Le projet complet avec son index.html et les fichiers associés css, images et js dans des dossiers séparés|
|“package.json”	|C’est le fichier de configuration de notre application pour npm. Il contient au minimum le nom du projet, la version (majeure, mineure et patch) et le tableau listant les dépendances installées avec npm.|
|“config.xml”|	C’est le fichier de configuration global du projet pour Cordova. Il contient les informations nécessaires sur l'application (nom, description, auteur, les plugins et les paramètres spécifiques aux plate-formes concernées |
|“www/index.html”|	C’est la page de démarrage du projet, celle qui sera affichée dans le navigateur ou dans le mobile.|
|||
