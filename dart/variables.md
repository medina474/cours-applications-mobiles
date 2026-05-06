+++
title = "Variables"
+++

Les variables sont des **références** vers des objets. La déclaration se fait avec ou sans typage.

```dart
void variables(int a) {
  String prenom = 'Albert';   // typage explicite
  var nom = 'Einstein';       // typage implicite par inférence
  const pays = 'France';      // constante compilée
  final int age = a;          // constante modifiable une seule fois
}
```

### Annotation de type

Une annotation de type est une déclaration explicite du type attendu pour une entité (variable, fonction, paramètre, etc.).

Il est préférable d’annoter explicitement, surtout dans des API ou des fonctions publiques.

## Types

Dart supporte les types suivant :

## Nombres

Il y a deux types de nombres, les deux représenté parsur 64 bits, les entiers `int` et les flottants `double`.

Chacun des deux types sont des enfant de la classes `num`.

Lors de l'utilisation du type `num` avec des constantes litérales il faut penser au point si on souhaite un double.

```
num x = 1;
if (x is double) print ('x est un double') else print ('x est un int');

num y = 1.0;
if (y is double) print ('y est un double') else print ('y est un int');
```

 Le type décimal n'existe pas.

```dart
print(0.2 + 0.1);
```

### Conversion

```dart
// String -> int
var un = int.parse('1');
var unVirguleUn = double.parse('1.1');

String unAsString = 1.toString();
String pi = 3.14159.toStringAsFixed(2);
```

## Chaines de caractères

Une chaîne Dart (objet `String`) contient une séquence de caractères UTF-16. Vous pouvez utiliser des guillemets simples `'` ou doubles `"` pour créer une chaîne litérale.

### Interpolation de chaine

Vous pouvez insérer la valeur d'une expression dans une chaîne en utilisant `${expression}`. Si l'expression est un identifiant simple, vous pouvez ignorer les accolades. Pour obtenir la chaîne correspondant à un objet, Dart appelle la méthode `toString()` de l'objet.

### Multiligne

Pour créer une chaîne multiligne, utilisez trois guillemets. (des simples ou des doubles)

var s1 = '''
Plusieurs lignes
de texte.
''';

### Chaines brutes

Vous pouvez créer une chaîne « brute » en la préfixant avec r. Les caractères habituels d'échappement ne sont plus échapés.

```dart
var s = r'Dans une chaine brute \n ne provoque pas de retour à la ligne.';
```

### Booléens

Pour représenter les valeurs booléennes, Dart utilise un type nommé bool. Seuls deux objets possèdent ce type : les littéraux booléens `true` et `false`, qui sont tous deux des constantes de compilation.


## Génériques

Un générique permet de paramétrer un type avec un ou plusieurs types spécifiques, afin d’écrire du code plus réutilisable et sûr, tout en conservant la vérification des types.

Une annotation de type générique permet de paramétrer le type que nous ne connaissons pas à l'avance. Le générique est un type en contrat d'intérim, qui attend qu'un vrai type vienne le remplacer. Par convention un type générique ne prend qu'une seule lettre comme T, E, K ou V.

Un type générique est placé entre `<>`.


## Symbol

Un objet Symbole représente un opérateur ou un identifiant déclaré dans un programme Dart. Vous n'aurez peut-être jamais besoin d'utiliser des symboles, mais ils sont précieux pour les API qui font référence aux identifiants par leur nom, car la minification modifie les noms des identifiants, mais pas leurs symboles.

## Null


#### Typage dynamique

En Dart, le mot-clé `dynamic` permet de déclarer une variable sans lui associer un type fixe. On retrouve le fonctionnement du langage JavaScript que l’on voulait justement éviter.

- Le compilateur n’impose aucun type.
- Le type peut changer à tout moment.
- Moins de sécurité de type (les erreurs sont détectées plus tard).
- Pas d’assistance de l’IDE (auto-complétion limitée).
- Plus difficile à maintenir dans les projets de grande taille.
- Il est souvent utilisé pour du code très flexible ou pour interagir avec du JSON.

```dart
dynamic valeur = 10;
valeur = 'texte';     // Autorisé
valeur = [1, 2, 3];   // Toujours autorisé
```

L’appel de méthodes ou de propriétés sur une variable dynamique ne sera vérifié qu’à l’exécution.

```dart
dynamic x = 'Bonjour';
print(x.length); // OK : String possède length

x = 42;
print(x.length); // Erreur d'exécution : int n’a pas de length
```

#### Constantes

En Dart, les mots-clés `final` et `const` servent tous deux à déclarer des valeurs immuables (en: immutable), mais ils ont des différences importantes en termes de moment d’évaluation et de comportement.

`final` : valeur définie une seule fois à l'exécution

- La variable peut être initialisée à l'exécution, mais une seule fois.
- Elle ne peut pas être modifiée ensuite.
- Elle peut dépendre de valeurs **calculées** à l’exécution. (Comme la date du jour par exemple)

`const` : valeur connue à la compilation

- La variable doit être déterminée au moment de la compilation.
- Elle est constante de bout en bout, et toutes ses sous-valeurs aussi.
- Elle est stockée en mémoire comme une constante compilée.

### Null safety

> Le null safety signifie que le compilateur garantit, à la compilation, qu’une variable ne pourra pas contenir null, sauf si elle est explicitement autorisée à le faire.

Ce programme ne peut être compilé, en effet le compilateur vérifie que la variable a été initialisée avant d'être utilisée.

```dart
String nom;
print(nom.length);
```

```dart
String nom;
nom = 'Albert';
print(nom.length); // La variable a été initialisée avant.
```

Suivant le contexte l'affectation n'est pas toujours garantie, un type nullable indique que la vriable peut ne pas être initialisée.

```dart
String? nom;
print(nom.length); // La variable n'a peut être pas été initialisée avant. Le compilateur refuse.
```

Il est nécessaire de tester avant le fait que la variable est non nulle.

```dart
String? nom;
if (nom != null) {
  print(nom.length); // La variable n'a peut être pas été initialisée avant. Le compilateur refuse.
}
```

#### null assertion

Je suis absolument sûr que la variable sera non nulle. On utilise l'opérateur null assertion `!.` pour forcer l'accès aux membres de l'objet.

```dart
String? nom;
print(nom!.length); // La variable n'a peut être pas été initialisée avant. Le compilateur refuse.
```

Si on s'est trompé est que la variable est nulle alors le programme plante !


inférence
: L’inférence (ou inférence de type) en Dart est la capacité du compilateur à déterminer automatiquement le type d’une variable ou d’une expression, sans qu’il soit nécessaire de le préciser explicitement. L'inférence fonctionne au moment de la compilation, pas à l'exécution. Le type ne peut pas changer ensuite.

typage dynamique
: Le typage dynamique signifie que le type d'une variable est déterminé à l’exécution, et peut changer au cours du programme.

mutable
: Un objet mutable permet de changer ses propriétés, ses éléments ou son contenu sans avoir à créer un nouvel objet.

immutable
: Un objet immutable est un objet dont l’état interne (valeurs, propriétés, contenu) ne peut jamais être changé une fois qu’il a été instancié.

cast
: Un cast (ou transformation de type) est une opération qui indique explicitement au compilateur qu’une valeur d’un type peut être considérée comme étant d’un autre type. C'est surtout utilisé en POO pour cibler un niveau précis dans une chaîne d'héritage de classes.
