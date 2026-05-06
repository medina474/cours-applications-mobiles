# Collections

## Listes

La collection la plus courante dans presque tous les langages de programmation est probablement le tableau, ou groupe ordonné d'objets. En Dart, les tableaux sont des objets de type liste ; la plupart des gens les appellent donc simplement listes.

Les littéraux de liste Dart sont représentés par une liste d'expressions ou de valeurs séparées par des virgules, entre crochets ([]).

```dart
var liste = [1, 2, 3];
```

En utilisant l'annotation de types

```dart
List<int> liste = [1, 2, 3];
```

Si la liste est vide et que l'on souhaite inférer.

```dart
var liste = <int>[];
```

Les listes utilisent une indexation de base zéro, où 0 est l'index de la première valeur et list.length - 1 celui de la dernière valeur. Vous pouvez obtenir la longueur d'une liste grâce à la propriété .length et accéder à ses valeurs grâce à l'opérateur d'indice ([]) :

## Sets

Dans Dart, un ensemble est une collection non ordonnée d'éléments **uniques**. La prise en charge des ensembles par Dart est assurée par les littéraux d'ensemble et le type Set<E>.

```dart
var halogenes = {'fluor', 'chlore', 'brome', 'iode', 'astate'}; // inférence avec un litéral
```

En utilisant l'annotation de types

```dart
Set<String> liste = {'fluor', 'chlore', 'brome', 'iode', 'astate'};
```

## Maps

En général, une map est un objet associant des clés (K) et des valeurs (V). Ces clés et valeurs peuvent être de n'importe quel type d'objet. Chaque clé n'apparaît qu'une seule fois, mais la même valeur peut être utilisée plusieurs fois. La prise en charge des map par Dart est assurée par les littéraux de carte et le type Map<K, V>.

```dart
var gifts = {
  'first': 'partridge',
  'second': 'turtledoves',
  'fifth': 'golden rings',
};

var nobleGases = {2: 'helium', 10: 'neon', 18: 'argon'};
```

En utilisant l'annotation de types

```dart
Map<String, String> gifts;
Map<int, String>  nobleGases;
```

Attention le literal vide `{}` correspond à une Map et non pas à un Set. Les deux utilisent l'accolade. Comme il n'y a rien à l'intérieur le compilateur ne peut pas savoir si il doit contenir des paires de clés/valeurs ou des valeurs seules.

### Spread operator

Dart prend en charge l'opérateur de propagation (...) et l'opérateur de propagation sensible aux valeurs nulles (...?) dans les littéraux de liste, de carte et d'ensemble. Les opérateurs de propagation offrent un moyen concis d'insérer plusieurs valeurs dans une collection.

Par exemple, vous pouvez utiliser l'opérateur de propagation (...) pour insérer toutes les valeurs d'une liste dans une autre liste :

```dart
var list = [1, 2, 3];
var list2 = [0, ...list];
```

### Control flow

Le control flow dans les listes en Dart est une fonctionnalité très expressive qui permet d’utiliser des structures de contrôle (if, for, etc.) directement à l’intérieur des littéraux de liste, pour construire dynamiquement des collections.

Créer une List en incluant des éléments sous condition (if) ou en générant des éléments par itération (for) — directement dans la déclaration de la liste.

```dart
bool estConnecté = true;

var menu = [
  'Accueil',
  if (estConnecté) 'Profil',
  'Contact',
];

print(menu); // ['Accueil', 'Profil', 'Contact']
```

```dart
var nombres = [for (var i = 0; i < 5; i++) i * i];

print(nombres); // [0, 1, 4, 9, 16]
```

### Itération

Boucle classique

```dart
var fruits = ['pomme', 'banane', 'cerise'];

for (var i = 0; i < fruits.length; i++) {
  print(fruits[i]);
}
```

for-in

```dart
for (var fruit in fruits) {
  print(fruit);
}
```

forEach

```dart
fruits.forEach((fruit) {
  print(fruit);
});
```

Pour les maps il ya trois itérations possibles : sur les clés, sur les valeurs, sur la paire clé-valeur.

```dart
var capitales = {
  'France': 'Paris',
  'Espagne': 'Madrid',
  'Italie': 'Rome',
};

for (var entry in capitales.entries) {
  print('${entry.key} → ${entry.value}');
}

for (var pays in capitales.keys) {
  print('Pays : $pays');
}

for (var capitale in capitales.values) {
  print('Capitale : $capitale');
}

capitales.forEach((pays, capitale) {
  print('$pays → $capitale');
});
```
