---
title: "UI"
---

## Commencez par penser de manière déclarative

Si vous êtes habitué à des langages et frameworks impératifs (tel que Android SDK ou iOS UIKit), vous devez commencer à penser au développement d'applications sous un nouvel angle.

De nombreuses hypothèses que vous pourriez avoir ne s'appliquent pas à Flutter. Par exemple, dans Flutter, vous pouvez reconstruire des parties de votre interface utilisateur à partir de zéro au lieu de la modifier. Flutter est assez rapide pour le faire, même sur chaque image si nécessaire.

Flutter est **déclaratif**. Cela signifie que Flutter construit son interface utilisateur pour refléter l'état actuel de votre application :

UI = f(state)

Lorsque l'état de votre application change (par exemple, l'utilisateur actionne un interrupteur dans l'écran des paramètres), vous modifiez l'état, ce qui déclenche un rafraîchissement de l'interface utilisateur. Il n'y a pas de changement impératif de l'interface utilisateur elle-même (comme widget.setText) - vous modifiez l'état et l'interface utilisateur se reconstruit **à partir de zéro**.

En savoir plus sur l'approche déclarative de la programmation de l'interface utilisateur dans le guide de démarrage.

Le style déclaratif de la programmation de l'interface utilisateur présente de nombreux avantages. Remarquablement, il n'y a **qu'un seul chemin de code** pour n'importe quel état de l'interface utilisateur. Vous décrivez à quoi devrait ressembler l'interface utilisateur pour un état donné, une fois, et c'est tout.

Au début, ce style de programmation peut ne pas sembler aussi intuitif que le style impératif.

## Scaffold

## Menu Tiroir

Dans un widget Scaffold la propriété drawer permet d'ajouter un objet widget de type menu tiroir.

Ajoutez maintenant un tiroir à l'échafaudage. Un tiroir peut être n'importe quel widget, mais il est souvent préférable d'utiliser le widget Tiroir de la bibliothèque de matériaux, qui respecte les spécifications de Material Design.

Maintenant que vous avez un tiroir en place, ajoutez-y du contenu. Pour cet exemple, utilisez un ListView. Bien que vous puissiez utiliser un widget Colonne, ListView est pratique car il permet aux utilisateurs de faire défiler le tiroir si le contenu prend plus d'espace que l'écran ne le prend en charge.

Remplissez le ListView avec un DrawerHeader et deux widgets ListTile. Pour plus d'informations sur l'utilisation des listes, consultez les recettes de listes.

## Widgets Stateless / Stateful


```
class _MyWidgetState extends State<MyWidget>
```

La classe du Widget doit dériver de la classe `State` mais en reprenant

```dart
import 'package:flutter/material.dart';

//This function triggers the build process
void main() => runApp(const MyApp());

// StatefulWidget
class MyApp extends StatefulWidget {
const MyApp({Key? key}) : super(key: key);

@override
// ignore: library_private_types_in_public_api
_MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
@override
Widget build(BuildContext context) {
  return MaterialApp(
  debugShowCheckedModeBanner: false,
  home: Scaffold(
    backgroundColor: Color.fromARGB(255, 230, 255, 201),
    appBar: AppBar(
    leading: const Icon(Icons.menu),
    backgroundColor: Colors.green,
    title: const Text(
      "GeeksforGeeks",
      textAlign: TextAlign.start,
    ),
    ), // AppBar
    body: const Center(
    child: Text(
      "StateFul Widget",
      style: TextStyle(color: Colors.black, fontSize: 30),
    ),
    ), // Container
  ), // Scaffold
  ); // MaterialApp
}
}
```
