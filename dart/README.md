> [!NOTE]
> Dart est un langage de programmation conçu par **Google** en 2011. Il est surtout connu pour son rôle dans le développement d'applications mobiles multiplateformes grâce au framework applicatif **Flutter**.

Initialement, Dart visait à offrir une **alternative à JavaScript**, jugé trop permissif et difficile à maintenir, pour le développement d'applications web de grande envergure.

Dart a été créé pour surmonter certaines limitations de JavaScript, un langage déjà bien établi mais qui, selon les développeurs, ne pouvait plus évoluer pour résoudre certains problèmes.

### Caractéristiques de Dart :

Syntaxe Familière : Si vous connaissez déjà des langages comme Java, C# ou JavaScript, vous trouverez la syntaxe de Dart familière.

Typage Statique et Dynamique : Dart supporte à la fois le typage statique (pour une meilleure performance et sécurité) et le typage dynamique (pour plus de flexibilité).

Gestion de la Mémoire : Dart utilise un ramasse-miettes (garbage collector) pour la gestion automatique de la mémoire.

Compilation AOT et JIT : Dart peut être compilé à l'avance (Ahead-Of-Time, AOT) pour des performances optimales, ou juste à temps (Just-In-Time, JIT) pour un développement rapide.

Comme Dart visait à remplacer javascript au sein des navigateurs, il a été possible dés le départ de le transpiler en javascript. Il était prévu que les navigateurs non mis à jour puisse executer du Dart par le biais du transpilage.

Pour la documentation et en savoir plus : https://dart.dev/

***transpiler***  
Un transpiler est un outil logiciel qui convertit du code source écrit dans un langage de programmation en code source dans un autre langage de programmation. Contrairement à un compilateur, qui traduit généralement du code source en code machine exécutable, un transpiler transforme le code d'un langage de haut niveau à un autre langage de haut niveau.

***JIT***  
La compilation **Just-In-Time** est une technique utilisée par certains environnements d'exécution pour convertir du code source ou du bytecode en code machine exécutable au moment de l'exécution, plutôt qu'avant l'exécution.

***AOT***  
La compilation **Ahead-Of-Time** est une technique de compilation où le code source est traduit en code machine exécutable avant son exécution. La compilation AOT se fait généralement lors de la phase de construction de l'application.

## Présentation du langage

### Fonction principale main()

Chaque application Dart a pour point d'entée la fonction `main`.

```dart
void main() {
  print('Bonjour, Dart !');
}
```

- [Variables](variables.md)
  - [Records](records.md)
  - [Collections](collections.md)
- [Iteration](iteration.md)
- [Contrôle de flux](flux.md)
- [Fonctions](fonctions.md)
- [Classes et objets](class.md)
- [Importation de bibliothèques](package.md)
- [Programmation asynchrone](asynchrone.md)
