# Memo - Formulaires sous LARAVEL
## *Campus Numérique 2018 - Véronique*
#

## Projet de découverte de la récupération des données d'un formulaire avec LARAVEL

1. cloner le dépot Git.

2. Placer le répertoire choisi dans le www de wampserver
```
mkdir [nom du répertoire]
cd [nom du répertoire]
git clone https://github.com/campus-digital-grenoble/PHP_Formulaire.git .
```

3. Installation des dépendances via composer (Vendor)
```
composer install
```
4. Ajouter le fichier d'environnement en dupliquant le .env.exemple
```
cp .env.example .env
```
5. Générer une clé unique dans le .env
```
php artisan key:generate
```
6. Lancer le projet
```
php artisan serve
```
___
## Ajouter une nouvelle route pour le formulaire HTML

Les routes doivent être ajoutées dans le fichier `routes/web.php`
```php
Route::get('/news/create', 'NewsController@create');
```
Cette route répond aux requêtes de type GET
```php
Route::post('/news', 'NewsController@store');
```
Cette route répond aux requêtes de type POST

Le formulaire est redirigé vers la vue avec la Méthode POST

```html
<form class="" action="/news" method="post">
```
```html
@extends('template')
@section('content')
    <div class="panel panel-default">
        <div class="panel-heading">
            <h2 class="panel-title">Formulaire #2 News</h2>
        </div>
        <div class="panel-body">
            <form class="" action="/news" method="post">
                {{ csrf_field() }}
                <div class="form-group">
                    <label for="title">Title</label>
                    <input type="text" class="form-control" name="title" placeholder="title">
                </div>
                <div class="form-group">
                    <label for="content">Content</label>
                    <textarea name="content" id="content" class="form-control" rows="8" cols="80"></textarea>
                </div>
                <button type="submit" class="btn btn-primary">Submit</button>
            </form>
        </div>
    </div>
@endsection
```
Pour que le formulaire soit sécurisé (sinon Laravel renvoie une erreur "This page has expired due to inactivity") il est nécessaire d'ajouter

```
{{ csrf_field() }}
```




