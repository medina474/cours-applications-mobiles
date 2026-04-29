+++
title = "TD"
+++

Créer un Widget pour la liste des acteurs
nouveau fichier lib/acteurs.dart

Déclarer la classe avec le mot clé `class`

```dart
import 'package:flutter/material.dart';

class ActeursWidget extends StatefulWidget {
}
```

Déclarer le constructeur c'est une fonction avec le même nom que la classe

```dart
ActeursWidget({super.key});
```

Ajoutons un titre

Les variables ou fonctions qui commencent avec un _underscore_ _ sont **privés** à la classe

```dart
class ActeursWidget extends StatefulWidget {
  const ActeursWidget({super.key, required this.title});

  final String _title;
}
```

C'est un Widget statefull il manque donc la méthode createState


```dart
@override
  State<ActeursWidget> createState() => _ActeursWidgetState();
```

Maintenant il faut écire la classe _ActeursWidgetState

```dart
class _ActeursWidgetState extends State<ActeursWidget> {}
```

La méthode build créé et retourne l'interface utilisateur du widget

```dart
@override
  Widget build(BuildContext context) {
    return Scaffold()
  }
```

La fonction `setState` indique à la classe que l'état a changé est qu'il faut reconstruire (build) l'interface utilisateur
