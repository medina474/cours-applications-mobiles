# Navigation

La navigation dans une application Flutter fait référence au mécanisme permettant de passer d’un écran (ou "page") à un autre. En Flutter, les écrans sont représentés par des widgets, souvent des StatelessWidget ou StatefulWidget, qu'on appelle dans ce contexte des routes.

Flutter utilise un système de pile (stack) pour gérer la navigation. Lorsqu’un nouvel écran est affiché, il est empilé au-dessus de l’écran courant. Quand on revient en arrière, il est retiré de la pile (pop), et l’écran précédent réapparaît.

## Navigator

Flutter fournit le widget Navigator pour gérer la navigation :

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => NouvelEcran()),
);
```

Revenir à l'écran précédent

```dart
Navigator.pop(context);
```

Pour envoyer des données à l'écran suivant il suffit de passer les données au constructeur.

```dart
Navigator.push(
  context,
  MaterialPageRoute(builder: (context) => NouvelEcran(data: "Bonjour")),
);
```

Pour renvoyer des données à l'écran qui a fait l'appel. Ce dernier doit attendre avec le mot clé `await`

```dart
final resultat = await Navigator.push(...);
```

Pour renvoyer une donnée.

```dart
Navigator.pop(context, "résultat");
```

## Routes nommées

Flutter permet de définir des routes nommées pour centraliser la navigation. Les routes sont Définies dans l'objet MaterialApp.

```dart
MaterialApp(
  initialRoute: '/',
  routes: {
    '/': (context) => HomePage(),
    '/profil': (context) => ProfilPage(),
  },
);
```

Pour appeler une route nommée

```dart
Navigator.pushNamed(context, '/profil');
```

## Navigator 2.0

Dans le but de remplacer l'objet Navigator qui utilise une logique impérative, Flutter a introduit une nouvelle version avec un fonctionnement déclaratif.

Cette nouvelle version supporte aussi la navigation par url pour les applications web.

Le contôle de la pile est plus complet, la navigation n'est pas limité à des pas en avant et en arrière.

Cependant la prise en main est plus complexe.
