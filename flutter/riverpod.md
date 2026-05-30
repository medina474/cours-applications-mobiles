# Riverpod

Quand on commence Flutter, on gère généralement l’état avec `setState()`. Mais le problème est que l’état est enfermé dans un widget qui est gère l'interface utilisateur.

- Chaque widget gère son propre état.
- La logique métier se retrouve éparpillée dans l’interface.
- Pour transmettre un état il faut le passer de widget en widget, c'eset le prop drilling

Riverpod est une bibliothèque de gestion d’état et d’injection de dépendances.

Son principe central est simple :

Toute donnée importante de l’application est exposée via un provider.

Un provider est un objet qui sait :

- comment créer une valeur
- comment la partager
- quand la reconstruire
- quand la détruire

Riverpod permet de séparer clairement :

- L’interface : Ce qui s’affiche
- La logique métier : Ce que l’application fait
- Les dépendances : Ce dont l’application a besoin

### 1 — Mise en place de Riverpod

Ajouter la dépendance :

```yaml
flutter_riverpod:
```

Modifier le point d’entrée de l’application afin d’utiliser Riverpod.

```dart
void main() {
  runApp(
    const ProviderScope(
      child: MyApp(),
    ),
  );
}
```

### Repository provider

```dart
final acteurRepositoryProvider = Provider<ActeurRepository>((ref) {
  return ActeurRepository();
});
```

Riverpod crée et fournit le repository

### Remplacer FutureBuilder par FutureProvider

```dart
final acteursProvider = FutureProvider<List<Acteur>>((ref) async {
  final repository = ref.watch(acteurRepositoryProvider);
  return repository.getActeurs();
});
```

Ce provider :

- récupère le repository
- appelle getActeurs()
- gère automatiquement l’état asynchrone

La vue n’a plus besoin d’être Stateful c'est maintenat Riverpod qui gère l'état.

```dart
class ActeurView extends ConsumerWidget {
  const ActeurView({super.key});

  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final acteursAsync = ref.watch(acteursProvider);

    return Scaffold(
      appBar: AppBar(
        title: const Text("Acteurs"),
      ),
      body: acteursAsync.when(
        loading: () =>
            const Center(child: CircularProgressIndicator()),

        error: (error, stackTrace) =>
            const Center(child: Text('Erreur de communication')),

        data: (acteurs) {
          if (acteurs.isEmpty) {
            return const Center(
              child: Text('Aucun acteur trouvé'),
            );
          }

          return ListView.builder(
            itemCount: acteurs.length,
            itemBuilder: (context, index) {
              final acteur = acteurs[index];

              return ListTile(
                title: Text(acteur.nom),

                subtitle: Text(
                  "${acteur.drapeauUnicode ?? ''} "
                  "${acteur.age ?? '?'} ans / "
                  "${acteur.nbFilm} films",
                ),

                leading: CustomCachedImage(
                  imageUrl:
                      "https://img.neotech.fr/cgi/images/tr:quality=50/"
                      "cinema%2fprofiles%2f${acteur.personneId}.jpg",
                  width: 42,
                  height: 42,
                  borderRadius: 21,
                  fit: BoxFit.cover,
                  errorWidget:
                      Image.asset('images/profile.jpg'),
                ),

                onTap: () {
                  Navigator.of(context).push(
                    MaterialPageRoute(
                      builder: (_) => RoleView(
                        personneId: acteur.personneId,
                        nom: acteur.nom,
                      ),
                    ),
                  );
                },
              );
            },
          );
        },
      ),
    );
  }
}
```

## NotifierProvider

Il permet de notifier des changement d'état.

Changer ActeurProvider en  AsyncNotifierProvider

```dart
final acteurProvider = AsyncNotifierProvider<ActeurNotifier, List<Acteur>>(
  ActeurNotifier.new,
);
```

Ajouter la classe `ActeurNotifier`. La méthode build est la méthode d'initialisation.

```dart
class ActeurNotifier extends AsyncNotifier<List<Acteur>> {

  @override
  Future<List<Acteur>> build() async {
    final repo = ref.read(acteurRepositoryProvider);

    final acteurs = await repo.getActeurs();
    return acteurs;
  }
}
```

Mettre en place la pagination sur le repository et le service Acteur.

Modifier la classe ActeurNotifier pour stocker l'état de la page.

```dart
  int _page = 1;
  bool _hasReachedEnd = false;
  bool _isLoadingMore = false;

  @override
  Future<List<Acteur>> build() async {
    final repo = ref.read(acteurRepositoryProvider);

    final acteurs = await repo.getActeurs(page: 1);

    _page = 1;
    _hasReachedEnd = acteurs.isEmpty;

    return acteurs;
  }
```

Ajouter une fonction permettant de modifier l'état c'est à dire de passer d'une page à l'autre

```dart
Future<void> loadMore() async {
    if (_hasReachedEnd || _isLoadingMore) return;

    _isLoadingMore = true;

    final repo = ref.read(acteurRepositoryProvider);

    final nextPage = _page + 1;

    try {
      final newActeurs = await repo.getActeurs(page: nextPage);

      final current = state.value ?? [];

      state = AsyncData([
        ...current,
        ...newActeurs,
      ]);

      _page = nextPage;
      _hasReachedEnd = newActeurs.isEmpty;
    } catch (e, st) {
      state = AsyncError(e, st);
    } finally {
      _isLoadingMore = false;
    }
  }
```

Finalement ajouter un inspecteur sur le scroll de la page et appeler la fonction loadMore du Notifier

```dart
NotificationListener<ScrollNotification>(
        onNotification: (scrollInfo) {
          if (scrollInfo.metrics.pixels >=
              scrollInfo.metrics.maxScrollExtent - 200) {
            ref.read(acteurProvider.notifier).loadMore();
          }
          return false;
        },
        child: acteursAsync.when(
```
