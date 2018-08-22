# Mémo C# .Net
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

* [Cours sur Open ClassRoom](https://openclassrooms.com/fr/courses/218202-apprenez-a-programmer-en-c-sur-net)
* [Documentation .NET](https://docs.microsoft.com/fr-fr/dotnet/standard/)

## Définitions

| Terme        | Définition     |
| ------------- |-------------- | 
| C#     | Language de programmation orienté objet récent (début 2000) inspiré de Java (donc typé) et développé par Microsoft. C'est le langage recommandé pour développer sous Windows. |
| .Net   | C'est le framework ou environnement d'exécution (aussi écrit Dot NET et prononcé "dotte nette") pour programmer en C# sous Windows : accès réseau, création de fenêtres, appel à une base de données... Pour développer sous MacOS ou Linux il faut utiliser .NET Core | 
| Variables | Obligatoirement écrit avec des caratères alphanumériques et _ (underscore) et doit forcément commencer par une lettre. Il ne doit pas être un mot réservé : Type ou classe déjà définie.|

![Types de base](images/csharp/variables.png)

### Conventions d'écriture des variables

* les `guillemets ( " )` servent à encadrer une chaîne de **caractères**
* les `apostrophes ( ' )` servent à encadrer un **caractère**.
```
"Une phrase" et 'A'.
```
* Pour utiliser une variable, il faut d'abord la déclarer : on réserve une partie de la mémoire pour cette variable. On spécifie ce qu'elle représentera *(un entier, un caractère, une image, ...)* en indiquant son type.
```
La syntaxe est : type nom;
```
* **NB** : le point-virgule est indispensable sans quoi Visual Studio ne peut pas compiler le code.
* **NB** : Il est nécessaire de donner une valeur par défaut aux variables crées. Sinon, le compilateur retourenera une erreur.
```
string message = string.Empty;
string message = "";
```
* Il existe deux sortes de types : les ``types valeur`` *(notamment les structures)* et les ``types référence`` *(notamment les classes)*.


### Les énumérations

Liste de valeurs qui a un type unique. Ce type est le nom de l'énumération. 
```java
enum Temps
{
    Inconnu,
    Soleil,
    Nuageux,
    Pluvieux
}
```
On peut ainsi déclarer une variable de type Temps :
```
Temps tempsDuJour = Temps.Soleil;
```
La variable est initialisée à la valeur "Soleil"

* **NB** : Les énumérations se déclarent en tant que membre d'une classe et non dans une méthode.


### Les opérateurs et l'utilisation des conditions est identiques à JAVA.

Rappel : 

| Opérateur           | Définition        | 
| ------------------- |------------------ | 
| <     |   plus petit que          |
| <=    |   plus petit ou égal à    |
| >     |   plus grand que          |
| >=    |   plus grand ou égal à    |
| ==    |   égal à                  |
| !=    |   différent de            |
| &&    |   comparaison "et"        |
| `||`  |   comparaison "ou"        |
|       |                           |
