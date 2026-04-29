# Importation de bibliothèques

En Dart, l'importation de bibliothèques (ou "packages") permet de réutiliser du code défini ailleurs, que ce soit dans le SDK de Dart lui même, dans des bibliothèques tierces, ou dans vos propres fichiers.

L'importation se fait avec le mot-clé `import`.

```dart
import 'dart:math';
import 'package:http/http.dart' as http;
```

### pubspec.yaml

Le fichier **pubspec.yaml** est un fichier de configuration central dans tout projet Dart ou Flutter. Il définit les métadonnées du projet (titre), ainsi que ses dépendances, ressources, et paramètres de build.

### pub.dev

pub.dev est le gestionnaire de packages officiel pour Dart et Flutter. C'est une plateforme centrale où les développeurs publient, découvrent, téléchargent et documentent des packages open source.

Dans le fichier pubspec.yaml, il faut ajouter dans la section `dependencies` les packages à importer

```yaml
dependencies:
  http: ^1.3.0
```

Le symbole `^` dans un fichier pubspec.yaml sert à spécifier une contrainte de version compatible, selon les règles de versionnage sémantique (semver). Il permet de dire : "j'accepte cette version et toutes les versions compatibles suivantes, tant qu’il n’y a pas de changement majeur".

^1.2.3	signifie de prendre de télécharger la version comprise entre >=1.2.3 et <2.0.0
