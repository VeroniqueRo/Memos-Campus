# Mémo C# .Net - HelloWorld
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

* [Cours sur le fonctionnement sur Open ClassRoom](https://openclassrooms.com/fr/courses/392266-developpement-c-net/391031-le-fonctionnement-de-net)
* [Cours HelloWorld sur Open ClassRoom](https://openclassrooms.com/fr/courses/218202-apprenez-a-programmer-en-c-sur-net/217501-les-winforms-ou-windows-forms)
* [Documentation Microsoft](https://docs.microsoft.com/fr-fr/visualstudio/ide/quickstart-visual-basic-console)

# Définition

`Langage compilé` : Après avoir écrit le code, il est nécessaire d'utiliser un compilateur qui transformera le programme en langage machine compris par le processeur.

Si une modification doit être apportée au programme, il faudra compiler à nouveau le code source.

Mais une fois compilé, le programme n'aura plus besoin de rien d'autres pour fonctionner.

`Langage interprété` : Il n'est pas tranformé en langage machine avant d'être exécuté. Un interpréteur transforme la source en un résultat. Les exemples les plus simples de langages interprétés sont les langages permettant d'afficher une page web, ils sont lus par une programme externe *(le navigateur web)* qui affichera un résultat.

Si une modification est ajoutée au code source, il n'y aura pas besoin de compiler une nouvelle fois l'application.

Mais ces types de programmes ont besoin d'autres programmes pour être exécutés.

# Fonctionnement de .net

Le C# est un langage à mi-chemin entre un **langage compilé** et **langage interprété** : il n'est pas directement compilé en langage machine, mais il n'est pas non plus interprété !

Le C# est précompilé en un langage intermédiaire *(appelé IL pour "Intermediate Language")*.

Lors de l'exécution, ce langage intermédiaire va être compilé en langage machine et exécuté par le CLR *(Common Language Runtime)*, ce "runtime" va en quelque sorte faire l'intermédiaire entre le code et le système d'exploitation en apportant une importante abstraction vis à vis de fonctions systèmes de bases *(entrés/sorties, gestion de la mémoire, etc...)*.


## Shéma du fonctionnement interne de .net
![Fonctionnement interne de .net](images/csharp/fonctionnement-dot-net.png)

# Création d'un nouveau projet sous Visual Studio

 Dans la fenêtre principale, allez sur la menu `Fichier`, puis `Nouveau` et `Projet`. 

 Dans la fenêtre qui s'ouvre choisir le type de projet `Application console (.NET Framework)`

 Le Framework crée une `Solution` avec le nom choisie

 Elle génère différents dossiers dont `Program.cs` 
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace NomChoisiPourLaSolution
{
    class Program
    {
        static void Main(string[] args)
        {
        }
    }
}
```
# Gestionnaire de paquets : NuGet

* [Tuto de l'utilisatiopn de NuGet - OpenClassroom](https://openclassrooms.com/fr/courses/2818931-programmez-en-oriente-objet-avec-c/2819156-utilisez-le-gestionnaire-de-package-nuget)

NuGet est un gestionnaire de package permettant de faciliter la gestion des références externes d'un projet. Il est utilisable aussi en mode console  
* Aller dans `Outils`
* Choisir `Gestionnaire des packages NuGet` -> `Gérer les packages Nuget pour la solution`

```
package à utiliser : Newtonsoft.Json
```
----
# Utilisation d'une Bibliothèque de classes (.dll)
 
* [Créez un projet bibliothèque de classes - OpenClassroom](https://openclassrooms.com/fr/courses/2818931-programmez-en-oriente-objet-avec-c/2819146-creez-un-projet-bibliotheque-de-classes)

## Pourquoi utiliser des bibliothèques de classes ?
* Pour leur aspect réutilisable :  
Il est possible de stocker dans une librairie des classes et des méthodes qui auront besoin d'être utilisées plusieurs fois et/ou partagées par plusieurs applications.  

* Pour l'architecture globale du projet :
Architecturer son application permet de faciliter sa mise en place, sa maintenabilité et son évolutivité. 

## Pour créer une dll dans la "solution"

```
-> clic droit sur notre solution et faire Ajouter > Nouveau Projet  
-> Choisir le type "Bibliothèque de classes"  
-> Lui donner un nom 
```

*nb : après création du projet library : lancer "générer la solution" pour afficher les fichiers .dll et .pdb*

## Générer et utiliser la library  

```
-> clic droit sur les références du projet et sélectionner « Ajouter une référence »  
-> projet > solution > selectionner la library > ok
```

## Exemple appel de la library
```
MaBibliotheque.Bonjour bonjour = new MaBibliotheque.Bonjour();  //objet.class nom = new objet.class()
bonjour.DireBonjour(); //nom.methodedansclassBonjour()
```

# Récupération d'une API

## Ressources en ligne
* [JsonLint](https://jsonlint.com/) : Permet de tester et de visualiser une API 
* ​[Json2csharp](http://json2csharp.com/) ​: Cet outil en ligne permet de trouver la structure de données à utiliser pour convertir un flux json en objet C#

# Création d'un dossier de tests unitaires

## Création du dossier global

* Faire un clic droit sur la `solution souhaitée`
* Choisissez `Ajouter`, puis `Nouveau projet`
* Dans la boîte de dialogue Nouveau Projet, développez `Installé`, développez `Visual C#`, puis choisissez `Test`.
* Dans la liste des modèles, sélectionnez `Projet de test unitaire(;NET Framework)`.
* Saisir un nom (exemple UnitTests) dans la zone Nom, puis choisissez OK.
* Le projet "UnitTests" est ajouté à la solution.
* Dans le projet "UnitTests", ajoutez éventuellement une référence à la solution.
* Dans l’Explorateur de solutions, sélectionnez `Références` dans le projet "UnitTests" puis choisissez `Ajouter une référence` dans le menu contextuel.
* Dans la boîte de dialogue `Gestionnaire de références`, développez `Solution` puis cochez l’élément souhaité.

## Ajout d'un test sur une classe spécifique

* Dans la classe à tester faire un clic sur classe à tester
* Choisir `créer des tests unitaires`
* Dans la boite de dialogues selectionner le projet de tests, puis choisissez OK.

*NB : Les références seront ajoutées automatiquement et le nom par défaut sera NomdelaclasseTests.cs*

# Utilisation des Fake objets pour l'injection de dépendances

## Création d'une interface :  

* Faire un clic droit sur le dossier souhaité
* Choisissez `Ajouter`, puis `Nouvel élément` ou `Ctrl + Maj +A`
* Choisir `Interface` 
* Nommer ->  Ok
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace HelloWorld
{
    public interface IDateTime
    {
        DateTime Date { get; } // Exemple de propriété à implémenter
    }
}
```
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace TransportsLibrary
{
    public interface IConnexionApi
    {
        String ConnexionApi(string url); // Exemple de méthode à implémenter
    }
}
```
## Création des classes qui implémentent cette interface

* Création d'une classe `RealDateTime` pour la date réelle
```csharp
namespace HelloWorld
{
    class RealDateTime : IDateTime
    {
        public DateTime Date
        {
            get { return DateTime.Now; } // Propriété retournant la date actuelle
        }

    }
}
```
### Dans l'exemple de la connexion a une API, la Connexion devient la RealConnexion 

* Création d'une classe `FakeConnexionApi` réservée aux tests
```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using UnitTestProject;

namespace TransportsLibrary
{
    class FakeConnexionApi : IConnexionApi
    {
        public String resultatJson { get; set; } // Propriété permettant de gérer les données de Ressource1

        public String ConnexionApi(string url) // Méthode qui implémente celle de l'interface
        {
            return resultatJson;
        }
    }
}
```
## Créez une application WPF 

* Allez sur la menu `Fichier`, puis `Nouveau` et `Projet`. 
* Choisir le type de projet `Application WPF (.NET Framework)`
* Choisir un nom -> `OK`


* [Implémentation d'un MVVM](https://www.youtube.com/watch?v=0IKOphciSZo)

Les liaisons peuvent être des liaisons de données `OneWay` ou `TwoWay` vers des données de flux entre View et ViewModel.


