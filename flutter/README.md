---
title: Flutter
---

Flutter est un **framework**, un ensemble d'outil pour développer des applications Web, Windows, Android et iOS à partir d'un socle commun.

Flutter est développé par Google c'est donc une alternative sérieuse et crédible aux développements d'applications natives.

Le langage utilisé est **[Dart](/dart)**, une tentative de remplacement de JavaScript qui utilise un **typage fort**.

Flutter reprend des concepts de React tout en les améliorant. Toute l'application est pensée en forme de Widget qui vont vivre et se rafraîchir de manière indépendante.

Les **widgets** : ils permettent de décrire simplement le rendu final. Chaque objet est défini indépendamment des contraintes parentes. C’est son emplacement dans le code qui permettra de définir ses contraintes extérieures. Cela permet de construire facilement son interface ; le code est alors plus facilement lisible et maintenable.

Les **composants** : ils ont été recréés par Google. Les développeurs disposent d’une galerie de composants s’adaptant à IOS comme Android, et aux différentes versions d’OS. Cependant une pléthore de composants hétéroclites quelque fois pas maintenu et conçus pour le même objectif ne rendent pas la tâche du développeur facile.

Une présentation en vidéo de Flutter https://www.youtube.com/watch?v=AEXIrThTgb0

### Un langage déclaratif

Programmation impérative
: La programmation impérative décrit comment accomplir une tâche. Le code suit une séquence d'instructions qui modifient l'état du programme étape par étape.

Programmation déclarative
: La programmation déclarative décrit ce qu’on veut faire, sans spécifier les étapes exactes. Le langage ou le moteur d’exécution décide comment y arriver.

Lorsqu’on utilise un style de programmation impératif, on modifie l’état de l’interface utilisateur manuellement à divers endroits du code, souvent en réponse à des événements. Cela peut mener à une situation où plusieurs parties du code changent la couleur du titre indépendamment, ce qui rend difficile de savoir quelle est réellement la couleur du titre à un instant donné. Le style impératif nécessite donc une attention constante à la cohérence de l’état.

```dart
Text title = Text('Bienvenue');

// À un moment donné :
title.style = TextStyle(color: Colors.red);

// Puis ailleurs dans le code :
if (isDarkMode) {
  title.style = TextStyle(color: Colors.white);
}

// Encore plus loin dans une autre méthode :
if (user.isPremium) {
  title.style = TextStyle(color: Colors.gold);
}
```

Ici, on modifie directement la couleur depuis plusieurs endroits du code.
À la fin, on ne sait pas quelle règle a prévalu : rouge, blanc ou doré ?

En programmation déclarative, on ne modifie pas directement l’élément UI. On décrit ce que doit être la couleur en fonction de l’état actuel du système. Le framework (comme Flutter) s’occupe de reconstruire la vue en conséquence. Cela garantit une source de vérité unique et une logique facile à raisonner.

```sql
Widget build(BuildContext context) {

  Color titleColor = switch ((user.isPremium, isDarkMode)) {
    (true, _) => Colors.gold,
    (false, true) => Colors.white,
    (false, false) => Colors.red,
  };

  return Text(
    'Bienvenue',
    style: TextStyle(color: titleColor),
  );
}
```

Ici, la couleur est entièrement déterminée par l’état du système (user, isDarkMode).
Elle est définie à un seul endroit, et tout changement d’état entraînera une reconstruction cohérente de l’interface.

Programmation déclarative :
- L’interface est décrite comme une fonction de l’état UI = f(state).
- L'arbre de widgets est reconstruit à chaque changement d’état.
- Le moteur du framework s’occupe de la différence et du rendu.

## Installation de Flutter

[installation](installation)


**Flutter Packages :** Utilisez des packages Flutter tiers provenant de pub.dev pour ajouter des fonctionnalités à votre application. Assurez-vous de vérifier la qualité et la popularité des packages avant de les intégrer dans votre projet.

[https://flutter.dev/](https://flutter.dev/)

## Anatomie d'un projet Flutter

fichier/dossier|description
---|---
.dart_tool|Cache interne utilisé par l’outil Dart pour stocker des métadonnées (ne pas modifier).
.idea|Paramètres spécifiques à l'IDE Android Studio. Pas essentiel au projet lui-même.
android|Contient les projets natifs Android (Kotlin/Java). Autogénéré, modification à la marge.
ios|Contient le projets natifs iOS (Swift/Objective-C).  Autogénéré, modification à la marge.
lib|Contient tous les fichiers sources de l'application.
linux|
macos|
test|Contient les tests unitaires et les tests widget.
web|
windows|
.gitignore|
.metadata|
analysis_options.yaml|
cinema_flutter.iml|
pubspec.lock| Fichier généré automatiquement qui verrouille les versions exactes des dépendances installées. Ne pas modifier. À versionner pour assurer des builds reproductibles.
pubspec.yaml| Fichier central de configuration de ton projet Flutter. Liste les dépendances (dependencies), les assets (images, fonts), et les plugins. Permet de nommer le projet, définir la version, etc.
README.md|

## Widgets

Les **Widgets** sont les éléments de base de toute interface utilisateur Flutter. Il est recommandé d'utiliser les widgets fournis par Flutter autant que possible pour créer une interface utilisateur efficace et réactive.

Flutter fonctionne comme un **arbre** de widgets. Chaque widget peut en contenir d'autres.

#### Exercice

Créer une application sur le modèle d'Empty Application.

Étudier la structure et le code source.


```dart
import 'package:flutter/material.dart';

void main() {
  runApp(const MainApp());
}

class MainApp extends StatelessWidget {
  const MainApp({super.key});

  @override
  Widget build(BuildContext context) {
    return const MaterialApp(
      home: Scaffold(
        body: Center(
          child: Text('Hello World!'),
        ),
      ),
    );
  }
}
```

### Widget MaterialApp

Le widget MaterialApp est le point d’entrée principal d’une application Flutter utilisant le design Material (le langage visuel de Google). Il encapsule toute la configuration de l'application : thème, navigation, localisations, titre, etc.

MaterialApp est un widget de haut niveau qui configure une application Flutter selon les principes du design Material.

Il fournit :

- Un thème visuel (couleurs, typographies, boutons, etc.)
- Une navigation avec des routes
- Un titre pour les systèmes d’exploitation
- La gestion de la localisation (langues)
- Des transitions, des effets d’ombre, des animations, etc.

### Widget Scaffold

Le widget Scaffold est un conteneur de base pour l'interface utilisateur d'une application Flutter Material Design. Il définit les grandes zones d’UI qu’on retrouve dans la majorité des applications.  Il fournit la structure visuelle classique d'une page d'application : barre d'app, tiroir, fond, bouton flottant, etc.

### Widget Center

Le widget Center est un widget de mise en page qui place son enfant au centre à la fois horizontalement et verticalement dans l’espace qui lui est alloué.

### Widget Text

Le widget Text en Flutter sert à afficher une chaîne de caractères (du texte) à l’écran. C’est l’un des widgets les plus fondamentaux de l’interface utilisateur.

## Concepts

[Les états](state.md)
[La navigation](navigation.md)

[introduction](introduction.md)
[composants](composants.md)
[ui](ui.md)
[future](future.md)
[carte](carte.md)
[barcode](barcode.md)
