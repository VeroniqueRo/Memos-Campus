# Mémo - CORDOVA + Vue.js
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

* [Site officiel VUE JS](https://fr.vuejs.org/index.html)

## Structure d’un projet Cordova + Vue.js

| Nom du répertoire	| Contenu |
| ------------- |:------------- |
| Contenu du répertoire “build”  |  | 
| Contenu du répertoire “config” |	|
| Contenu du répertoire “node_modules” | Les dépendances installées	|
| Contenu du répertoire “resources” |	 |
| Contenu du répertoire “src” |	|
| Contenu du répertoire “static” | |
| Contenu du répertoire “www” | |

## Commandes

* Lance le projet pour permettre son développement
    ```html
    npm run dev
    ```
* Génère un dossier utilisable en production. Dans ce projet "minifié" seront intégrées les `dépendencies` qui sont différentes des `dev-dépendencies` nécessaires au développement.

    ```html
    npm run build
    ```
* Commandes supplémentaires :
    
    Incrit le package dans le dosseir des dépendencies

    ```html
   --save
    ```
    Incrit le package dans le dosseir des dev-dépendencies

    ```html
   --save -dev
    ```

