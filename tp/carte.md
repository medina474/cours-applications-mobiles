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

>[!DANGER]
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

propriété|valeur
---      |---
méthode  | POST
url      | https://api.neotech.fr/rpc/etablissements_in_view
Content-Type| application/json
body     | { "min_lat": 47.5, "min_long": 6.5, "max_lat": 48.5, "max_long": 7.5 }

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

### Annulation de requête

Utiliser le package _dio_ plus complet que le simple _http_ qui permet l'annulation des requêtes

### Groupe de marquers

ajouter le paquet `flutter_map_marker_cluster`

- Rendre les marqueurs cliquables (GestureDetector).
- Afficher les infos dans un showDialog(), un BottomSheet, ou un widget flottant.

## Programmation avancée

### Gestion d’état avec Riverpod

L’objectif de cette partie est de restructurer l’application en séparant clairement :

* la récupération des données
* l’état de l’interface
* l’affichage

Ajouter la dépendance au paquet `Riverpod`

#### Création des providers

Créer les providers nécessaires pour gérer l’état de l’application :

#### Provider de localisation

Créer un provider chargé de :

- récupérer la position de l’utilisateur
- exposer un état de chargement
- gérer les erreurs de permission

#### Provider des établissements

Créer un provider asynchrone chargé de :

* récupérer la liste des établissements visibles
* exposer les états :

  * chargement
  * succès
  * erreur

Le provider devra recevoir en paramètre les limites visibles de la carte.

Exemple :

* latitude minimale
* latitude maximale
* longitude minimale
* longitude maximale

#### Provider des limites visibles

Créer un provider permettant de stocker dynamiquement les limites actuellement affichées sur la carte.

Mettre à jour ce provider lors des déplacements de la carte via `onPositionChanged`.

---

#### Utilisation dans l’interface

Modifier les widgets pour utiliser les providers.

Remplacer la logique locale (`setState`) par une consommation réactive avec :

* `ConsumerWidget`
* `ref.watch()`
* `ref.read()`

L’interface devra se mettre à jour automatiquement lors :

* d’un déplacement de carte
* d’un changement de position utilisateur
* d’une nouvelle récupération des établissements


## Mise en cache locale

L’objectif de cette partie est d’améliorer les performances de l’application en mettant en place une persistance locale.

Ajouter la dépendance au paquet `sembast`


### Création de la base locale

Créer une base locale permettant de stocker les établissements récupérés depuis l’API.

Créer :

* un service de base de données
* un store dédié aux établissements


### Sérialisation

Ajouter au modèle `Etablissement` :

* une méthode `toJson()`
* une méthode `fromJson()`

Ces méthodes permettront :

* l’enregistrement local
* la relecture depuis la base

### Sauvegarde automatique

À chaque récupération réussie depuis l’API :

* enregistrer les établissements dans la base locale
* remplacer les anciennes données

### Lecture depuis le cache

Lorsqu’une requête réseau échoue :

* charger les données depuis le cache local
* afficher les établissements disponibles

Afficher une indication visuelle précisant que les données proviennent du cache.

Exemple :

> Données hors ligne affichées

---

### Optimisation du cache

Mettre en place une stratégie d’expiration.

Exemple :

Les données sont considérées obsolètes après 15 minutes.

Si le cache est encore valide :

* afficher immédiatement les données locales
* éviter un appel réseau

Sinon :

* effectuer une nouvelle requête API


## Objectif pédagogique

Cette partie doit permettre de comprendre :

* la persistance embarquée
* la sérialisation d’objets
* la gestion d’un cache local
* les stratégies offline-first

---

## Défi final

Combiner Riverpod et Sembast pour mettre en place un fonctionnement **offline-first** :

1. Lire immédiatement les données du cache
2. Afficher les résultats
3. Rafraîchir silencieusement depuis l’API
4. Mettre à jour automatiquement l’interface si de nouvelles données sont disponibles

---

## Bonus expert

Mettre en place un provider unique orchestrant :

* lecture cache
* requête réseau
* synchronisation automatique
* invalidation du cache

Ce provider devra exposer un `AsyncValue<List<Etablissement>>`.

---

Ça introduit très naturellement une architecture Flutter moderne, cohérente avec ce que tu utilises déjà (Riverpod + persistance locale multiplateforme).

Ajouter un menu tabbar pour naviguer entre la carte et la liste des acteurs.
