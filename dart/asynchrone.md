+++
title = "Programmation asynchrone"
+++

> La programmation asynchrone permet d’exécuter des tâches **non bloquantes**, c’est-à-dire de lancer une opération (comme une requête réseau ou une lecture de fichier) sans arrêter l'exécution du reste du programme en attendant que cette opération se termine.

## Future<T> — une promesse de valeur à venir

Un Future<T> représente une valeur ou un résultat qui sera disponible dans le futur, typiquement après une opération asynchrone (comme une requête HTTP, une lecture de fichier, etc.).

```dart
Future<String> fetchData() async {
  return 'Hello world';
}
```

Attention ce qui est renvoyé par la fonction n'est pas une chaine de caractères (String) mais une promesse (objet Future).

## async et await

Le mot-clé `async` transforme une fonction pour qu'elle retourne un Future.

Le mot-clé `await` suspend l’exécution jusqu’à ce que le Future soit résolu. Et c'est seulement lors de la résolution que la véritable valeur est lue.

## Exercice

Ajouter le package http à votre projet.

Récupérer les données JSON contenue à l'URL https://json-placeholder.mock.beeceptor.com/users

```dart
final uri = Uri.parse('https://json-placeholder.mock.beeceptor.com/users');
final response = await http.get(url);
```

Afficher (print) le texte brut

```dart
print (response.body);
```

Convertir le texte brut en format dynamique Map<String, dynamic>

```dart
final List<dynamic> data = jsonDecode(response.body);
```

Créer une classe qui reflete la structure json à l'aide du site https://quicktype.io/dart

```dart
class User {
  final int id;
  final String name;
  final String company;
  final String username;
  final String email;
  final String address;
  final String zip;
  final String state;
  final String country;
  final String phone;
  final String? photo;

  User({
    required this.id,
    required this.name,
    required this.company,
    required this.username,
    required this.email,
    required this.address,
    required this.zip,
    required this.state,
    required this.country,
    required this.phone,
    this.photo,
  });
```

Ajouter la méthode factory qui créé une classe à partir de l'objet Map<String, dynamic>

```dart
factory User.fromJson(Map<String, dynamic> json) {
  return User(
    id: json['id'],
    name: json['name'],
    company: json['company'],
    username: json['username'],
    email: json['email'],
    address: json['address'],
    zip: json['zip'],
    state: json['state'],
    country: json['country'],
    phone: json['phone'],
    photo: json['photo'],
  );
}
```
