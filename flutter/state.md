+++
title = "Widgets Stateless / Stateful"
+++

## Stateless Widget

Les widgets stateless sans état sont idéaux pour représenter des parties de votre interface utilisateur qui ne changent pas en fonction des interactions des utilisateurs ou des mises à jour des données. Ils sont couramment utilisés pour afficher du contenu statique, tel que des en-têtes, des étiquettes, des icônes ou des images. Des exemples de widgets sans état incluent Text, Icon et Image.

Les widgets staleless sont sans état. Cela ne veut pas dire qu'ils ne sont pas complexes. Les widgets staleless **ne sont pas interractifs** mais ils peuvent contenir des widget stateful qui eux sont interractifs.

Un Widget **Stateless** : les widgets dont l'état **ne peut pas** être modifié une fois construits sont appelés widgets sans état. Ces widgets sont immuables une fois qu'ils sont construits, c'est-à-dire que tout changement dans les variables, les icônes, les boutons ou la récupération de données ne peut pas changer l'état de l'application.

Le widget sans état remplace la méthode build () et renvoie un widget. Par exemple, nous utilisons Text or the Icon est notre application flutter où l'état du widget ne change pas dans le runtime. Il est utilisé lorsque l'interface utilisateur dépend des informations contenues dans l'objet lui-même. D'autres exemples peuvent être Text, RaisedButton, IconButtons.

## Stateful Widget

D'un autre côté, un widget Stateful représente une partie de l'interface utilisateur qui peut changer au fil du temps ou en réponse aux interactions de l'utilisateur. Ces widgets sont mutables et peuvent être mis à jour dynamiquement.

Caractéristiques des widgets avec état :

État mutable : les widgets avec état peuvent maintenir un état interne mutable, qui peut changer au fil du temps. Cet état est généralement stocké dans un objet distinct appelé objet « State ».

Méthode de construction (build) : comme les widgets sans état, les widgets avec état ont également une méthode de construction. Cette méthode définit l’apparence et la structure initiales du widget.

Objet d'état : les widgets avec état sont **associés** à un objet d'état mutable. Cet objet State est responsable du stockage et de la gestion de l’état interne du widget.

Capacité de reconstruction : les widgets avec état peuvent demander une reconstruction de leur interface utilisateur lorsque leur état interne change. Cela les rend adaptés aux composants dynamiques de l’interface utilisateur.

Un widget Stateful est un widget avec état, ce qui signifie qu'il possède un objet State (défini ci-dessous) qui contient des champs qui **affectent** son apparence.


En Flutter, lorsqu’on utilise un StatefulWidget, on travaille avec deux classes étroitement liées :
- Le widget lui-même (StatefulWidget). Il ext immuable
- Son état mutable associé (State<T>). Contient l’état mutable. Gère les changements visuels.

### State

**State** : l'état est l'information qui peut être lue de manière synchrone lorsque le widget est construit et qui peut **changer** pendant la durée de vie du widget.

L'état d'une application peut très simplement être défini comme tout ce qui existe dans la mémoire de l'application pendant que l'application est en cours d'exécution. Cela inclut tous les widgets qui maintiennent l'interface utilisateur de l'application, y compris les boutons, les polices de texte, les icônes, les animations, etc. Alors maintenant que nous savons quels sont ces états, plongeons directement dans notre sujet principal, à savoir quels sont ces widgets avec et sans état et comment diffèrent-ils les uns des autres.

En d'autres termes, l'état du widget est la donnée des objets que ses propriétés (paramètres) entretiennent au moment de sa création (lorsque le widget est peint à l'écran). L'état peut également changer lorsqu'il est utilisé, par exemple lorsqu'un widget CheckBox est cliqué, une coche apparaît sur la case.

La classe State est la configuration de l'état. Il contient les valeurs (dans ce cas le titre) fournies par le parent (dans ce cas le widget App) et utilisées par la méthode build de l'État. Les champs d'une sous-classe de widget sont toujours marqués « final ».

createState() crée l’objet State quand le widget est inséré dans l’arbre.

Le widget peut être reconstruit plusieurs fois (hot reload, changement de parent, etc.)

L’instance de State garde la mémoire (counter) entre chaque reconstruction. L’objet State persiste tant que le widget reste dans l’arbre.

setState() est l’outil principal pour provoquer une mise à jour de l’UI.

Quand on appelle setState(() { ... }) dans le State :

- Flutter marque le widget comme sale (dirty).
- Il **reconstruit** le widget en appelant la méthode `build()`.
- L’interface se met à jour avec les nouvelles données.

### StatefulWidget décrit ce que le widget est.

Même si la classe StatefulWidget paraît vide, elle joue un rôle structurel crucial :

Flutter s'appuie sur les widgets immuables pour comparer deux versions de l’arbre de widgets et savoir s’il faut conserver le State existant ou le recréer.
Autrement dit :

- Deux StatefulWidget avec les mêmes données (clé, constructeur) → conservent le même objet State

Sinon → le State est détruit et un nouveau est créé

Ce que la classe StatefulWidget contient :

- Les paramètres transmis par l’extérieur
- La méthode createState() pour créer l’objet State

 Pourquoi ne pas tout mettre dans une seule classe ?

Parce que :

Le widget est immuable, mais l’état ne l’est pas

Flutter doit pouvoir recréer une instance du widget et décider s’il garde ou non son State

La séparation clarifie le cycle de vie (création, montée, mise à jour, destruction)

### key

À quoi sert la clé `key` en Flutter ?

Une Key est un **identifiant unique** que Flutter utilise pour savoir si deux widgets sont les "mêmes" dans l’arbre de rendu.

- Sans clé : Flutter se base uniquement sur la position dans l’arbre → possible erreurs lors des mises à jour.
- Avec clé : Flutter peut mieux gérer les reconstructions et préserver le bon State


> StatefulWidget décrit ce que le widget est.
State<T> est la classe qui gère comment il évolue dans le temps.
setState() est la méthode qui provoque une demande de mise à jour de l’UI.


Mutable
:  Un objet mutable est **modifiable** après sa création. Cela signifie que son contenu peut changer **sans recréer** un nouvel objet.

Immutable
: Un objet immutable est figé : il **ne** peut **pas** être modifié après sa création. Toute tentative de "modification" produit un **nouvel** objet, l'original restant intact.


Modifiable	✅ Oui	❌ Non
Sécurité	⚠️ Risque d’effets de bord	✅ Plus sûr, prévisible
Performance	✅ Moins de copies	⚠️ Crée souvent de nouveaux objets
Utilisé pour	État interne (ex. State)	Données constantes, configs
