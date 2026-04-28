+++
title = "Fonctions"
+++

Dart est un véritable langage orienté objet ; même les fonctions sont des objets et possèdent un type, Function. Cela signifie que les fonctions peuvent être assignées à des variables ou passées en arguments à d'autres fonctions. Vous pouvez également appeler une instance d'une classe Dart comme s'il s'agissait d'une fonction.

## Paramètres

Définition de fonctions avec ou sans paramètres

```dart
int addition(int a, int b) {
  return a + b;
}

void saluer(String nom) {
  print('Bonjour $nom');
}
```

### Paramètres positionnels

Les paramètres positionnels sont les paramètres classiques qui doivent être fournis dans un ordre précis lors de l'appel de la fonction. L'ordre des arguments doit correspondre à l'ordre des paramètres dans la définition de la fonction.

```dart
void saluer(String nom, int age) {
  print('Bonjour $nom, tu as $age ans.');
}

saluer('Alice', 30);  // ✅ Correct : 'Alice' est passé en 1er, '30' en 2ème
saluer(30, 'Alice');  // ❌ Erreur : l'ordre est incorrect
```

Dans ce cas là c'est facile pour le compilateur de détecter l'erreur car les types sont différents. Mais si les types sont identiques : nom, prénom par exemple. Comment savoir si l'on a fait une inversion ?

### Paramètres optionnels

Les paramètres positionnels optionnels sont des paramètres qui ne sont pas obligatoires, ils sont placés dans une liste entre crochets []. Si un paramètre n’est pas fourni, il prendra la valeur définie ou null par défaut.

```dart
void saluer([String prenom = 'Inconnu', String nom = 'Inconnu']) {
  print('Bonjour $prenom $nom');
}

saluer();  // ✅ Affiche : Bonjour Inconnu Inconnu
saluer('Alice');  // ✅ Affiche : Bonjour Alice Inconnu
```

```dart
void saluer(String nom, [int? age]) {
  print('Bonjour $nom, tu as ${age ?? 'un âge inconnu'}.');
}

saluer('Alice', 30);  // ✅ 'Alice' et '30' sont fournis
saluer('Bob');        // ✅ 'Bob' est fourni, age sera `null`
```

Dans l’argument positionnel facultatif, si nous ne transmettons pas la valeur, elle est définie sur null, il faut utiliser les types nullables.

###  Paramètres nommés

Les paramètres nommés permettent de passer des arguments à une fonction sans se soucier de leur position. Ils sont définis entre accollades {} et doivent être nommés lors de l'appel de la fonction. Ce sont des paramètres facultatifs. L'ordre n'a plus d'importance, seule la correspondance entre le nom du paramètre et la clé dans l'appel compte.

```dart
void saluer({String? prenom, String? nom}) {
  print('Bonjour ${prenom ?? 'Jean'} ${nom ?? 'Pierre'}');
}

saluer(prenom: 'Alice', nom: 'Dupont'); // ✅ Fonctionne, l'ordre n'a pas d'importance
saluer(nom: 'Dupont', prenom: 'Alice'); // ✅ Fonctionne, l'ordre n'a pas d'importance
```

Les paramètres nommés offrent un avantage lorsque plusieurs paramètres sont utilisés, car ils rendent les appels à la fonction plus lisibles et permettent de spécifier uniquement les paramètres nécessaires.

Le mot-clé `required` est utilisé pour rendre un paramètre obligatoire, même s’il est nommé.

```dart
void saluer({required String nom, int? age}) {
  print('Bonjour $nom, tu as ${age ?? 'un âge inconnu'}.');
}

saluer(nom: 'Alice', age: 30);  // ✅ Paramètres nommés
saluer(nom: 'Bob');             // ✅ L’ordre n’a pas d’importance
```

## fonctions lambdas

Les fonctions lambdas sont aussi appelées fonctions anonymes ou fonctions fléchées.

La fonction fléchée ne convient que si l’on a une seule expression (pas de blocs multiples, ni d'instructions complexes).

Elle est équivalente à une fonction courte sans bloc {} et avec return implicite.

```dart
var capitales = {
  'France': 'Paris',
  'Allemagne': 'Berlin'
};

capitales.forEach((pays, ville) => print('$ville est la capitale de $pays'));
```

La fonction anonyme est une fonction sans nom. il faut spécifier le return si cela est nécessaire.

```dart
nombres.forEach((n) {
  var double = n * 2;
  print(double);
});
```
