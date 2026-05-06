# Layout

> [!NOTE]
> Les widgets sont des classes utilisées pour créer des interfaces utilisateur.

Les widgets sont utilisés à la fois pour les éléments de mise en page et d'interface utilisateur.
Assemblez des widgets simples pour créer des widgets complexes.

Les widgets sont au cœur du mécanisme de mise en page de Flutter. Dans Flutter, presque tout est un widget : même les modèles de mise en page sont des widgets. Les images, icônes et textes que vous voyez dans une application Flutter sont tous des widgets. Mais les éléments que vous ne voyez pas sont également des widgets, tels que les lignes, les colonnes et les grilles qui organisent, contraignent et alignent les widgets visibles.

Tous les widgets de mise en page présentent l'un des éléments suivants :

- Une propriété `child` s'ils prennent un seul enfant, par exemple, Center ou Container
- Une propriété `children` s'ils prennent une liste de widgets, par exemple Row, Column, ListView ou Stack.

