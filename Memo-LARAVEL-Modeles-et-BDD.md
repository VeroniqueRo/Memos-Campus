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
# Les relations  

## Relation 1:n   --->  hasMany()

Une boisson a plusieurs ventes
  
Dans le model Boisson, ajouter :

```php
public function ventes()
{
return $this->hasMany('App\Vente');
}
```      
Dans le model Vente, ajouter
```php
public function boisson ()
{
return $this->belongsTo('App\Boisson');
}
```

La méthode `boisson` (au singulier) permet de trouver la boisson qui appartient à la vente `(belongsTo)`.
C'est la réciproque de la méthode précédente.  


Dans le fichier de migration vente :
```php
public function up()
    {
    Schema::create('ventes', function (Blueprint $table)
    {
        $table->increments('id');
        $table->integer('nbSucre'); 
        $table->integer('boisson_id')->unsigned();
        $table->foreign('boisson_id')->references('id')->on('boissons');            
        $table->timestamps();
    });
```
Dans le fichier controller vente, ajouter dans l'entête les liens réciproques des 2 modèles
```php
    use App\Vente;
    use App\Boisson; 
```
        
et ajouter une fonction store
```php
//ajouter une commande
public function store(Request $request)
{
    $newVente = new Vente();
    
    $newVente->boisson_id = request('inputBoisson');
    $newVente->nbSucre = request('inputNbSucre');
    $newVente->save();

    return redirect('/Liste_ventes');
}
```
    
Dans le fichier vente.blade :
```php
<table class = "table table-hover table-bordered">  
                <tr class="active">
                    <td>Numéro de vente</td>
                    <td>Nom de la boisson</td>
                    <td>Nombre de sucres</td>  
                    <td>Prix</td>
                    <td>Date de la vente</td>
                </tr>
                @foreach($ventes as $vente)
                    <td>{{$vente->id}}</td>
                    <td>{{$vente->boisson->nom}}</td>
                    <td>{{$vente->nbSucres}}</td>
                    <td>{{$vente->boisson->prix}} cts</td>
                    <td>{{$vente->created_at}}</td>
                    </tr>
                @endforeach
            </table>
```
Dans le fichier route 
```php
    // Route pour l'ajout d'une vente

        Route::post('/machineACafe','VenteController@store')->name('ajoutVente');
```
----
## Relation n:n  ---> belongsToMany() 

On veut créer des recettes à partir des ingrédients.

Une boisson peut avoir plusieurs ingrédients et un ingrédient peut appartenir à plusieurs boissons  

Dans le model Boisson :
```php
public function ingredients()
{
    return $this->belongsToMany('App\Ingredient')->withPivot('nbDose');
}  
```         
Dans le model Ingredient :
```php
public function boissons()
    {
<<<<<<< HEAD
        return $this->belongsToMany('App\Boisson')->withPivot('nbDose');
=======
        return $this->belongsToMany('App\Boisson')->withPivot('nbDose','id');
>>>>>>> 886357e5266a7a3d515fa9076b24577e9d8dd71a
    }  
``` 
___   
## Créer la table de liaison entre Boisson et Ingrédients (qui correspond aux Recettes)

En ligne de commande

    $ php artisan make:migration create_boisson_ingredient_table


## Dans le fichier de migration qui vient d'être créé, préciser les champs dans la table de liaison (clé primaire & étrangère)
``` php
public function up()
    {
        Schema::create('boisson_ingredient', function (Blueprint $table) {

            $table->integer('boisson_id');
            $table->integer('ingredient_id');
            $table->primary(['boisson_id','ingredient_id']);  //clé primaire : couple
            $table->foreign('boisson_id')->references('id')->on('boissons'); //clé étrangère
            $table->foreign('ingredient_id')->references('id')->on('ingredients'); //clé étrangère
            $table->integer('nbDose');
            $table->timestamps();
        });
    }
``` 

Faire la migration en ligne de commande : 

    php artisan migrate

___   
## Afficher toutes les recettes et toutes les boissons

Dans le fichier RecetteController
```php
public function showRecipes() 
{
    //Récupèrer les ingrédients d'une boisson
    $boissons= Boisson::all()->load('ingredients');

    //Retourner la vue avec les données 
    return view('recettes.lister-recettes', ["boissons"=> $boissons]);
}
```
Dans le fichier recette.blade
```php
@foreach ($boissons as $boisson)
    @foreach($boisson->ingredients as $ingredient)
<tr>
    <td>{{$boisson->nom}}</td>
    <td>{{$ingredient->nom}}</td>
    <td>{{$ingredient->pivot->nbDose}}</td>
</tr> 
    @endforeach 
@endforeach 
```
Dans le fichier route
```php
<<<<<<< HEAD
    Route::get('/Liste_recettes','recetteController@index');    
=======
    Route::get('/liste_recettes','RecetteController@index')->name('listeRecettes')
>>>>>>> 886357e5266a7a3d515fa9076b24577e9d8dd71a
```
## Afficher le tableau des Ingrédients d'une boisson (Sur la même page que la boisson)  
Dans le fichier BoissonController
```php
function detailsBoisson($id) {

        $boisson = Boisson::find($id);
        $ingredients = $boisson->ingredients()->get();
        // dump($ingredients);
        $allIngredients = Ingredient::all();

        return view('boissons.detail-boisson', ['boisson'=>$boisson, 'ingredients'=> $ingredients, 'listeIngredients'=>$allIngredients]);
    
    }
```
Dans le fichier detail-boisson.blade
```php
<<<<<<< HEAD
@foreach ($boisson->ingredients as $ingredient)
    <tr>
        <td>{{$ingredient->pivot->id}}</td> 
        <td>{{$boisson->nom}}</td> 
        <td>{{$ingredient->nom}}</td>
        <td>{{$ingredient->pivot->nbDose}}</td> 
        <td>
            <form id= "delete{{$ingredient->pivot->id}}" method="post" action="/ingredient/{{$boisson->id}}/{{$ingredient->id}}">
                {{ csrf_field() }}
                {{method_field('DELETE')}}
                <div class="btn-group">
                    <button type="submit" form="delete{{$ingredient->pivot->id}}" class="btn btn-outline-danger"> X </button>
                </div>
            </form>
        </td>
    </tr>
@endforeach  
=======
@foreach ($ingredients as $ingredient)
        <tr>
            <td>{{$ingredient->id}}</td>
            <td>{{$ingredient->nom}}</td>
            <td>{{$ingredient->pivot->nbDose}}</td>
            <td>{{$ingredient->stock}}</td>
        </tr>
        @endforeach
>>>>>>> 886357e5266a7a3d515fa9076b24577e9d8dd71a
```
Dans le fichier controller 

*(attention : cette methode effectue plusieurs actions)*  
```php
function lien(boisson $id)
    {	/*$boisson =boisson::find($id);*/
        $boisson = $id->load('ingredients'); // load relation avec ingredients
        $allIngredients = Ingredient::all(); // récupère toutes les données ingredients
        $allIngredients= $allIngredients->diff($boisson->ingredients); //différence entre les données présentes et absentes (affiche les ingrédients qui ne sont pas déjà présents dans la recette)
        $data = [
            'boisson' => $boisson,
            'allIngredients' => $allIngredients,
        ];

        return view('back_office/resultBoisson', $data);
    }
```
## Créer une liste déroulante avec tous les ingrédients disponibles sauf ceux déjà utilisés

Dans le controller boisson
```php
    function lien(boisson $id)
	{	$boisson = $id->load('ingredients'); // load relation avec ingredients
		$allIngredients = Ingredient::all(); // récupère toutes les données ingredients
		$allIngredients= $allIngredients->diff($boisson->ingredients); //différence entre les données présentes et absentes (affiche les ingrédients qui ne sont pas déjà présents dans la recette)
		$data = [
			'boisson' => $boisson,
			'allIngredients' => $allIngredients,
		];

		return view('back_office/resultBoisson', $data);
	}
```

Dans le fichier resultBoisson
```php
    <form class="form-inline col-sm-12 push-3" method ="post" action="/recipe/create/{{$boisson->id}}">
			{{ csrf_field() }}

		<select class="form-control col-sm-3" name="ingredient">
			@foreach($allIngredients as $ingredient)
			<option value="{{$ingredient->id}}">{{$ingredient->nomIngredient}}</option>
			@endforeach
		</select>
		</br>
		<input type="text" name="nbDose" class="form-control" placeholder="quantité" required ="required">
				
		<button type="submit" class="btn btn-outline-secondary" name="valider">valider</button>
				
	</form>
```
Dans le fichier route
```php
    Route::get('/boissons/{id}', 'boissonController@lien');  
```
## Ajouter une recette depuis la boisson sélectionnée

Dans le fichier controller
```php
    public function addRecipe(Request $request, boisson $boisson)
	{	// $ingredient récupère l'id de l'ingredient via la requete
		$ingredient = Ingredient::find($request->input('ingredient'));
		$nbDose = $request ->input('nbDose');
		
		$boisson->ingredients()->attach($ingredient, ['nbDose'=> $nbDose]);

		return redirect()->back();
	}   
```

Dans le fichier .blade
```php
    <form class="form-inline col-sm-12 push-3" method ="post" action="/recipe/create/{{$boisson->id}}">
			{{ csrf_field() }}

		<select class="form-control col-sm-3" name="ingredient">
			@foreach($allIngredients as $ingredient)
			<option value="{{$ingredient->id}}">{{$ingredient->nomIngredient}}</option>
			@endforeach
		</select>
		</br>
		<input type="text" name="nbDose" class="form-control" placeholder="quantité" required ="required">
				
		<button type="submit" class="btn btn-outline-secondary" name="valider">valider</button>
				
	</form>
```
Dans le fichier route
```php
    Route::post('recipe/create/{boisson}','boissonController@addRecipe');
```
    
