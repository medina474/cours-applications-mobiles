# Gestion des erreurs

Votre code Dart peut lever (*throw*) et intercepter (*catch*) des exceptions. Les exceptions sont des erreurs indiquant qu'un événement inattendu s'est produit. Si une exception n'est pas interceptée, l'isolat (*isolate*) qui l'a générée est suspendu et, dans la plupart des cas, l'isolat ainsi que son programme sont arrêtés brutalement.

Contrairement à Java, toutes les exceptions de Dart sont non vérifiées (unchecked exceptions). Les méthodes ne déclarent pas quelles exceptions elles peuvent lever et vous n'êtes pas obligé d'intercepter les exceptions.

Dart fournit les classes `Exception` et `Error`, ainsi que de nombreuses sous-classes prédéfinies. Un programme Dart peut lever n'importe quel objet non nul comme exception, pas uniquement des objets dérivés de `Exception` ou `Error`. Cependant il est préférable de définir vos propres exceptions dérivées des classes génériques.

## Lever une exception

Pour lever une exception il faut utiliser le mot-clé `throw`.

```dart
throw FormatException('Le format du n° de téléphone est incorrect');
```

Vous pouvez également lever des objets arbitraires comme une chaine de caractères (objet `String`).

```dart
throw 'Le format du n° de téléphone est incorrect';
```

> [!NOTE]
> Dans du code de qualité production, on lève généralement des objets qui implémentent Error ou Exception.

Comme la levée d'une exception est une expression, vous pouvez utiliser throw dans une expression fléchée (=>) ainsi que partout où une expression est autorisée :

```dart
void distanceTo(Point other) => throw UnimplementedError();
```

## Intercepter une exception

Intercepter une exception empêche sa propagation (sauf si vous la relancez explicitement). Cela vous donne l'occasion de la traiter. 

```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
}
```

Pour gérer plusieurs types d'exceptions, vous pouvez définir **plusieurs** clauses catch. La première clause correspondant au type de l'objet levé traitera l'exception. Si aucune clause ne précise de type, elle peut gérer n'importe quel objet levé :

```dart
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  buyMoreLlamas();
} on Exception catch (e) {
  print('Exception inconnue : $e');
} catch (e) {
  print('Objet inattendu : $e');
}
```

Comme le montre l'exemple précédent, vous pouvez utiliser :

- `on`
- `catch`
- ou les deux ensemble.

Utilisez `on` lorsque vous avez uniquement besoin de spécifier le type de l'exception à intercepter.

Utilisez `catch` lorsque votre gestionnaire doit accéder à l'objet exception lui-même.

Vous pouvez fournir un ou deux paramètres à catch(). Le premier correspond à lobjet exception levé et le second est la pile d'appels représentée par un objet `StackTrace`.

```dart
try {
  // ···
} on Exception catch (e) {
  print('Exception details:\n $e');
} catch (e, s) {
  print('Exception details:\n $e');
  print('Stack trace:\n $s');
}
```

Pour traiter partiellement une exception tout en la laissant se propager, utilisez le mot-clé `rethrow`

```dart
void misbehave() {
  try {
    dynamic foo = true;
    print(foo++); // Runtime error
  } catch (e) {
    print('misbehave() partially handled ${e.runtimeType}.');
    rethrow; // Allow callers to see the exception.
  }
}

void main() {
  try {
    misbehave();
  } catch (e) {
    print('main() finished handling ${e.runtimeType}.');
  }
}
```

## Bloc finally

Pour garantir qu'un morceau de code s'exécute qu'une exception soit levée ou non, utilisez une clause finally. Si aucune clause catch ne correspond à l'exception, celle-ci sera propagée **après** l'exécution du bloc finally.

```dart
try {
  breedMoreLlamas();
} finally {
  // Always clean up, even if an exception is thrown.
  cleanLlamaStalls();
}

```

La clause finally est également exécutée après toute clause catch correspondante :

```dart
try {
  breedMoreLlamas();
} catch (e) {
  print('Error: $e'); // Handle the exception first.
} finally {
  cleanLlamaStalls(); // Then clean up.
}
```

## Assertions `assert`

Pendant le **développement**, utilisez une instruction assert pour interrompre l'exécution normale du programme lorsqu'une condition booléenne est fausse.

```dart
assert(nom != null);
```

Pour associer un message à une assertion, ajoutez une chaîne de caractères comme second argument :

```dart
assert(
  text != null,
  'Le texte ne doit pas être nul',
);
```

The first argument to assert can be any expression that resolves to a boolean value. If the expression's value is true, the assertion succeeds and execution continues. If it's false, the assertion fails and an exception (an AssertionError) is thrown.

Dans le code de production, les assertions sont ignorées et les arguments passés à `assert()` ne sont même pas évalués.

Par conséquent, les assertions ne doivent jamais être utilisées pour exécuter une logique métier ou des validations indispensables au fonctionnement de l'application. Elles servent uniquement à détecter des erreurs de programmation pendant le développement.
