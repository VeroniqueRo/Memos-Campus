# PHP avec le FRAMWORK LARAVEL
## *Campus Numérique 2018 - Véronique ROUAULT*
#
## Installer composer
Installation avec les commandes sous git bash avec l'install de Windows

`Attention` : se placer dans le dossier où l'on veut travailler avant de lancer la ligne de commande

Sous Windows utiliser [Composer-Setup.exe](https://getcomposer.org/download/)

Il suffira de taper *composer* dans git bash pour lancer une commande en ligne.



```
@ECHO OFF
php C:\composer.phar" %*
```
[Tuto d'installation en français](https://www.formations-laravel.fr/articles/decouverte/2017-01-12-installation-d-un-projet-laravel-avec-windows.html)

## Qu'est-ce que composer ?

Composer est un gestion de dépendances pour PHP.

C'est un système qui permet de définir les différentes librairies dont a besoin une application PHP pour fonctionner.

Composer se charge de les télécharger avec son autoloader intégré.
Il permet aussi d'installer des librairies personnelles.

Pour télécharger une librairie supplémentaire, aller sur le site :   [packagist.org](https://packagist.org/)

* Les librairies s'installent dans le dossier *vendor*
* Les fonctions qui permettent de télécharger les librairies sont enregistrées dans le fichier *composer.json*. elles peuvent être utiles surtout en phase de développement.


## Installation : Création du projet
```
composer create-project --prefer-dist laravel/laravel +nom du projet
```
Installe Laravel et crée un nouveau projet (sans la partie développement. commande --prefer-dist)

NB : A chaque nouveau projet il faut installer `Laravel` et `composer` car les projets LARAVEL sont indépendants les uns des autres.    

Lorsque l'on clone pour la première fois un projet depuis `git`, il est nécessaire de faire la commande pour récupérer le dossier `/vendor` ignoré par le `.gitignore`
```
composer install
```
NB : Si le `.env` n’existe pas, il faut copier le `.env.example` et renommer la copie en `.env`.    
Le `.env` sert à définir l’environnement du projet.     
Il ne doit pas être versionné sur github cra il contient les données propres à l'environnement du projet avec notamment des données sensibles comme le mot de passe.    
L'ajouter au `gitignore` s'il n'y est pas (par défault)

## Lancer le serveur
```
php artisan serve
```
## Installation de la débugbar
```
composer require barryvdh/laravel-debugbar --dev
```
Relancer le serveur et rafraichir la page.
## Configuration de l’éditeur (Visual Studio Code)
Installer l'extension
```
Laravel Blade Syntax Highlighting
```
# Grands principes de LARAVEL
Le trio gagnant du framework
1. Les `Routes`     
Elles définissent le chemin avec des `get` (récupérer) ou des `post` (envoyer) et passe un controlleur   

```
/routes
```
```php
Route::get('/lien-afficher','NomduController@functiondanslecontrolleur');
```
2. Les `Controller`     
Ils font les traitements et leur objectif est de retourner une vue
```
/app/Http/Controllers
```
```php
<?php

namespace App\Http\Controllers;

use Illuminate\Http\Request;
use App\Boisson;// lien vers la classe Boisson

class BoissonController extends Controller
{
    // Méthode pour lister les boissons avec le Model
    function afficheBoissons() {
        
        $boissons = Boisson::all();// Appelle la classe pour ajouter toutes les données

        return view('boissons.lister-boissons', ['boissons'=>$boissons]);// retourne la vue (avec . pour remplacer /) avec un paramètre passé
    
    }
}
?>
```
3. Les `Vues`       
Ce sont les pages visibles du site
```
/resources/views
```
## Les template
Un `template` est un squelette `html` des pages à afficher    
Il utilise une base classique `html + head + body + footer` 
On utilisera des mots clés pour appeler les informations à y afficher

Pour appeler le template du menu ou du footer dans le template principal
```php
@include('template.menu')
@include('template.footer')
```
Pour insérer une section d'une vue
```php
 @yield('titre')
 ```
## Mots clés dans les vues
Pour appeler le `template` dans les vues
```php
@extends('template.template')
```
Pour selectionner la partie qui sera insérée dans le template
```php
@section('titre')
    La liste des ingredients
@endsection
```
# Modèles

`Un modèle permet d'interagir avec les tables de la BDD`


## Créer un modèle & sa migration
Ligne de commande pour créer un modèle et sa migration
```php
php artisan make:model Nom_modele -m
```
Le fichier modèle créé :
```php
App/Nom_modele.php
```

Le fichier de migration créé :
```php
Database/Migrations/create_nomTable_table
```

Renseigner la fonction "UP" avec les champs que l'on veut créer dans la table
```php
class CreateBoissonTable extends Migration
{
    public function up()
    {
        Schema::create('boissons', function (Blueprint $table) {
            $table->increments('id');
            $table->string('name')->unique();
            $table->integer('price');
            $table->timestamps();
        });
    }
}
```

Dans le modèle et dans la classe, indiquer les champs que l'on autorise à modifier 
```php
class Boisson extends Model
{
    //Préciser les champs que l'on a le droit de modifier 
    protected $fillable = ['name', 'price'];
}
```
Pour créer la table dans la BDD : 
```php
php artisan migrate
```
A noter, dans Bash, il est possible d'utiliser Tinker pour dialoguer avec la BDD
```php
php artisan tinker
```

# Bonnes pratiques et conventions d'écriture
"Les fichiers LARAVEL doivent être courts"
1. Créer un `controller` pour chaque ressources
```
class NomdelaressourceController
```
2. Modifier la route pour appeler le controlleur créé
```
Nomdelaressource@function
```
`A noter` : Le nom de la route est celui qui s'affichera dans la barre du navigateur mais peut être différent de celui de la vue.   
C'est le `return` indiqué dans le controller qui définit quelle vue sera retournée.

Les colonnes de BDD sont généralement `snake_case` mais les noms de propriétés sont `camelCase`.
Colons can be used to align columns.

| Ecriture de base  |  en snake_case |   en camel_case |
| ----------------- |:-------------------------:| ----------------:|
| nom de variable   |  nom_de_variable          | NomDeVariable    |
| NomDeVariable     |  nom_de_variable          | NomDeVariable    |
|   Variable        |  variable                 | Variable         |

Le nom du modèle doit avoir le même nom que la table mais au singulier et avec la Première lettre en majuscule
 
Eloquent est capable de faire la conversion automatiquement.

| Nom du Modèle  | Nom de la table de la BDD | 
| -------------- |:-------------------------:|
| Boisson        | boissons                  |
| CommandeUser   | comannde_users            |

Les constantes de classe DOIVENT être déclarées dans toutes les majuscules avec des séparateurs de soulignement.
Les noms de classe doivent être déclarés dans StudlyCaps.
Les constantes de classe doivent être déclarées dans toutes les majuscules avec des séparateurs de soulignement.
Les noms de méthodes doivent être déclarés dans camelCase. (c'était snake_case en L3)
Les noms de propriété et les arguments de fonction n'ont généralement pas de règle spécifique, mais doivent être écrits en fonction du paquet. Le document Laravel sur la convention ne donne pas plus d'informations sur les noms de propriétés. La seule règle est: utilisez toujours la même chose. Je suggérerais camelCase.
Les noms de fonctions sont camelCase. (cependant, les normes officielles de codage PHP conseillent snake_case).
Pour les noms de variables je suggérerais camelCase, cependant snake_case est conseillé par les normes officielles de codage PHP, contrairement aux recommandations de Zend Framework, qui interdit explicitement les underscores. Les variables ne sont pas mentionnées dans le groupe d'interopérabilité du framework PHP et je ne trouve aucun exemple dans le framework de base Laravel car tous les noms de variables sont des mots simples.
