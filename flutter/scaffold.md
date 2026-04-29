# Scaffold

La classe Scaffold (échafaudage) est un widget extensible qui remplit tout l'espace disponible ou l'écran. Il fournit des propriétés pour afficher les widgets utiles à une application tels que AppBar, Drawer, SnackBar, Bottom-Sheet, FloatingActionButton et BottomNavigationBar.

```dart
Widget build(BuildContext context) {
  return Scaffold(
    appBar: AppBar(
      title: const Text('Cinéma'),
    ),
    body: Center(child: Text(
      'Application Cinéma',
      style: TextStyle(fontSize: 40),)
    ),
    backgroundColor: Colors.blueGrey.shade200,
  );
}
```


**AppBar**, qui est une barre horizontale généralement affichée en haut d'une application à l'aide de la propriété appBar.

**BottomAppBar**, est une barre horizontale généralement affichée au bas d'une application à l'aide de la propriété bottomNavigationBar.

**FloatingActionButton**, qui est un bouton circulaire généralement affiché dans le coin inférieur droit de l'application à l'aide de la propriété floatingActionButton.

**Drawer**, qui est un panneau vertical généralement affiché à gauche du corps (et souvent masqué sur les téléphones) à l'aide de la propriété drawer.

**BottomNavigationBar**, qui est un tableau horizontal de boutons généralement affichés en bas de l'application à l'aide de la propriété bottomNavigationBar.

**SnackBar**, qui est une notification temporaire généralement affichée près du bas de l'application à l'aide de la méthode ScaffoldState.showSnackBar.

**BottomSheet**, qui est une superposition généralement affichée près du bas de l'application. Une feuille du bas peut être persistante, auquel cas elle est affichée à l'aide de la méthode ScaffoldState.showBottomSheet, ou modale, auquel cas elle est affichée à l'aide de la fonction showModalBottomSheet.

ScaffoldState, qui est l'état associé à ce widget.
statefull
