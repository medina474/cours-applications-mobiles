# TP Cartographie

> Créer une page contenant une carte avec des marqueurs pour localiser les établissements. Ajouter un menu tabbar pour naviguer entre la carte et la liste des acteurs.
{class=objectif}

Dans le fichier _pubspec.yaml_ ajouter les dépendances aux packages _flutter_map_ et _latlong2_

_pubspec.yaml_
```yml
  flutter_map: ^8.1.1
  latlong2: ^0.9.1
```

### Attributs d'état du widget

```dart
final MapController _mapController = MapController();
LatLng? _userLocation;
cList<Marker> _markers = [];
```

### Fonction pour determiner la position de l'utilisateur

```dart
Future<void> _determinePosition() async {
  bool serviceEnabled = await Geolocator.isLocationServiceEnabled();
  if (!serviceEnabled) return;

  LocationPermission permission = await Geolocator.checkPermission();
  if (permission == LocationPermission.denied) {
    permission = await Geolocator.requestPermission();
    if (permission == LocationPermission.denied) return;
  }

  if (permission == LocationPermission.deniedForever) return;

  final position = await Geolocator.getCurrentPosition();
  final userLatLng = LatLng(position.latitude, position.longitude);

  setState(() {
    _userLocation = userLatLng;
  });

  _mapController.move(userLatLng, 14);
}
```

### Récupérer via la Web service la liste des établissements dans une région donnée

```dart
Future<List<Feature>> getEtablissements(LatLngBounds bounds) async {
  final url =
      'http://localhost:3002/geojson/etablissements?bbox=${bounds.northWest.longitude},${bounds.northWest.latitude},${bounds.southEast.longitude},${bounds.southEast.latitude}';
  final response = await http.get(Uri.parse(url));
  final Map<String, dynamic> geojson = jsonDecode(response.body);
  return geojson["features"].map((e) => Feature.fromJson(e)).toList();
}
```

### Convertir la liste des établissements en liste de markers

```dart
    Future<void> _getMarkers() async {
      final bounds = _mapController.camera.visibleBounds;
      final etablissements = await getEtablissements(bounds);

      final markers =
          etablissements
              .map<Marker>(
                (e) => Marker(
                  point: LatLng(
                    e.geometry.coordinates[1],
                    e.geometry.coordinates[0],
                  ),
                  child: Icon(
                    Icons.location_on,
                    color: Colors.deepPurple,
                    size: 40,
                  ),
                ),
              )
              .toList();

      if (mounted) {
        setState(() {
          _markers = markers;
        });
      }
    }
```

- Écouter les mouvements de la carte (zoom/déplacement) avec onPositionChanged
- Récupérer les limites visibles (MapCamera.visibleBounds).
- Appeler service.fetch(bounds) avec ces limites.
- Afficher les markers correspondants.

```dart
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Carte")),
      body: FlutterMap(
        mapController: _mapController,
        options: MapOptions(
          initialCenter:
              _userLocation ?? LatLng(45.75, 4.85), // Centre de votre région
          initialZoom: 13,
          onMapReady: _getMarkers,
          onPositionChanged: (position, hasGesture) {
            _getMarkers();
          },
        ),
        children: [
          TileLayer(
            urlTemplate: 'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
            subdomains: ['a', 'b', 'c'],
            userAgentPackageName: 'com.example.cinema_app',
          ),
          MarkerLayer(markers: _markers),
        ],
      ),
    );
  }
}
```

### Debouncer

Un Debouncer (ou antirebond en français) est un mécanisme permettant de contrôler la fréquence à laquelle une fonction est exécutée, en retardant son appel jusqu'à ce qu’un certain délai se soit écoulé depuis la dernière invocation. Il est utile quand un événement peut se produire trop fréquemment et causer des problèmes de performance ou de surcharge.

- Chaque fois que l’événement se déclenche, le debouncer annule le précédent appel planifié.
- Il reprogramme l’appel à la fonction dans 300 ms.
- Si aucun nouvel événement ne survient dans ce délai, la fonction est finalement exécutée.

```dart
Timer? _debounce;

void onMapMoved(LatLngBounds bounds) {
  _debounce?.cancel();
  _debounce = Timer(Duration(milliseconds: 300), () {
    poiService.getEtablissements(bounds);
  });
}
```

### Annulation de requête

Utiliser le package _dio_ plus complet que le simple _http_

### Groupe de marquers

```yml
flutter_map_marker_cluster: ^1.4.0
```

> N'est pas compatible avec la dernière version de flutter_map. Les joies des packages tiers.
{class=danger}

- service.fetch() est déclenché sans await, donc l'exécution continue immédiatement après (le setState() et l'affichage de la carte ne sont pas bloqués).
- Le téléchargement des tuiles commence tout de suite.
- Une fois les données du service récupérées, on peut facultativement mettre à jour l’interface via setState() si on veut afficher les établissements (ex. des Marker).
- Ajouter une couche de type MarkerLayer.
- Rendre les marqueurs cliquables (GestureDetector).
- Afficher les infos dans un showDialog(), un BottomSheet, ou un widget flottant.
