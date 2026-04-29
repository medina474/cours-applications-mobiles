# Classes

Une classe est un modèle (ou plan) pour créer des objets.
Elle définit des propriétés (attributs) et des comportements (méthodes).

```dart
class Personne {
  String nom = "inconnu";
  int age = 0;

  void sePresenter() {
    print('Bonjour, je m\'appelle $nom et j\'ai $age ans.');
  }
}
```

Pour instancier une classe il n'est pas nécessaire d'utiliser le mot clé `new`.

```dart
void main() {
  var p1 = Personne();
  p1.nom = 'Alice';
  p1.age = 30;
  p1.direBonjour(); // Bonjour, je m'appelle Alice et j'ai 30 ans.

  var p2 = new Personne();
  p2.nom = 'Robert';
  p2.age = 70;
  p2.direBonjour(); // Bonjour, je m'appelle Alice et j'ai 30 ans.
}
```

### Constructeur

Un constructeur est une méthode qui permet d’instancier une classe avec des valeurs dès le départ. La méthode n'a pas de type de retour parce que c'est implicitement le type classe en question et elle est nommé identiquement à la classe.

```dart
class Personne {
  String nom = "inconnu";
  int age = 0;

  Personne(String nom, int age) {
    this.nom = nom;
    this.age = age;
  }
}
```

Le mot-clé `this` est un référent explicite à l’instance courante d'une classe.
Il est utilisé pour accéder aux attributs ou méthodes de l'objet en cours, notamment lorsque des noms identiques sont utilisés avec des paramètres ou variables.

Si le corps du constructeur ne contient que des affectations this on peut utiliser un raccourcis entre le paramètre du constructeur et l'attribut de la classe.

```dart
class Personne {
  String nom;
  int age;

  Personne(this.nom, this.age);
}
```

Il n'est plus nécessaire de donner des valeurs par défaut ou de rendre nullable les attributs car le compilateur sait que les attributs seront obligatoirement affectés par le constructeur.

### Constructeurs nommés

Un constructeur nommé est une variation du constructeur standard d'une classe. Il crée directement une instance de la classe concernée.

En principe, les possibilités offertes avec les paramètres optionnels du constreur sont suffisantes pour gérer les cas particuliers. Cependant, il peut être pratique d’en posséder plusieurs et de leur donner un nom afin de rendre leur utilité plus explicite.

```dart
class Personne {
  String? nom;
  int age;

  Personne({this.nom, required this.age});
  Personne.anonyme(this.age);
}

var p1 = Personne(age: 18);
var p2 = Personne.anonyme(18);
```

L'attribut nom étant optionnel, il n'y a aucune différence dans l'utilisation du constructeur nommé. Seule la lisibilité du code est améliorée.

### liste d’initialisation

La liste d'initialisation est appelée avant le corps du constructeur. Cela permet d'avoir des atttributs déclarés `final` mais sans être des paramètres du constructeur.

```dart
class Personne {
  String? nom;
  int age;

  Personne({this.nom, required this.age});
  Personne.anonyme(this.age) : nom = 'Anonyme';
}
```

L'intéret est de pouvoir initialiser des attributs privés ou d'utiliser des calculs dans l'initiaisation, ce qui n'est pas possible avec des paramètres ou un corps de fonction.

### Accessibilité

Tout identifiant (classe, attribut, fonction...) est public par défaut.

Pour rendre un élément privé, il suffit de préfixer son nom par un _ (underscore). Mais il n'est privé qu'au niveau du fichier (library) pas dans la classe en elle même.

- Une variable _interne définie dans a.dart ne sera pas visible dans b.dart même si elle fait partie de la même classe importée.
- En revanche, deux classes dans le même fichier peuvent accéder aux membres privés l’une de l’autre.

### Getters/setters

```dart
class Carré {
  double _côté;

  Carré(this._côté);

  double get aire => _côté * _côté;

  set côté(double valeur) {
    if (valeur > 0) {
      _côté = valeur;
    }
  }
}
```

### Héritage

L'annotation @override permet de redéfinir une méthode héritée.

```dart
class Animal {
  void parler() => print('Un bruit');
}

class Chien extends Animal {
  @override
  void parler() => print('Wouf !');
}
```

annotation
: Une annotation en Dart est un métadonnée qui précède une déclaration (classe, méthode, variable, etc.) et informe le compilateur ou certains outils qu’un comportement particulier est attendu.

### La classe mère

`super` représente la classe mère.

Le constructeur d'un classe peut appeler le constructeur de la classe mère y faisant référence et en transmettant les paramètres (ici key) reçus.

```dart
class MonWidget extends StatelessWidget {
  const MonWidget({Key? key}) : super(key: key);
}
```

Peut s'écrire de manière plus concise en

```dart
class MonWidget extends StatelessWidget {
  const MonWidget({super.key});
}
```

### Factory

le mot-clé factory permet de définir un constructeur particulier, qui ne crée pas nécessairement une nouvelle instance chaque fois qu’il est appelé. À la différence d'un constructeur nommé, il peut retourner une instance existante ou différente.

C’est un mécanisme souple, utile pour :

- retourner une instance existante (singleton, cache),
- appliquer une logique conditionnelle à la création,
- retourner une sous-classe,
- ou masquer certains détails d’instanciation.

L'exemple le plus courant est la création d'objet à partir d'une variable JSON.

```dart
class Personne {
  final String nom;
  final int age;

  Personne(this.nom, this.age);

  factory Personne.fromJson(Map<String, dynamic> json) {
    return Personne(json['nom'], json['age']);
  }
}

var p = Personne.fromJson({'nom': 'Alice', 'age': 30});
```

Les fonctions factory ne peuvent pas accéder à `this`.

#### Object

C’est la superclasse de tous les types en Dart.

Il offre une interface minimale (comme toString() et hashCode).

Contrairement à dynamic, le compilateur vérifie les accès aux membres. Il ne permet d’accéder qu’aux méthodes définies dans Object (c'est à dire pas grand chose). Pour accéder aux méthodes de l'objet il faut faire un cast explicite.

```dart
Object valeur = 'Bonjour';

print(valeur.length);  // Erreur à la compilation : `Object` ne connaît pas `length`

print((valeur as String).length); // OK après un cast
```

#### as/is

L'opérateur as permet de faire un cast explicit.

```dart
num x = 10;
int y = x as int; // Cast explicite
```

L'opérateur is permet de tester le type d'une variable.

```dart
if (valeur is String) {
  print(valeur.length); // Le cast n'est plus nécessaire, le compilateur comprend ici que valeur est une String
}
```
