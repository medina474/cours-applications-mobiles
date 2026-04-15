# Progressive Web App

> [!NOTE]
> **Objectif :** Accéder à une application hybride directement depuis le navigateur du terminal sans passer par un outil tiers.

Accéder à internet sur un appareil mobile, c’est soit ouvrir un site web via un navigateur, soit télécharger une application sur sa tablette ou son smartphone. Dans le premier cas, et à  condition que le site en question ait été conçu en **responsive design**, il y a de fortes chances qu’il mette du temps à se charger. Or une page qui met plus de 3 secondes à apparaître sur un écran est abandonnée par plus de la moitié des internautes.

Autres problèmes propres aux sites web, l’impossibilité d’avoir un affichage hors connexion et la nécessité de faire une recherche ou de saisir une URL lorsque l’on veut y accéder.

Les applications sont-elles mieux loties ? Pas forcément. Entre le moment où elle est trouvée dans la jungle des stores et celui où elle est effectivement ouverte, une application perd en moyenne 20% de
ses utilisateurs et autant de clients potentiels.

Pour une entreprise, la technologie Progressive web apps offre deux avantages principaux : elle lui apporte une présence sur mobile qui sera repérée et référencée par Google ; et elle offre à ses prospects une expérience utilisateur inédite.

Pour faire simple, les PWA combinent les meilleures fonctionnalités des pages web et des applis.

Pour les propriétaires d’appareils mobiles, elles ne se téléchargent pas : nul besoin d’aller fouiner
dans l’AppStore ou le Play Store pour les trouver. En revanche, elles vont visuellement apparaître sur l’écran avec une icône ressemblant à celle d’une appli : inutile de rentrer l’URL à chaque fois que l’on souhaite se connecter. Le navigateur web s'ouvre en plein écran sans barre d'adresse, ni boutons, ni menus. L'expérience utilisateur est très proche d'une vraie application.

Dans une PWA c'est le navigateur de l'appareil mobile qui se charge d'encapsuler le site web compatible dans une application hybride. L'application est créée directement sur l'appareil, le développeur n'a pas besoin d'outils spécifiques ou de compilateur pour créer une application PWA.

### Conditions

Pour rendre une page web compatible PWA, il faut satifaires quelques conditions.

- Une PWA doit être hébergée sur un serveur sécurisé utilisant [HTTPS](../../securité/https/).
- [Web App Manifest](manifest) : Un fichier JSON appelé manifeste web app doit être inclus dans l'application.
- [Service Workers](service-workers) : Les service workers sont des scripts JavaScript qui s'exécutent en arrière-plan et permettent à l'application de fonctionner hors ligne, d'améliorer les performances et de fournir des fonctionnalités telles que les notifications push. Ils sont essentiels pour une PWA.
- Technologies Web Standards : La PWA est construite à l'aide de technologies web standard telles que HTML, CSS et JavaScript.
- **Responsive Design** : L'application doit être conçue pour être responsive, c'est-à-dire qu'elle doit s'adapter à différentes tailles d'écrans et être utilisable sur les smartphones, tablettes et ordinateurs de bureau.
- Navigation sans interruption : Une PWA doit permettre une navigation **fluide** et sans interruption, offrant une expérience utilisateur semblable à celle d'une application native. La conception d'une [SPA](single-page-application) est essentiel.
- Capacités natives (Facultatif) : Les PWA peuvent accéder à certaines fonctionnalités natives de l'appareil, telles que la caméra, le GPS, les notifications push, etc., en utilisant des APIs telles que l'API de géolocalisation, l'API de notifications, etc.

En respectant ces conditions, vous pouvez développer une PWA qui offre une expérience utilisateur performante et engageante, similaire à celle des applications natives, tout en profitant des avantages de l'écosystème web.

## Frameworks

[jQuery Mobile](jquerymobile)

[Bootstrap](bootstrap)

[framework7](framework7)

[OnsenUI](onsenui)


## Outils

- [PWA Builder](https://www.pwabuilder.com/)
- [Mask Icon](https://maskable.app/editor)
- [PWA Workshop](https://pwa-workshop.js.org/fr/)

## Travaux pratiques

[Travaux pratiques](travaux-pratiques)
