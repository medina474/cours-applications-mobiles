# Travaux dirigés 1

## Consommation d’une API REST et modélisation en Dart

On souhaite développer une application Flutter qui affiche une liste d’acteurs récupérée depuis le service web suivant :

https://api.neotech.fr/acteurs

Ce service retourne un JSON de la forme :

```json
[
  {
    "personne_id": 1003,
    "nom": "Jean Reno",
    "metaphone": "JNRN",
    "naissance": "1948-07-30",
    "age": 77,
    "deces": null,
    "nationalite": "fr",
    "drapeau_unicode": "🇫🇷",
    "nb_film": 10,
    "popularite": 144.789
  }
]
```

## Partie 1 – Création de la classe `Acteur`

### Question 1

Identifier les types des champs de la structure JSON :

clé JSON | type
---|---
`personne_id` |int
`nom`         |String
`naissance`   | DateTime
`age`|
`deces`|
`popularite`|

### Question 2

Créer une classe Dart `Acteur` avec :

* des attributs **typés** correspondant au JSON
* en utilisant les conventions Dart (`camelCase`)

> [!INFO]
> ***camelCase*** : Convention de nommage dans laquelle les mots composant une phrase ou une expression sont fusionnés en un seul terme sans espaces, et chaque mot débute par une majuscule à l'exception du premier.

exemple `personne_id` devient `personneId`.

### Question 3 – Constructeur

Créer un constructeur avec :

* **paramètres nommés**
* mot-clé `required` lorsque nécessaire

**Objectif** : pouvoir instancier proprement un acteur :

```dart
Acteur(
  personneId: 1003,
  nom: "Jean Reno",
  age: 77,
  ...
);
```

### Question 4 – Paramètres optionnels

Certains champs peuvent être absents ou nuls.

Adapter votre classe pour gérer ce cas.


## Partie 2 – Du JSON vers l’objet

Problème Le JSON reçu est une `Map<String, dynamic>`. Comment transformer cela en objet `Acteur` ?

### Question 5 – Méthode de conversion

Créer une méthode permettant de construire un `Acteur` à partir d’un JSON.

Deux approches sont possibles :

* constructeur classique
* ou **constructeur factory**

### Rappel : constructeur factory

Un constructeur `factory` :

* ne crée pas forcément directement l’objet
* peut contenir de la logique
* retourne une **instance** de la classe

```dart
factory Acteur.fromJson(Map<String, dynamic> json) {
  return Acteur(
    personneId: json['personne_id'],
    nom: json['nom'],
    ...
  );
}
```

### Question 6

Implémenter :

```dart
factory Acteur.fromJson(Map<String, dynamic> json)
```

* convertir la date (`String` en `DateTime`)
* gérer les `null`
* gérer les `double`

---

## Partie 3 – Appel du service web

### Question 7

Ajouter la dépendance HTTP au projet Flutter.

### Question 8

Créer une fonction :

```dart
Future<List<Acteur>> fetchActeurs()
```

Cette fonction doit :

1. appeler l’API
2. décoder le JSON
3. transformer chaque élément en `Acteur`


```dart
final List data = json.decode(response.body);
```

---

# Partie 4 – Interface Flutter

### Question 9

Créer un `StatefulWidget` qui :

* appelle `fetchActeurs()` dans `initState`
* stocke le résultat dans un `Future`

### Question 10

Utiliser un `FutureBuilder` pour :

* afficher un loader pendant le chargement
* afficher une erreur si nécessaire
* afficher la liste des acteurs

### Question 11

Afficher chaque acteur dans un `ListTile` avec :

* nom
* âge
* nombre de films
* drapeau


## Les films

https://api.neotech.fr/equipes?personne_id=eq.31&select=alias,films(film_id,titre)