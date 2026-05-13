# Travaux pratiques 1/4"
+++

## Application

_main.dart_
```dart
import 'package:flutter/material.dart';
import 'views/acteurs.dart';

void main() {
  runApp(const MainApp());
}

class MainApp extends StatelessWidget {
  const MainApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Cinéma',
      theme: ThemeData(primarySwatch: Colors.indigo),
      home: ActeursWidget(),
      debugShowCheckedModeBanner: true,
    );
  }
}
```

La classe `MaterialApp` est le point d'entréz visuel pour toute application Flutter qui suit les règles de design Material de Google (comme la plupart des applications Android modernes).

`title` définit le nom utilisé dans le sélecteur d’applications Android.

`theme` définit les couleurs, les polices, les formes de l'application.

`debugShowCheckedModeBanner` : Affiche une petite bannière "DEBUG" pour indiquer que l'application est en mode débogage. Elle est affichée par défaut en mode débogage, pour la cacher, mettre l'argument du constructeur à false. Cela n'a pas d'effet en mode release car la bannière ne s'affiche jamais.

`home` est l'écran de démarrage.

> C’est un socle prêt-à-l’emploi pour démarrer une app Flutter "à la Google", avec un bon look et un bon comportement.
{class=definition}

MaterialApp apporte aussi un système de navigation, de localisation (traduction) et de gestion des erreurs.

## Web service clients

```
http://api.neotech.fr/acteurs
```

### Classe modèle de données

Allez sur https://app.quicktype.io. Collez le résultat JSON en texte brut d'un élément et choisissez « Dart » comme langage.

Placez le résultat dans un fichier _acteur.dart_ dans un dossier _models_.

_models/acteurs.dart_
```dart
import 'dart:convert';

class Acteur {
  int personneId;
  String nom;
  String metaphone;
  DateTime? naissance;
  int? age;
  DateTime? deces;
  String? nationalite;
  String? drapeauUnicode;
  int nbFilm;
  double popularite;

  Acteur({
    required this.personneId,
    required this.nom,
    required this.metaphone,
    this.naissance,
    this.age,
    this.deces,
    this.nationalite,
    this.drapeauUnicode,
    required this.nbFilm,
    required this.popularite,
  });

  factory Acteur.fromJson(Map<String, dynamic> json) => Acteur(
    personneId: json["personne_id"],
    nom: json["nom"],
    metaphone: json["metaphone"],
    naissance: json["naissance"] != null ? DateTime.parse(json["naissance"]) : null,
    age: json["age"],
    deces: json["deces"] != null ? DateTime.parse(json["deces"]) : null,
    nationalite: json["nationalite"],
    drapeauUnicode: json["drapeau_unicode"],
    nbFilm: json["nb_film"],
    popularite: json["popularite"]?.toDouble(),
  );
}
```

Attention le ou les éléments qu vous choisissez ne sont peut-être pas représentatifs de l'ensemble des données. des valeurs nulles peuvent apparaître sans que cela soit prévu, à l'inverse des valeurs nulles ne pésagent pas de type de données.

### Méthode d'accès aux données

Écrire une fonction de service qui va demander au webservice les données, puis va les renvoyer typées.

```dart
Future<List<Acteur>> getActeurs() async {
  final response = await http.get('http://api.neotech.fr/acteurs');
  final data = jsonDecode(response.body) as List;
  return data.map<Acteur>((json) => Acteur.fromJson(json)).toList();
}
```

Cette fonction peut être mise directement dans le Widget ActeurView, c'est une solution rapide et fonctionnelle mais pas idéale.

```dart
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(title: Text("Acteurs"),),
    body: FutureBuilder<List<Acteur>>(
      future: futureActors,
      builder:
        (context, snapshot) => switch (snapshot.connectionState) {
          ConnectionState.waiting => Text("Attente des données"),
          ConnectionState.done => switch (snapshot) {
            _ when !snapshot.hasData => Text("Aucune donnée"),
            _ when snapshot.data!.isEmpty => Text("Aucun acteur trouvé"),
            _ => ,
          },
          _ => Text("Erreur"),
        },
    ),
  );
}
```
