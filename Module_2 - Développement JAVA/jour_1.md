# Jour 1 - Développement JAVA - 13/02/2023

## Outils: 

- nodejs: via l'installation de nvm (https://github.com/coreybutler/nvm-windows) qui inclut une version node qui lui même inclut une version npm
- JDK: Environnement de compilation et d'exécution du code JAVA. Il inclut JRE (librairies pour exécution du code), JVM (environnement d'exécution)
- Maven: gestion des dépendances externes + cycle de vie et build des applications
- gitlab: préférence à github pour l'auto-hébergement des dépôts git

## JAVA:

### Utilisation sur bloc-notes

- Création d'un fichier `MaClasse.java`: le fichier doit porter le même nom que la classe qu'il contient
  
  public class MaClasse {
  
    public static void main (String[] args) {
      System.out.println ("Bonjour");
    }
  }

- Compilation du fichier avec la commande `javac NomDuFichier.java` (`javac MaClasse.java`). Cette commande crée un fichier avec l'extension `.class`
- Lecture du fichier avec la commande `java NomDeClasse` (`java MaClasse`)
- Packager en JAR (Java Archive), un archive des classes: `jar cfe MonArchive.jar MaClasse MaClasse.class`. Cela va créer un fichier jar
- Lancer le JAR avec la commande: `java -jar MonArchive.jar`


### Utilisation sur IntelliJ IDEA

- Creation du programme JustePrix 
- Découverte des méthodes Scanner et Math. Random() qui génère un nombre aléatoire
- Utilisation des boucles While ou Do While

### Architecture

- JDK : Outils de compilation
- JRE: Librairies de classes (pour l'exécution)
- JVM: Environnement d'exécution indépendant de l'OS

Il existe: 
- Garbage Collector: supprime automatiquement les espaces mémoires des variables non utilisées (Vs l'utilisation de pointeurs dans d'autres langages comme C, pour manipuler les données et libérer les espaces mémoires)
- Classpath: Variable qui définit la racine à partir de laquelle il faut chercher les chemins
- ClassLoader: Permet de charger les différentes classes

### Raccourcis clavier:

- Organiser le code: `Ctrl + Alt + L`
- Commenter une ligne: `Ctrl + / (du pavé numérique)`
- Commenter un bloc de code (multi-lignes): `Ctrl + Maj + / (du pavé numérique)`

## Evaluation:

Seront pris en compte:
- Qualité du code
- Java Doc
- Bonnes pratiques de nommage des fichiers, des variables et des paramètres
