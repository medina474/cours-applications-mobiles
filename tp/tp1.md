# TP 1 — Gestion d’état avec Riverpod et mise en cache locale

## Objectifs pédagogiques

À l’issue de ce TP, vous serez capables de :

* comprendre les limites de `FutureBuilder`
* comprendre l’intérêt d’un gestionnaire d’état
* utiliser **Riverpod**
* séparer :
  * l’interface graphique
  * la logique métier
  * l’accès aux données
* mettre en place un mécanisme de **fallback vers un cache local**
* gérer les erreurs réseau de manière élégante

---

# Contexte

Dans le TD précédent :

* vous avez créé une classe `Acteur`
* vous avez consommé une API REST
* vous avez affiché les données dans une `ListView`
* vous avez utilisé un `FutureBuilder`

L’application fonctionne… mais possède plusieurs limitations.

## Limites de l’approche précédente

Avec `FutureBuilder` :

* chaque widget gère lui-même son état
* la logique réseau se rapproche rapidement de l’interface
* il devient difficile :
  * de partager les données
  * de mettre les données en cache
  * de gérer des rechargements
  * de gérer plusieurs sources de données

## Les Gestionnaires d’état

Un gestionnaire d’état permet :

* de centraliser les données
* de centraliser la logique métier
* de découpler l’UI des sources de données

Dans ce TP, nous allons utiliser **Riverpod**

Riverpod est une bibliothèque Flutter moderne permettant :

* l’injection de dépendances
* la gestion d’état
* le partage de données
* la gestion simplifiée de l’asynchrone

## Nouvelle architecture

L’application devra désormais utiliser :

```
UI → Provider Riverpod → Repository → Sources de données
```

## Architecture attendue

```
lib/
├── models/
│   └── acteur.dart
├── services/
│   ├── acteur_api_service.dart
│   └── acteur_local_service.dart
├── repositories/
│   └── acteur_repository.dart
├── providers/
│   └── acteur_provider.dart
├── views/
│   └── acteur_view.dart
```


# Partie 1 — Mise en place de Riverpod

Ajouter la dépendance :

```yaml
flutter_riverpod:
```

Modifier le point d’entrée de l’application afin d’utiliser Riverpod.


---

# Partie 2 — Repository

Dans le TP précédent, le service API était directement utilisé par l’interface.

Nous allons désormais introduire un **Repository**

Le repository servira d’intermédiaire entre :

* l’application
* les différentes sources de données

Créer une classe `ActeurRepository`

Cette classe devra exposer :

```dart
Future<List<Acteur>> getActeurs()
```

# Partie 3 — Source distante

Créer un service `acteur_api_service.dart`

Ce service devra :

* appeler l’API distante
* transformer le JSON en objets `Acteur`

---

# Partie 4 — Cache local

## Problématique

Que se passe-t-il si :

* le serveur est indisponible ?
* le smartphone n’a plus de réseau ?

L’application ne doit pas devenir inutilisable.

## Objectif

Mettre en place un système de fallback :

```text id="m8y2pt"
API distante indisponible
            ↓
Chargement du cache local
```

Créer un service local : `acteur_local_service.dart`

Ce service simulera un cache local.

Pour simplifier ce TP, les données pourront être stockées :

* dans une variable mémoire
* ou dans un fichier JSON local

---

## Méthodes attendues

```dart
Future<void> saveActeurs(List<Acteur> acteurs)

Future<List<Acteur>> loadActeurs()
```

# Partie 5 — Fallback

Modifier le repository afin de :

1. tenter de charger les données depuis l’API
2. sauvegarder les données localement si succès
3. charger le cache local en cas d’erreur réseau


## Comportement attendu

```text
API OK
  → sauvegarde cache
  → affichage

API KO
  → lecture cache
  → affichage cache
```

# Partie 6 — Provider Riverpod

## Question 7

Créer un provider Riverpod permettant :

* d’exposer la liste des acteurs
* de gérer automatiquement :

  * loading
  * erreur
  * données

Utiliser : `FutureProvider`

# Partie 7 — Interface Flutter

Modifier `ActeurView` afin :

* d’utiliser Riverpod
* de supprimer le `FutureBuilder`
* d’utiliser : `ConsumerWidget`

Afficher :

* un loader pendant le chargement
* la liste des acteurs
* un message d’erreur si aucune donnée n’est disponible

