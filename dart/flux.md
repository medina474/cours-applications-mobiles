+++
tile = "Contrôle de flux"
+++

## if

Dart prend en charge les instructions « if » avec des clauses « else » facultatives. La condition entre parenthèses après « if » doit être une expression dont l'évaluation donne un booléen

## if-case

Les instructions Dart if prennent en charge les clauses case suivies d'un modèle.

```dart
if (pair case [int x, int y]) return Point(x, y);
```

Si la valeur correspond au modèle, la branche s'exécute avec toutes les variables définies par le modèle dans la portée.

```dart
if (data is Map<String, Object?> &&
    data.length == 1 &&
    data.containsKey('user')) {
  var user = data['user'];
  if (user is List<Object> &&
      user.length == 2 &&
      user[0] is String &&
      user[1] is int) {
    var name = user[0] as String;
    var age = user[1] as int;
    print('User $name is $age years old.');
  }
}
```

```dart
if (data case {'user': [String name, int age]}) {
  print('User $name is $age years old.');
}
```

This case pattern simultaneously validates that:

    json is a map, because it must first match the outer map pattern to proceed.
        And, since it's a map, it also confirms json is not null.
    json contains a key user.
    The key user pairs with a list of two values.
    The types of the list values are String and int.
    The new local variables to hold the values are name and age.

Les motifs sont une catégorie syntaxique du langage Dart, comme les instructions et les expressions. Un motif représente la forme d'un ensemble de valeurs qu'il peut comparer à des valeurs réelles.

## Instruction switch

Une instruction switch évalue une expression de valeur par rapport à une série de cas. Chaque clause case est un modèle de correspondance de valeur. Vous pouvez utiliser n'importe quel type de modèle pour un cas.

Lorsque la valeur correspond au modèle d'un cas, le corps du cas s'exécute. Les clauses de cas non vides se terminent par un saut à la fin du commutateur après achèvement. Elles ne nécessitent pas d'instruction break. D'autres méthodes valides pour terminer une clause de cas non vide sont les instructions `continue`, `throw` ou `return`.

Utilisez une clause `_` par défaut ou générique pour exécuter du code lorsqu'aucune clause de cas ne correspond.

Les cas vides passent au cas suivant, ce qui permet aux cas de partager un corps. Pour un cas vide qui ne passe pas, utilisez `break` pour son corps. Pour un passage non séquentiel, vous pouvez utiliser une instruction `continue` et une étiquette :

Utilisez `default` ou le générique `_` pour exécuter du code lorsqu'aucune clause case ne correspond.

L'instruction switch suit la logique de programmation impérative.

```dart
var command = 'OPEN';
switch (command) {
  case 'CLOSED':
    executeClosed();
  case 'PENDING':
    executePending();
  case 'APPROVED':
    executeApproved();
  case 'DENIED':
    executeDenied();
  case 'OPEN':
    executeOpen();
  default:
    executeUnknown();
}
```

```dart
switch (command) {
  case 'OPEN':
    executeOpen();
    continue newCase; // Continue de s'exécuter sur l'étiquette newCase.

  case 'DENIED': // Un cas vide est pris en charge par le bloc suivant
  case 'CLOSED':
    executeClosed(); // Exécute pour DENIED et CLOSED,

  newCase:
  case 'PENDING':
    executeNowClosed(); // Exécute pour OPEN et PENDING.
}
```

## Expression switch

Une expression switch produit une valeur basée sur le corps de l'expression, quelle que soit la casse. Vous pouvez utiliser une expression switch partout où Dart autorise les expressions, sauf au début d'une instruction d'expression.

```dart
var x = switch (y) { ... };
```

Les instructions switch peuvent être réécrites avec une expression switch

```dart
// Where slash, star, comma, semicolon, etc., are constant variables...
var token;

switch (charCode) {
  case slash || star || plus || minus: // Logical-or pattern
    token = operator(charCode);
  case comma || semicolon: // Logical-or pattern
    token = punctuation(charCode);
  case >= digit0 && <= digit9: // Relational and logical-and patterns
    token = number();
  default:
    throw FormatException('Invalid');
}
```

devient

```dart
var token = switch (charCode) {
  slash || star || plus || minus => operator(charCode),
  comma || semicolon => punctuation(charCode),
  >= digit0 && <= digit9 => number(),
  _ => throw FormatException('Invalid'),
};
```

L'expression switch suit la logique de programmation déclarative.

### Clause de protection

Pour définir une clause de protection facultative après une clause case, utilisez le mot-clé `when`. Une clause de protection peut suivre une clause if case, ainsi que des instructions et expressions switch.

when agit comme un filtre supplémentaire après le pattern principal. Cela permet d’éviter des if imbriqués ou des cas dupliqués.

```dart
String getAccessLevel(User user) => switch (user.role) {
  'admin' when user.isActive => 'Full access',
  'admin' => 'Inactive admin',
  'user' when user.isActive => 'Limited access',
  'user' => 'Inactive user',
  _ => 'Unknown role',
};
```

```dart
final result = switch ((x, y)) {
  (var a, var b) when a + b > 10 => 'Sum is large',
  (var a, var b) => 'Sum is small or equal',
};
```
