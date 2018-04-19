# Memo - JAVA - JDBC
## *Campus Numérique 2018 - Véronique*
#
## Ressources en ligne

* [Open Class-Room](https://openclassrooms.com/courses/apprenez-a-programmer-en-java/jdbc-la-porte-d-acces-aux-bases-de-donnees)

* `JDBC` signifie `Java DataBase Connectivity`
* JDBC permet à des programmes Java de communiquer avec des bases de données.

## Créer une connexion avec MySQL

1. Récupérer le driver JAVA MySQL sur le site d'Oracle
```
mysql-connector-java-5.1.46.zip
```
2. Décompresser l'archive et récupérer le fichier bin.jar
```
mysql-connector-java-5.1.46-bin.jar
```
3. Le placer dans le répertoire `/lib/ext` présent dans le dossier d'installation du `JRE` (Sous C://Programmes)

*A noter* : Si l'application doit être exportée sous plusieurs postes, il est préférable de l'ajouter au `CLASSPATH`

4. Ajouter le code de connexion dans le `main`
* Créer une Classe Connect
* Ne pas oublier les import 
```
import java.sql.Connection;
import java.sql.DriverManager;
```
```java
public class Connect {
    public static void main(String[] args) {
        // Procédure levant une exception e cas de problème de connexion (mot de passe invalide...)
        try {
            Class.forName("com.mysql.jdbc.Driver");
            System.out.println("Driver OK !");
            // Url de connexion qui doit toujours commancer par JDBC +  le type de BDD
            // + Localisation de la machine physique + le port utilisé (à trouver directement dans MySQL)
            // + Nom de la base de donnée utilisée
            String url = "jdbc:mysql://localhost:3306/test-jdbc";
            String user = "root";
            String passwd = "";

            Connection conn = DriverManager.getConnection(url, user, passwd);
            System.out.println("Connexion effective !");

        } catch (Exception e) {
            e.printStackTrace();
        }
    }
```    
Cette procédure lève une exception en cas de problème (mot de passe invalide…).
5. Pour connecter IntelliJ avec le Driver installé
Aller dans
* File
* Project Structure 
    ```
    Ctrl + Alt + Maj + S
    ```
* Modules
* Dependencies
* Cliquer sur le +
* Jars or Directories
* Pointer sur le fichier .jar ajouté dans le jre ()

## Récupérer les données de la BDD MySQL

Création 
```java
//Création d'un objet Statement
            Statement state = conn.createStatement();

            //L'objet ResultSet contient le résultat de la requête SQL
            ResultSet result = state.executeQuery("SELECT * FROM personnage");

            //On récupère les MetaData
            ResultSetMetaData resultMeta = result.getMetaData();

            System.out.println("\n*********");

            //On affiche le nom des colonnes
            for(int i = 1; i <= resultMeta.getColumnCount(); i++)

                System.out.print("\t" + resultMeta.getColumnName(i).toUpperCase() + "\t *");

            System.out.println("\n*********");

            while(result.next()){

                for(int i = 1; i <= resultMeta.getColumnCount(); i++)

                    System.out.print("\t" + result.getObject(i).toString() + "\t |");

                System.out.println("\n*********");
            }

            result.close();
            state.close();
```
Les quatre étapes nécessaires à l'interrogation de la BDD :

1. Création de l'objet `Statement` ;

2. Exécution de la requête SQL ;

3. Récupération et affichage des données via l'objet `ResultSet` ;

4. Fermeture des objets utilisés (bien que non obligatoire, c'est recommandé).

**Nota** : Les `metadatas` (ou, plus communément, `les métadonnées`) constituent un ensemble de données servant à décrire une structure. Elles permettent de connaître ici le nom des tables, des champs, leur type…

L'objet de type `ResultSetMetaData` récupére les métadonnées de la requête, (ses informations globales). Cet objet est ensuite utilisé pour récupérer le nombre de colonnes renvoyé par la requête SQL ainsi que leur nom. Cet objet de métadonnées permet de récupérer des informations très utiles, comme :

* le nombre de colonnes d'un résultat ;
* le nom des colonnes d'un résultat ;
* le type de données stocké dans chaque colonne ;
* le nom de la table à laquelle appartient la colonne (dans le cas d'une jointure de tables) ;
* etc...


L'objet `Statement` (fourni par l'objet `Connexion` graca à l'instruction `conn.createStatement()`) permet d'exécuter des instructions SQL, il interroge la base de données et retourne les résultats. Ensuite, ces résultats sont stockés dans l'objet `ResultSet`, grâce auquel on peut parcourir les lignes de résultats et les afficher.

Les requètes SQL peuvent être de différents types :

* CREATE
* INSERT
* UPDATE
* SELECT
* DELETE

### Les méthode de l'objet ResultSet

Il existe une méthode getXXX() par type primitif ainsi que quelques autres correspondant aux types SQL :

* `getArray`(int colummnIndex)
* `getAscii`(int colummnIndex)
* `getBigDecimal`(int colummnIndex)
* `getBinary`(int colummnIndex)
* `getBlob`(int colummnIndex)
* `getBoolean`(int colummnIndex)
* `getBytes`(int colummnIndex)
* `getCharacter`(int colummnIndex)
* `getDate`(int colummnIndex)
* `getDouble`(int colummnIndex)
* `getFloat`(int colummnIndex)
* `getInt`(int colummnIndex)
* `getLong`(int colummnIndex)
* `getObject`(int colummnIndex)
* `getString`(int colummnIndex)

## 