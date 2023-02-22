# Jour 7 - Développement JAVA - Tests Unitaires et Méthode toString - 21/02/2023

## Tests Unitaires

### Ajout d'une dépendance Junit:

Dans le fichier `pom.xml` il faut ajouter la dépendence MAVEN sous les propriétés

```
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter</artifactId>
        <version>5.8.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```
On précise le scope du lifecycles de Maven, pour n'utiliser la dépendance que pendant ce scope (test dans notre cas).
Pour toute autre dépendance, on peut chercher le code Maven correspondan à ajouter dans MAVEN.

### Création d'un fichier test automatiquement:
- Se placer sur la classe qu'on souhaite tester
- Clic droit => Generate => test
- Choisir les méthodes à intégrer dans le test (Généralement, toutes les méthodes doivent soit avoir des paramètres, soit retourner une valeur)
- Pour créer un dossier regroupant les tests dans le dossier `src` (plutôt qu'un fichier de test au même niveau que la classe à tester):
	- Clic droit sur le dossier `src => New => Directory`
	- Choisir `test/java` qui sera proposé

### Création d'un mock
- Créer un package `mocks` dans le package des tests dans le dossier `test`
- Créer une classe à l'intérieur de ce package pour mocker le service souhaité (`RandomMock` par exemple) et qui étend la classe du service souhaité (`Random` par exemple) 
- Identifier la méthode du service utilisée dans notre code (comme `nextInt` de `Random`) et la surcharger (override)
```
public class RandomMock extends Random {

    @Override
    public int nextInt(int max) {
        return 50;
    }

    @Override
    public int nextInt(int min, int max) {
        return 50;
    }
}
```
- Utiliser la classe mockée pour les tests
```
    @Test
    void should_play_and_win() {
        Scanner scanner = new Scanner("93 75 80 90 50");
        RandomMock random = new RandomMock();

        JustePrix justePrix = new JustePrix(scanner, random);
        boolean winOrLoose = justePrix.play();

        assertFalse(scanner.hasNext()); // permet de vérifier si une autre entrée utilisateur existe après la fin du jeu
        assertTrue(winOrLoose); // permet de vérifier si l'utilisateur a gagné
    }
```

## Méthode toString():
Tout affichage d'un objet avec la méthode `System.out.println`, va exécuter la méthode `toString()` de cet objet pour l'afficher.
Par défaut, cette méthode affiche la référence de l'objet dans la mémoire
Il est possible de surcharger cette méthode, et ainsi l'affichage d'un objet avec la méthode `System.out.println` va pouvoir définir un affichage custom de l'objet.

- Sans override:
	`org.zenika.academy.tamagotchi.animals.Chat@20ad9418`
- Avec un override:
```
    @Override
    public String toString() {
        String result = """
                 /\\_/\\\s
                ( o.o )\s
                 > ^ <  \s""";
        result += this.hasPoop ? "Beurk !" : "";
        result += "\nSante : " + this.health + "/" + MAX_HEALTH
                + " | Faim : " + this.hanger + "/" + MAX_HANGER
                + " | Joie : " + this.happiness + "/" + MAX_HAPPINESS;
        return result;
    }
  ```
