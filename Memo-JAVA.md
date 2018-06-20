# Memo - JAVA
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

* [Mémo des mots clés Java sur Developpez.com](http://thierry-leriche-dessirier.developpez.com/tutoriels/java/mots-cles-java/#LIV-B-9)

* [Memento Java](http://www.icauda.com/files/memento-java.pdf)

## Définitions

`Java` est un langage de programmation développé par *Sun Microsystems* (aujourd'hui racheté par *Oracle*) dont la plus grande force est son excellente portabilité (Une fois créé, il fonctionnera aussi bien sous Windows, Mac ou Linux).

`Java` est un langage typé et compilé orienté objet.

`JDK (Java Developpement Kit)` est l'outil de compilation nécessaire à la programmation en Java

`JRE (Java Runtime Environnement)` est l'outil indispensable pour l'utilisation de programme en Java

## Utilisations

* des `applications`, sous forme de fenêtre ou de console.
* des `applets` : des programmes incorporés à des pages web.
* des `applications mobiles`, avec J2ME.

## Installation de l'environnement

* Installer JDK
* Ajouter le chemin vers JDK dans le PATH des variables d'environnement
    ```
    C:\Program Files\Java\jdk1.8.0_161\bin
    ```
* Ajouter une variable "JAVA_HOME" dans les variables d'environnement
    ```
    "JAVA_HOME" : C:\Program Files\Java\jdk1.8.0_161
    ```

* Si JRE et JDK sont tous les deux présents dans les variables d'environnement (PATH) JDK doit être placé avant JRE.

* Dans la console, `javac` doit être accessible et afficher les infos suivantes :

```
$ javac
Usage: javac <options> <source files>
where possible options include:
  -g                         Generate all debugging info
  -g:none                    Generate no debugging info
  -g:{lines,vars,source}     Generate only some debugging info
  -nowarn                    Generate no warnings
  -verbose                   Output messages about what the compiler is doing
  -deprecation               Output source locations where deprecated APIs are used
  -classpath <path>          Specify where to find user class files and annotation processors
  -cp <path>                 Specify where to find user class files and annotation processors
  -sourcepath <path>         Specify where to find input source files
  -bootclasspath <path>      Override location of bootstrap class files
  -extdirs <dirs>            Override location of installed extensions
  -endorseddirs <dirs>       Override location of endorsed standards path
  -proc:{none,only}          Control whether annotation processing and/or compilation is done.
  -processor <class1>[,<class2>,<class3>...] Names of the annotation processors to run; bypasses default discovery process
  -processorpath <path>      Specify where to find annotation processors
  -parameters                Generate metadata for reflection on method parameters
  -d <directory>             Specify where to place generated class files
  -s <directory>             Specify where to place generated source files
  -h <directory>             Specify where to place generated native header files
  -implicit:{none,class}     Specify whether or not to generate class files for implicitly referenced files
  -encoding <encoding>       Specify character encoding used by source files
  -source <release>          Provide source compatibility with specified release
  -target <release>          Generate class files for specific VM version
  -profile <profile>         Check that API used is available in the specified profile
  -version                   Version information
  -help                      Print a synopsis of standard options
  -Akey[=value]              Options to pass to annotation processors
  -X                         Print a synopsis of nonstandard options
  -J<flag>                   Pass <flag> directly to the runtime system
  -Werror                    Terminate compilation if warnings occur
  @<filename>                Read options and filenames from file
  ```

## Premier pas de danse en JAVA

Ecriture du programme HelloWorld.java

```java
public class HelloWorld {
    public static void main(String[] args) {
    System.out.println("Hello, World!");
    }
}
```
Définition d’une `classe` ​*HelloWorld* ​, qui a une `méthode statique` (attachée à la classe et non aux instances de cette classe) *main* ​ (nous passons sur les arguments) et qui utilise la `méthode statique`  *println* de la classe ​*System.out* ​pour faire l’affichage du texte.

Compilation du programme (sur le shell placé dans le répertoire )

```
ls
```
Affichage de la console : 

    HelloWorld.java

Commande pour compiler Java :
```
javac HelloWorld.java
```
Création du fichier compilé *HelloWorld.class*
Affichage de la console :

    HelloWorld.class  HelloWorld.java

Commande pour exécuter Java :
```
java HelloWorld
```
Affichage de la console :

    Hello, World!

Etapes exécutées par la commande `java` :

* cherche la classe HelloWorld dans l’environnement (par défaut dans le répertoire courant => définie dans ​HelloWord.class
* charge cette classe
Page 3/14Introduction à Java
* cherche la méthode par défaut, ​main ​ et l’exécute


```
javac *.java
```
Compile tous les fichiers java du répertoire.

NB : Lors de l’exécution, la classe ne peut être trouvée que depuis le répertoire ​java (le package) où elle se trouve.
La notion de package est très utile pour organiser son code.

## L'outil de build *Maven*

Cet outil permet de gérer des dépendances (modules externes) et le cycle de compilation comme Composer (PHP) ou Artisan (Laravel).

* [Lien de téléchargement de Maven](http://maven.apache.org/)
* [Instructions d'installation](http://maven.apache.org/install.html)

Placer le dossier dézippé `apache-maven-3.5.3-bin` dans le `C:/Programmes` et lancer la commande dans le dossier où se trouve les fichiers à compiler (Hello_2) au niveau *pom.xml*
En effet, l’utilisation de Maven repose sur un Project Object Model (POM)ici un seul fichier ​pom.xml à côté sur répertoire ​src. 

    mvn -v

Permet de vérifier la version de Maven et s'il est bien installé.

    mvn compile


Quand on fait `mvn compile` Maven crée un répertoire *target* contenant les classes compilées.

    mvn clean

Supprime les classes et le dossier `target` compilé

    mvn install

Installe toutes les dépendances et compile en créant un répertoire `target`

    mvn clean install

A faire à la fin d'un projet quand on veut effacer le dossier avec les classes compilées et tout recompiler (créer le dossier Target et compiler les classes)

    java -cp target/classes hello.HelloWorld

Il faut indiquer à Java le (ou les) chemin pour trouver les classes pour l’exécution. On utilise ici l’option ​`-cp` (classpath) pour indiquer de chercher dans le répertoire ​target/classes.

    java -cp target/hello-1.jar hello.HelloWorld

Maven “installe” le projet en créant le jarfile. Qui permet de "Pakager" ses applications dans une archive (avec quelques méta-données -https://fr.wikipedia.org/wiki/JAR_(format_de_fichier). Ce jarfile `.jar` peut être passé comme un répertoire pour indiquer un endroit où trouver des classes, via l’option ​-cp ​ (le “classpath”)

## Ajouter un package pour ajouter l'heure dans le projet Hello_3
```java
<dependencies>
    <dependency>
      <groupId>joda-time</groupId>
      <artifactId>joda-time</artifactId>
      <version>2.9.2</version>
    </dependency>
  </dependencies>
  ```
Si l'instruction `mvn install` ne suffit pas à installer les dépendances manquantes, elles peuvent être ajutées manuellement dans le fichier `pom.xml`

```
$ java -cp target/hello-1.jar:/c/Users/veronique.rouault/.m2/repository/joda-time/joda-time/2.9.2/joda-time-2.9.2.jar hello.HelloWorld
The current local time is: 14:24:23.285
Hello world!
```
## Les variables en Java

Déclaration de variable

```java
1 <Type de la variable> <Nom de la variable>
```
Il y a deux types de variables en Java

* Des variables de type simple ou "primitif" (Nombre entiers, réels, boléens ou string)
* Des variables de type complexe ou des "objets"

### Les variables

Une variable contient une valeur et, en java, doit être typée.

* Le type `int` concerne les varibales numériques
* Le type `boléen` true or false
* le type `char` est composé d'un seul charactère et s'écrit entre deux simples apostrophes 
    ```java
        public class Variables {
	public static void main(String[] args) {

		int myNumber=42;
		boolean isFun=true; 
		char movieRating='A'; 

	    }   
    }
    ```
    La suite des normes d'ériture est dans [OpenClassroom](https://openclassrooms.com/courses/apprenez-a-programmer-en-java/les-variables-et-les-operateurs)

* Modulo

    Le modulo en math retourne le reste d'une division de deux nombres.

    14 modulo (%) 6 renvera 2 (14/6 = 2*6 + 2)
    ```java
    public class Modulo {
        public static void main(String[] args) {

            int myRemainder = 14 % 6;
            System.out.println(myRemainder);

        }
    } 
    ```
* Les opérateurs

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
    | 

Les évalutations des boléens se font dans l'ordre :
    
    d'abord ! puis && puis ||

* Les conditions ternaires sont composées de trois parties
    
1. Une expression boléenne `(fuelLevel > 0) ?`
2. Une instruction unique exécutée si l'expression unique est vraie `'Y' :`
3. Une instruction unique exécutée si l'expression unique est fausse `'N' ;`

```java
public class Ternary {
	public static void main(String[] args) {
		
		int fuelLevel = 3;

		char canDrive =
		(fuelLevel > 0) ? 'Y' : 'N';
		System.out.println(canDrive);

	}
}
```
Renvoie

    Y

* Les conditions avec `Switch`
```java
public class Switch {
	public static void main(String[] args) {
		
		char penaltyKick = 'L';

		switch (penaltyKick) {

			case 'L': System.out.println("Messi shoots and scores!");
								break; 
			case 'R': System.out.println("Messi misses the goal!");
								break;
			case 'C': System.out.println("Keeper blocks his shoot!");
								break;
			default:
				System.out.println("Messi is in position...");

		}

	}
}
```
* Résumé de l'utilisation des classes et des méthodes (Code Cademy)
```java
class Dog extends Animal {
  
  int age;
	public Dog(int dogsAge) {
  	age = dogsAge;
  }
  
  public void bark() {
    System.out.println("Woof!");
	}
	
  public void run(int feet) {
    System.out.println("Your dog ran " + feet + " feet!");
	}
  
  public int getAge() {
    return age;
	}

	public static void main(String[] args) {
    
    Dog spike = new Dog(4);
    spike.bark();
    spike.run(40);
    int spikeAge = spike.getAge();
    System.out.println(spikeAge);
    spike.checkStatus();

	}
}
```
## Les tableaux en Java (ArrayList)

* ArrayList est une classe pré définie en Java
    ```java
    import java.util.ArrayList;

    public class Temperatures {
        
        public static void main(String[] args) {

        ArrayList<Integer> weeklyTemperatures = new ArrayList<Integer>();
            
            weeklyTemperatures.add(78);// Ajoute un élément dans le tableau
            weeklyTemperatures.add(67);
            weeklyTemperatures.add(89);

            System.out.println( weeklyTemperatures.get(1));
            // Affiche la température de l'index 1 soit 67

            // Parcoure le tableau et en affiche tous les éléments
                for (int j = 0; j < weeklyTemperatures.size(); j++) {
            
                    System.out.println(
                    weeklyTemperatures.get(j));
                }
            }
        }
    }
    ```

    1. Appel de la classe ArrayList : `import java.util.ArrayList;`
    2. Pour ajouter un élément dans un tableau on utilise la méthode  `add()`
    3. Pour accéder à un élément du tableau on utilise son index et la méthode `get(index)`

            System.out.println( weeklyTemperatures.get(1));
                }

        Donnera `67`

    4. Pour insérer un élément à un index précis utiliser la notation :

            weeklyTemperatures.add(1, 78);

        Ajoutera `78` à l'index `1` du tableau

    5. Dans la boucle `for` on utilisera la méthode `size` pour définir la longueur total du tableau

    6. Une boucle `for each` s'écrira

        ```java
        for (Integer temperature : weeklyTemperatures) {
                    System.out.println(temperature);
                }
        ```
* `HashMap` est une autre classe prédéfinie

    Le `HashMap` contient un ensemble de clés et une valeur pour chaque clé. Il permet de récupérer une valeur en appelant sa clé.

    ```java
    import java.util.HashMap;

    public class Restaurant {
        public static void main(String[] args) {
        
        // Crée un tableau avec une clé (String) et sa valeur (Integer)
        HashMap<String, Integer> restaurantMenu = new HashMap<String, Integer>();
        
        // Ajoute un élément dans le HashMap
        restaurantMenu.put("Turkey Burger",13);
        restaurantMenu.put("Naan Pizza", 11);
        restaurantMenu.put("Cranberry Kale Salad", 10);

        // La méthode get permet de récupérer la valeur avec la clé
        System.out.println(  restaurantMenu.get("Naan Pizza"));

        // Affiche la taille du tableau
        System.out.println(
            restaurantMenu.size());

            // Affiche les infos pour chaque élémet du tableau
            for (String item : restaurantMenu.keySet()) {

			System.out.println("A " + item + " costs " + restaurantMenu.get(item) + " dollars.");

		}

        }
    }
    ```

    1. Ajouter des éléments avec la méthode `.put("Key",value)`
    2. Pour récupérer des éléments on utilise la clé avec la méthode `.get("Key")`
    3. la méthode `.size()` permet de récupérer la longueur du tableau
    4. La méthode `.keySet()` retourne la liste des clés du tableau





# Créer un projet avec Maven

[Cours complet sur Openclassroom](https://openclassrooms.com/courses/organisez-et-packagez-une-application-java-avec-apache-maven/creez-votre-premier-projet-maven)

En respectant les conventions de Maven, on peut lui demander de générer un squelette de notre projet. Maven s'appuie sur des archétypes (des modèles).
Pour demander à Maven de générer un squelette simple, on peut utiliser l'archétype `quickstart`.

Ligne de commande à taper dans le répertoire de notre application :
```
mvn archetype:generate -DarchetypeArtifactId=maven-archetype-quickstart -Darchetype
```
Réponses à doneraux questions posées :

* groupld  : l'organisation qui porte le projet (exemple : org.exemple.demo)
* artifactld   : le Projet (exemple: Mon-appli)
* version (1.0-SNAPSHOT) : Laisser vide
* package (org.exemple.demo) : Laisser vide

Confirmer ce que l'on a saisi avec Y (yes)

## Les fichiers d'un projet Maven

le fichier de configuration du projet contient 
```
pom.xml
```
Le projet contient une arborescence de base : 
```
🗁 Mon-appli
├── 🗎 pom.xml
└── 🗁 src
    ├── 🗁 main
    │   └── 🗁 java
    │       └── 🗁 org
    │           └── 🗁 exemple
    │               └── 🗁 demo
    │                   └── 🗎 App.java
    └── 🗁 test
        └── 🗁 java
            └── 🗁 org
                └── 🗁 exemple
                    └── 🗁 demo
                        └── 🗎 AppTest.java
```

```
mvn package
```
Commande qui compile, exécuté les tests et génère un fichier JAR

## Glossaire POO

| Termes              | définition        | 
| -------------       |-------------      | 
| Objet               | Programme autosuffisant
| Classe       | Ensemble d'attributs et de méthodes (Moule de l'objet)    |
| Classe abstraite | Classe qui ne peut pas être instanciée |
| Classe concrète | Classe qui peut être instanciée pour créer un objet |
| Instance            |  *Instancier* une classe, c'est se servir d'une classe afin qu'elle crée un objet. Une instance est donc un objet |
| Attribut (ou propriétés)  | Un attribut est une variable de la classe|
| Méthodes            | Une méthode est une fonction de la classe |
| Héritage (Extend)| Création d'une classe fille qui récupère les attributs de la classe mère |
| Parent | Classe principale |
| Enfant | Classe qui hérite des attributs et méhodes de la classe parent |
| Interface | Classe 100% abstraite pouvant être utilisée par plusieurs enfants |
| Implements | Mot clé pour qu'une classe utilise une interface |
| Package | C'est le dossier où les classes sont rangées / Charger un package permet d'utiliser les classes qu'il contient  |
| Polymorphisme | Comportement d'une méthode qui peut être différent selon les situations  |
| Constructeur | Méthode appelée lors de la construction d'un objet |
| Getteur | Permet de récupérer les attributs de la classe |
| Setteur | Permet de modifier les attributs de la classe |
| Surcharger | Redéfinir une méthode dans une classe fille |
| Import | Mot clé permettant d'utiliser une classe d'un package différent  |
| Build | Processus couvrant toutes les étapes nécessaires à la création d'un "livrable" du projet |
| Final | Mot-clé indiquant qu'un élément ne peut être changé dans la suite du programme |
| Principe d'encapsulation | Seul le créateur de la classe peut la modifier. Avec des attributs privés l'accès à la classe est réservée |

## Exemples de syntaxe

* Définir un objet de type classe

    ```java

    public class Chien {

        private String nom;

        public void mange(Aliment aliment) {
           System.out.println("quelque chose à afficher");
        }

        ...
    }
    ```
* Définit un objet de type interface, qui spécifie un comportement
    ```java
    public interface Animal {

        String getNom();
        String getCri();
        int getAge()
        void mange(Aliment aliment);
        ...
    }
    ```
    NB : Une interface ne contient que des définitions, c'est-à-dire pas de code. 
* Indique qu'une classe implémente une(des) interface(s). 

    ```java
    public class Chien implements Animal {
        ...
    }
    ```
    NB : Une classe peut implémenter plusieurs interfaces, séparées alors par des virgules
    ```java
    public class Chien implements Animal, Serializable, Cloneable {
        ...
    }
    ```
    Lorsqu'une classe implémente une interface, elle doit en implémenter toutes les méthodes, sauf si elle est marquée abstract

