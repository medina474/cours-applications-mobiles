# Boucles et instructions de contrôle

### Boucles `for`

Vous pouvez itérer avec une boucle `for` classique comme dans les autres langages.

```dart
var message = StringBuffer('Dart is fun');
for (var i = 0; i < 5; i++) {
  message.write('!');
}
```

Les fermetures (closures) à l'intérieur des boucles for de Dart capturent la valeur de l'index. Cela évite un piège courant rencontré en JavaScript. Par exemple :

```dart
var callbacks = [];
for (var i = 0; i < 2; i++) {
  callbacks.add(() => print(i));
}

for (final c in callbacks) {
  c();
}
```

La sortie est 0 et 1, comme attendu. Contrairement à JavaScript qui afficherait 2 et 2.

Parfois, vous n'avez pas besoin de connaître le compteur d'itération lorsque vous parcourez un type `Iterable`, comme une `List` ou un `Set`. Dans ce cas, utilisez une boucle `for-in`, plus lisible :

```dart
for (var candidate in candidates) {
  candidate.interview();
}
```

Dans l'exemple précédent, candidate est défini à l'intérieur du corps de la boucle et référence successivement chaque valeur de candidates. candidate est une variable locale. La réaffecter dans la boucle ne modifie que cette variable locale pour l'itération en cours et n'altère pas l'itérable candidates d'origine.

Pour traiter les valeurs obtenues depuis l'itérable, vous pouvez également utiliser un pattern dans une boucle for-in :

```dart
for (final Candidate(:name, :yearsExperience) in candidates) {
  print('$name has $yearsExperience of experience.');
}
```

Les classes implémentant Iterable disposent également d'une méthode `forEach()`

```dart
var collection = [1, 2, 3];
collection.forEach(print); // 1 2 3
```

# Boucles `while` et `do-while`

Une boucle `while` évalue sa condition **avant** chaque itération :

```dart
while (!isDone()) {
  doSomething();
}
```

Une boucle `do-while` évalue sa condition **après** l'exécution du bloc :

```dart
do {
  printLine();
} while (!atEndOfPage());
```

## `break` et `continue`

Utilisez `break` pour arrêter une boucle :

```dart
while (true) {
  if (shutDownRequested()) break;
  processIncomingRequests();
}
```

Utilisez `continue` pour passer directement à l'itération suivante :

```dart
for (int i = 0; i < candidates.length; i++) {
  var candidate = candidates[i];
  if (candidate.yearsExperience < 5) {
    continue;
  }
  candidate.interview();
}
```

Si vous utilisez un Iterable comme une liste ou un ensemble, Il convient de filtrer avant

```dart
candidates
    .where((c) => c.yearsExperience >= 5)
    .forEach((c) => c.interview());
```

## Étiquettes (Labels)

Une étiquette est un identifiant suivi de deux-points (nomEtiquette:) placé devant une instruction pour créer une instruction étiquetée.

Les boucles et les blocs switch sont souvent utilisés comme instructions étiquetées. Une instruction étiquetée peut ensuite être référencée dans une instruction break ou continue :

- `break nomEtiquette;` : termine l'exécution de l'instruction étiquetée. Cela permet notamment de sortir d'une boucle externe spécifique lorsqu'on se trouve dans des boucles imbriquées.

- `continue nomEtiquette;` : ignore le reste de l'itération en cours de la boucle étiquetée et passe directement à son itération suivante.

Les étiquettes servent à contrôler précisément le flux d'exécution. Elles permettent de choisir quelle boucle ou quel bloc doit être affecté, plutôt que d'agir par défaut sur la boucle la plus interne.

```dart
outerLoop:
for (var i = 1; i <= 3; i++) {
  for (var j = 1; j <= 3; j++) {
    print('i = $i, j = $j');
    if (i == 2 && j == 2) {
      break outerLoop;
    }
  }
}
print('outerLoop exited');
```

```dart
outerLoop:
for (var i = 1; i <= 3; i++) {
  for (var j = 1; j <= 3; j++) {
    if (i == 2 && j == 2) {
      continue outerLoop;
    }
    print('i = $i, j = $j');
  }
}
```
