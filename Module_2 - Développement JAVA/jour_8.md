# Jour 8 - Développement JAVA - Evaluation Blanche - utilisation de Stream et Collection - 22/02/2023

## Stream

L'utilisation de Stream permet de se concentrer sur l'essentiel (le résultat attendu et non la manière de l'obtenir) et de l'exprimer sous une forme expressive et succincte (paradigme déclaratif, se concentrer sur le quoi plutôt que le comment). 

### Vérifier si un élément ne correspond à aucun élément dans une liste: stream + noneMatch

1. Convertir la liste d'élements qu'on veut parcourir en Stream avec la méthode `stream()`
2. Utiliser la méthode `noneMatch()` qui prend une fonction (prédicat, lambda, callback) en paramètres à appliquer sur chaque élément de la liste
3. Cette fonction va prendre l'élement parcouru en paramètre et va vérifier une condition sur cet élément
4. Si la condition est fausse pour tous les éléments, la méthode `noneMatch()` renvoie `true`, sinon `false`

Dans l'exemple ci-dessous, on parcourt une liste de recette, à laquelle on applique la méthode `noneMatch()`. On demande si une des recettes a un nom qui correspond au nom reçu au paramètre. Si aucune recette trouvée, on obtient true, sinon false.

Sachant que pour l'instanciation d'une recette, il faut donner en argument une liste d'ingrédients, alors qu'on reçoit en paramètres un array d'ingrédients, on utilise `Arrays.stream(ingredients).toList()` pour convertir l'array reçu en paramètre en liste.

```
   public void addRecipe(String name, Author author, Ingredient[] ingredients) {
        if(this.recipes.stream().noneMatch(r -> r.getName().equalsIgnoreCase(name))) {
            this.recipes.add(new Recipe(name, author, Arrays.stream(ingredients).toList()));
        }
    }

```

### Vérifier si un élément correspond à un élément dans une liste: stream + anyMatch

1. Convertir la liste d'élements qu'on veut parcourir en Stream avec la méthode `stream()`
2. Utiliser la méthode `anyMatch()` qui prend une fonction (prédicat, lambda, callback) en paramètres à appliquer sur chaque élément de la liste
3. Cette fonction va prendre l'élement parcouru en paramètre et va vérifier une condition sur cet élément 
4. Si la condition est fausse pour tous les éléments, la méthode `anyMatch()` renvoie `false`, sinon `true`

Dans l'exemple ci-dessous, on parcourt une liste d'aliments, à laquelle on applique la méthode `anyMatch()` pour vérifier si l'aliment reçu en paramètre (plus précisement son nom) correspond à un aliment (plus précisement au nom d'un aliment) dans cette liste. Si aucun aliment trouvé, on obtient false, sinon true.

```
    public boolean existsIn(Food food) {
        return this.foods.stream().anyMatch(f -> f.getName().equalsIgnoreCase(food.getName()));
    }
```

### Concaténer des éléments en chaînes de caractères: stream + map + collect

1. Convertir une liste d'élements en Stream avec la méthode `stream()`
2. Mapper sur cette liste en appelant pour chaque entrée la méthode `toString()` (généralement override) pour les convertir en string
3. Concaténer les strings obtenues par des virgules avec la méthode `collect`

```
    public String toString() {
        String result = this.name + " par " + this.author.getFirstname() + " " + this.getAuthor().getLastname() + " : ";
        result += this.ingredients.stream().map(Ingredient::toString).collect(Collectors.joining(", "));
        return result;
    }
    
```

### Récupérer un ou une liste d'éléments précis: stream + filter

1. Convertir la liste d'élements qu'on veut parcourir en Stream avec la méthode `stream()`
2. Utiliser la méthode `filter()` qui retourne les éléments du stream correspondant à la fonction Prédicat fournie en paramètre. Cette fonction va vérifier une condition sur chacun des éléments et retourner ceux qui l'affirment.

Dans l'exemple ci-dessous, on parcourt une liste de recettes pour ne récupérer que les recettes dont un des ingrédients (classe fille d'aliments) correspond à un aliment du frigo reçu en argument:
- on convertit la liste en stream
- on applique la méthode filter à qui on demande de retourner toutes les recettes dont le nom d'un des ingrédients existe dans le frigo reçu en argument (pour rappel, une recette dispose d'une liste d'ingrédients et un frigo une liste d'aliments. Les ingrédients héritent des aliments et de leur attributs nom, ils ont donc le même nom)
- ensuite, pour ne récupérer que la première recette, on utilise la méthode `findFirst()`
- si le stream est vide (aucun ingrédient n'existe dans le frigo), on demande de retourner null avec la méthode `orElse`


```
    public Recipe searchBy(Fridge fridge) {
        return this.recipes.stream().filter(
                (Recipe r) -> r.getIngredients().stream().anyMatch(fridge::existsIn)
        ).findFirst().orElse(null);
    }
```

Dans l'exemple ci-dessous, on parcourt une liste de recette et on souhaite récupérer les recettes dont l'auteur correspond à l'auteur reçu en argument:
- on convertit la liste en stream
- on applique la méthode filter à qui on demande de retourner toutes les recettes dont le nom et prénom de l'auteur correspond au nom et prénom de l'objet author reçu en paramètre (pour rappel, l'objet recette a un attribut auteur correspondant à un objet author)
- ensuite, on transforme le stream obtenu en liste

```
    public List<Recipe> writedBy(Author author) {
        return this.recipes.stream().filter(
                (Recipe r) -> r.getAuthor().getFirstname().equals(author.getFirstname())
                        && r.getAuthor().getLastname().equals(author.getLastname())
        ).collect(Collectors.toList());
    }
```

## Collections

### Supprimer des éléments qui répondent à une certaine condition: Colletions + removeIf

La méthode `removeIf` est une méthode qui s'applique aux objects Collections. Elle permet de supprimer des éléments d'une collection qui répondent à une condition précise.
Cette méthode parcourt notre collection. Elle prend en paramètre une fonction (prédicat) qui elle-même prend paramètre l'élement parcouru et renvoie le résultat d'une condition qu'on précise. Si la condition est satisfaire pour l'élement parcouru, il est donc supprimé, sinon elle ne fait rien.

```
    public void remove(Food food) {
        this.foods.removeIf(f -> f.getName().equalsIgnoreCase(food.getName()));
    }

```
