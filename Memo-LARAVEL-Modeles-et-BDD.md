# Mémo LARAVEL - Modèles et BDD
## *Campus Numérique 2018 - Véronique ROUAULT*
#

# Les Modèles

`Un modèle permet d'interagir avec les tables de la BDD`

## Créer un modèle & sa migration
Ligne de commande pour créer un modèle et sa migration
```php
php artisan make:model Nom_modele -m
```
* Le fichier modèle créé sera dans :
```php
App/Nom_modele.php
```

* Le fichier de migration créé sera :
```php
Database/Migrations/create_nomTable_table
```
Pour créer une table de migration directement dans le dossier Database/Migrations/
```php
php artisan make:migration create_nomTable --create=nomTable
```

## Renseigner la fonction "UP" avec les champs que l'on veut créer dans la table
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
Pour annuler la dernière migration faite. (`Attention` : à utiliser prudemment car la table et les données seront perdues).
```php
php artisan migrate:rollback
```