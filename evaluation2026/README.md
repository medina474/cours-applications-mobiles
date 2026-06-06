# Évaluation 2026

> [!WARNING]
> Travail individuel. Partage de code = partage des points.

Vous avez le droit à toute la documentation, vos anciens travaux et les ressources de types forums. Les outils de communication ne sont pas autorisés (Discord, email, pastebin, etc.).

Ce n'est pas un concours de vitesse, Vous n'êtes pas autorisé à sortir avant la fin de la séance.

Vous vous efforcerez de réaliser un développement qui suit les bonnes pratiques, notamment au niveau de la séparation des responsabilités, et des tests unitaires. La qualité du code et son intégration dans le reste de l'application seront notés.

Le sujet est volontairement imprécis, c'est à vous de définir et de concevoir une application de type professionnelle.

## Contexte :

Le but est de développer un quiz dans votre application Flutter Cinéma existante. Le jeu comporte quatre écrans :

- l'écran d'accueil où l'utilisateur entre son nom,
- l'écran de selection du quiz,
- l'écran du jeu avec les questions,
- l'écran du score affichant le résultat final.
- Retour à l'écran de selection du quiz

Il est demandé de **persister** les données pour afficher la progression du joueur sur un quiz. La vitesse de réponse doit être prise en compte dans le calcul du score voir éliminatoire. Il faut mettre en avant les thèmes qui n'ont pas encore été joués.

Des animations ludiques à l'affichage du score comme une image qui tombe du haut puis rebondit avant de se stabiliser, ou le score qui s'incrémente seraient les bienvenues. 

## Documentation technique :

Dans l'écran d'accueil de l'application remplacer l'icône du 3e bouton par une icône représentant un quiz.

Récupérer les différents thèmes avec un appel au web service suivant

```
https://api.neotech.fr/quizzes?select=quiz_id,quiz
```

Les illustrations

```
https://img.neotech.fr/cgi/images/tr:width=300/cinema%2fquiz%2f3.png
```

remplacer le chiffre 3 juste devant .png par l'id du quiz. Les propriétés de l'image peuvent être modifiées pour correspondre à votre besoin et à l'optimisation de la bande passante.

Voir la documentation de l'api : 

https://pkg.go.dev/github.com/kritihq/kriti-images#section-readme


Récupérer les questions d'un thème par un appel au web service

```
https://api.neotech.fr/quizzes?quiz_id=eq.1
```

Utiliser les images fournies pour indiquer la performance du joueur