+++
title = "records"
+++

Les enregistrements sont un type d'agrégat anonyme et immuable. Comme les autres types de collections, ils permettent de regrouper plusieurs objets en un seul. Contrairement aux autres types de collections, les enregistrements sont de taille fixe, hétérogènes et typés.

Les enregistrements sont des valeurs réelles ; vous pouvez les stocker dans des variables, les imbriquer, les transmettre à et depuis des fonctions, et les stocker dans des structures de données telles que des listes, des maps et des ensembles (set).

### Records expressions

Les expressions d'enregistrements sont des listes délimitées par des virgules de champs nommés ou positionnels, placées entre parenthèses.

```dart
var record = ('premier', a: 2, b: true, 'dernier');
```

### Champs nommés

Dans une annotation de type d'enregistrement, les champs nommés sont placés à l'intérieur d'une section de paires type-nom délimitée par des accolades `{}`, après tous les champs positionnels. Dans une expression d'enregistrement, les noms précèdent chaque valeur de champ et sont suivis de deux points :

```dart
({int a, bool b}) record;

record = (a: 123, b: true);
```

### Annotation de types

Les annotations de type d'enregistrement sont des listes de types délimitées par des virgules et entre parenthèses. Elles permettent de définir les types de retour et les types de paramètres. Par exemple, les instructions (int, int) suivantes sont des annotations de type d'enregistrement :

```dart
(int, int) coordonnees;
```

### Destructuration

La destructuration permet d'extraire rapidement des élements d'un enregistrement et de les affecter à des variables distinctes.

```dart
(int, int) swap((int, int) record) {
  var (a, b) = record;
  return (b, a);
}
```

### Champs

Les champs d'enregistrement sont accessibles via des getters intégrés. Les enregistrements étant immuables, les champs n'ont pas de setters.

Les champs nommés exposent les getters du même nom. Les champs positionnels exposent les getters du nom $<position>, ignorant les champs nommés.

```dart
var record = ('premier', a: 2, b: true, 'dernier');

print(record.$1); // premier
print(record.a);  // 2
print(record.b);  // true
print(record.$2); // dernier
```
