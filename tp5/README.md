# TP Cartographie

> Créer une page contenant une carte avec des marqueurs pour localiser les établissements cinématographiques. 


### Scaffold Carte

```dart
class CarteWidget extends StatefulWidget {
  const CarteWidget({super.key});

  @override
  State<CarteWidget> createState() => _CarteWidgetState();
}

class _CarteWidgetState extends State<CarteWidget> {
 
  @override
  void initState() {
    super.initState();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Carte")),
      body: FlutterMap(
```

### Afficher la carte

Dans le fichier _pubspec.yaml_ ajouter les dépendances aux packages `flutter_map` et `latlong2`.

- Ajouter FlutterMap comme widget principal du scaffold. 
- Utiliser Les tuiles d'OpenStreetMap comme fond de carte.
- Régler correctement la propriété `userAgentPackageName`

> [!CAUTION]
> On non-web platforms, the inadequately identified requests to the public OpenStreetMap tile servers are blocked

### Déterminer la position de l'utilisateur

Utiliser le paquet `geolocator` pour déterminer la position de l'utilisateur. 

- Tester l'application avec l'émulateur Android. 
- Vérifier que les permissions sont correctement définies dans le fichier `AndroidManifest.xml`.

```xml
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
```

### Récupérer via la Web service la liste des établissements dans une région donnée

propriété   |valeur
---         |---
méthode     | POST
url         | https://api.neotech.fr/rpc/etablissements_in_view
Content-Type| application/json
body        | { "min_lat": 47.5, "min_long": 6.5, "max_lat": 48.5, "max_long": 7.5 }

- Utiliser l'extension [Rest Client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) de VSCode pour visualiser le retour du web service
- Convertir la liste des établissements en liste de markers
- Écouter les mouvements de la carte (zoom/déplacement) avec `onPositionChanged`
- Récupérer les limites visibles (`MapCamera.visibleBounds`).
- Appeler service.fetch(bounds) avec ces limites.
- Afficher les markers correspondants.

### Debouncer

> Un Debouncer (ou antirebond en français) est un mécanisme permettant de contrôler la fréquence à laquelle une fonction est exécutée, en retardant son appel jusqu'à ce qu’un certain délai se soit écoulé depuis la dernière invocation. Il est utile quand un événement peut se produire trop fréquemment et causer des problèmes de performance ou de surcharge.

- Chaque fois que l’événement se déclenche, le debouncer annule le précédent appel planifié.
- Il reprogramme l’appel à la fonction dans 300 ms.
- Si aucun nouvel événement ne survient dans ce délai, la fonction est finalement exécutée.

```dart
import 'dart:async';

class Debouncer {
  Debouncer({required this.delay});

  final Duration delay;
  Timer? _timer;

  void run(void Function() action) {
    _timer?.cancel();
    _timer = Timer(delay, action);
  }

  void dispose() {
    _timer?.cancel();
  }
}
```

### Groupe de marquers

ajouter le paquet `flutter_map_marker_cluster`

- Rendre les marqueurs cliquables (GestureDetector).
- Afficher les infos dans un showDialog(), un BottomSheet, ou un widget flottant.

--

> [!NOTE]
> Cette partie n'a pas été réalisée

### Annulation de requête

Utiliser le package _dio_ plus complet que le simple _http_ qui permet l'annulation des requêtes