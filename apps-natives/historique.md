# Histoire du développement mobile

## Psion

À la fin des années 80 la société britannique **Psion**  développe **EPOC**, un système d’exploitation pour OS mobile. Il est l’un des premiers systèmes d’exploitation pensés spécifiquement pour les appareils mobiles et plus spécifiquement pour les assistants personnels (PDA). Il fonctionne d’abord en version 16 bits (EPOC16), puis évolue vers une version 32 bits (EPOC32), plus moderne.

![psion](psion.webp)

EPOC introduit plusieurs concepts importants pour l’époque : un système multitâche préemptif, une exécution depuis la mémoire ROM (pour économiser les ressources) et la possibilité pour les utilisateurs de développer leurs propres applications via un langage simple proche du BASIC (OPL _Open Programming Language_). La version 32 bits marque une évolution majeure avec une architecture orientée objet en C++, une évolution du langage BASIC compatible avec Microsoft Visual Basic (OVAL _Object-based Visual Application Language_) un support des processeurs ARM et une volonté d’ouvrir la plateforme à d’autres constructeurs.

[Plaquette commerciale Psion Workabout](workabout.pdf)

![Psion Workabout](workabout.webp)

En 1998, Psion fonde avec Nokia, Ericsson et Motorola une coentreprise pour développer Symbian OS, un nouveau système pour une nouvelle génération de téléphones mobiles.

## Nokia

Symbian OS équipera de nombreux smartphones au début des années 2000, notamment chez Nokia.

Au fil des années, **Nokia** fait évoluer Symbian pour répondre à des usages de plus en plus riches : navigation web, multimédia, GPS, applications tierces. Plusieurs variantes apparaissent (UIQ puis S60), ce qui entraîne une forte fragmentation. Le développement repose principalement sur le C++, avec des API complexes et peu homogènes, rendant l’écosystème difficile d’accès pour les développeurs. 

Malgré sa domination commerciale (39 % de parts du marché mondial en 2008), Symbian souffre d’un retard en matière d’expérience utilisateur et d’outillage de développement, surtout face à l’arrivée de nouveaux standards plus simples et plus cohérents.

En 2010 Symbian^3 est la dernière version majeur du système. Un ancien dirigeant de Microsoft est alors nommé comme PDG de Nokia.

![Nokia UIQ](nokia-uiq.jpg)

### MeeGo

MeeGo est un système d’exploitation open source lancé en 2010, issu de la fusion de deux projets : Maemo (porté par Nokia) et Moblin (développé par Intel). L’objectif est de créer une plateforme Linux unifiée capable de fonctionner sur différents types d’appareils : smartphones, tablettes, netbooks et systèmes embarqués. MeeGo repose sur une architecture moderne, avec un noyau Linux et des technologies comme Qt pour le développement d’applications, ce qui le rend théoriquement attractif pour les développeurs.

Sur le plan technique, MeeGo propose une approche plus ouverte et flexible que Symbian, avec une interface moderne et une meilleure adaptation aux écrans tactiles. Il est notamment utilisé sur un appareil emblématique, le Nokia N9, souvent salué pour son ergonomie innovante (navigation par gestes). MeeGo est perçu comme une tentative sérieuse de Nokia pour revenir dans la course face à iPhone et Android.

Cependant, le projet est rapidement abandonné après le partenariat stratégique entre Nokia et Microsoft, qui impose Windows Phone comme priorité. MeeGo n’a donc pas le temps de se développer ni de construire un écosystème solide. Il reste néanmoins important dans l’histoire du mobile comme une tentative avancée de plateforme ouverte, et il influencera plus tard d’autres projets dérivés comme Sailfish OS.

### Stephen Elop

Stephen Elop joue un rôle central dans la phase finale de Nokia sur le marché du mobile, à un moment critique de son histoire.

C'est un ancien dirigeant de Microsoft. Nommé PDG de Nokia en 2010, il hérite d’une entreprise encore dominante en volume mais en perte de vitesse face à iPhone et Android. Il devient célèbre pour son mémo interne dit de la “burning platform” (plateforme en feu), dans lequel il explique que Nokia doit changer radicalement de stratégie pour survivre.

Sa décision la plus marquante est l’abandon progressif de Symbian et du projet MeeGo au profit d’un partenariat stratégique avec Microsoft. Nokia adopte alors Windows Phone comme système principal pour ses smartphones (gamme Lumia). Ce choix vise à créer un “troisième écosystème” capable de rivaliser avec iOS et Android, mais il arrive trop tard et ne parvient pas à inverser la tendance du marché.

Finalement, cette stratégie conduit à la vente de la division mobile de Nokia à Microsoft en 2013. Le rôle de Stephen Elop est donc controversé : pour certains, il a tenté une transformation nécessaire dans un contexte très difficile ; pour d’autres, il a accéléré le déclin de Nokia en abandonnant trop vite ses propres technologies.

## Palm

flowchart TD
    A[Christmas] -->|Get money| B(Go shopping)
    B --> C{Let me think}
    C -->|One| D[Laptop]
    C -->|Two| E[iPhone]
    C -->|Three| F[fa:fa-car Car]