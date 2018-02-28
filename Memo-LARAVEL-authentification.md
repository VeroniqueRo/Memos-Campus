# Mémo LARAVEL - Authentification
## *Campus Numérique 2018 - Véronique ROUAULT*
#

Laravel contient une authentification permettant de se connecter, déconnecter, enregistrer et même envoyer un email lors de la perte du mot de passe.

## Commande pour créer les routes et vues

Pour créer automatiquement les routes et vues

```php
php artisan make:auth
```

## Commande pour avoir la liste des routes :

```php
php artisan route:list
```
Dans le fichier web.php les routes suivantes sont crées :

```php
Auth::routes();
Route::get('/home', 'HomeController@index')->name('home');
```
Il faut modifier le "/home" en /

En cas de problème de redirection vérifier le HomeController :
```php
public function index()
{
    return view('tableaubord'); //choisir la bonne vue à retourner
}
```
## Protéger les routes

Pour que les utilisateurs qui ne sont pas authentifiés ne puissent pas accéder au site, il faut protéger les routes en ajoutant à la fin de toutes les routes le Middleware :
```php
Route::get('/Liste_boissons','BoissonController@index')->name('listeBoissons')->middleware('auth');
```
Si un internaute entre l'URL "https://www.lapausesimpose.club/Liste_boissons" on sera redirigé vers la page Login.

Pour protéger l'accès à la page d'enregistrement `register`, ajouter dans le RegisterController (Http/Controllers/Auth)

```php
public function __construct()
    {
        $this->middleware('auth');
    }
```

## Récupérer les informations Utilisateurs

Ajouter dans le Controller le lien :

```php
use Illuminate\Support\Facades\Auth;
```
Vérifier si l'utilisateur est connecté :
```php
Auth::check(); // Retourne True or False
```
Récupérer l'id de l'utilisateur :
```php
Auth::id();
```
Récupérer un objet avec les données de l'utilisateur
```php
Auth::user();
```
Infos

Liste des fichiers créés automatiquement :

Dans le fichier "web.php", le code suivant a été ajouté pour créer l'ensemble des routes :
```php
Auth::routes();
Route::get('/home', 'HomeController@index')->name('home');

    Vue : 'home'
    Dans les "Views" il y a 2 nouveaux dossiers : Auth et Layouts
    Dossier "Auth" :
        Dossier Passwords contenant les vues 'email' et 'reset'
        Vue 'Login'
        Vue 'Register'
    Dossier "Layouts" :
        Vue 'app' : template avec barre de navigation et déconnexion
    Controller : HomeController (App\Http\Controllers)
    ...
```
