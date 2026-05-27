# TP Cartographie

> Créer une page contenant une carte avec des marqueurs pour localiser les établissements. Ajouter un menu tabbar pour naviguer entre la carte et la liste des acteurs.

Dans le fichier _pubspec.yaml_ ajouter les dépendances aux packages `flutter_map` et `latlong2`.

### Fonction pour determiner la position de l'utilisateur

Utiliser une fonction pour déterminer la position de l'utilisateur. 

Tester l'application avec l'emulateur Android. Vérifier que les permissions sont correctement définies.


### Récupérer via la Web service la liste des établissements dans une région donnée

POST https://api.neotech.fr/rpc/etablissements_in_view

Type de la requête

Content-Type: application/json

Corps de la requête POST

{ "min_lat": 47.5, "min_long": 6.5, "max_lat": 48.5, "max_long": 7.5 }

- Convertir la liste des établissements en liste de markers
- Écouter les mouvements de la carte (zoom/déplacement) avec onPositionChanged
- Récupérer les limites visibles (MapCamera.visibleBounds).
- Appeler service.fetch(bounds) avec ces limites.
- Afficher les markers correspondants.

### Debouncer

Un Debouncer (ou antirebond en français) est un mécanisme permettant de contrôler la fréquence à laquelle une fonction est exécutée, en retardant son appel jusqu'à ce qu’un certain délai se soit écoulé depuis la dernière invocation. Il est utile quand un événement peut se produire trop fréquemment et causer des problèmes de performance ou de surcharge.

- Chaque fois que l’événement se déclenche, le debouncer annule le précédent appel planifié.
- Il reprogramme l’appel à la fonction dans 300 ms.
- Si aucun nouvel événement ne survient dans ce délai, la fonction est finalement exécutée.

### Annulation de requête

Utiliser le package _dio_ plus complet que le simple _http_ qui permet l'annulation des requêtes

### Groupe de marquers

ajouter le paquet `flutter_map_marker_cluster`

- Rendre les marqueurs cliquables (GestureDetector).
- Afficher les infos dans un showDialog(), un BottomSheet, ou un widget flottant.
