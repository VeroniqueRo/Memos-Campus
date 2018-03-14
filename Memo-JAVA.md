# Memo - JAVA
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

[Nom du lien](https://docs.docker.com/).

## Définitions

`Java` est un langage de programmation développé par *Sun Microsystems* (aujourd'hui racheté par *Oracle*) dont la plus grande force est son excellente portabilité (Une fois créé, il fonctionnera aussi bien sous Windows, Mac ou Linux).

`Java` est un langage typé et compilé orienté objet.

`JDK (Java Developpement Kit)` est l'outil de compilation nécessaire à la programmation en Java

`JRE (Java Runtime Environnement)` est l'outil indispensable pour l'utilisation de programme en Java

## Utilisations

* des `applications`, sous forme de fenêtre ou de console.
* des `applets` : des programmes incorporés à des pages web.
* des `applications mobiles`, avec J2ME.

## Installation

JDK doit être installé et le chemin vers JDK doit être ajouté dans le PATH => 
```
C:\Program Files\Java\jdk1.8.0_161\bin
```

Si JRE et JDK sont présents dans les variables d'environnement (PATH) JDKdoit être placé avant JRE.

Dans la console, `javac` doit être accessible et afficher les infos suivantes :

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

### Les variables de type numérique

* Le type `byte` (1 octet) peut contenir les entiers entre 
-128 et +127
    ```java
    byte temperature;
    temperature = 64;
    ```
* Le type `short` (2 octets) contient les entiers compris entre -32768 et +32767
    ```java
    short vitesseMax;
    vitesseMax = 32000;
    ```
* Le type `int` (4 octets) va de -2*109 à 2*109 (2 avec 9 zéros)
    ```java
    int temperatureSoleil;
    temperatureSoleil = 15600000; //La température est exprimée en kelvins
    ```
* Le type `long` (8 octets) peut aller de −9×1018  à 9×1018.
    ```java
    long anneeLumiere;
    anneeLumiere = 9460700000000000L;
    ```
    NB : Il faut impértivement ajouter un L à la fin du nombre sinon le complateur  ne compilera pas

* Le type `float` (4 octets) est utilisé pour les nombres avec une virgule flottante.
    ```java
    float pi;
    pi = 3.141592653f;
    ```
    ou
    ```java
    float pi;
    pi = 3.141592653f;
    ```
    NB : Il faut utiliser un point plutôt qu'une virgule



    La suite des normes d'ériture est dans [OpenClassroom](https://openclassrooms.com/courses/apprenez-a-programmer-en-java/les-variables-et-les-operateurs)