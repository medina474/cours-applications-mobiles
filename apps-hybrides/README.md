# Applications hybrides

> [!NOTE]
> **Objectif :** Combiner l'avantage d'un développement web et la possibilité d'une application native.

Une application hybride est une application qui **embarque un navigateur web**. Toute la partie navigation (barre d'adresse, menu, retour arrière) est cachée à l'utilisateur. L'avantage est que l'application web ressemble trait pour trait à une application native. Ses capacités sont améliorées par rapport à une application web car les l'application hybride prennent en charge ce qui ne l'est pas habituellement par un navigateur (lecteur code barre, lecteur RFID, caméra, stockage, etc…)

L'autre avantage est que l'application embarque son propre navigateur même si le terminal possède un navigateur obsolète.

L'application peut être distribuée via un magasin d'application comme Play Store et/ou Apple Store.

Les performances sont légèrement en retrait par rapport à une application native car l'interprétation d'une page web n'est pas une exécution directe par le processeur, mais passe par le moteur de rendu HTML (généralement Chromium)

Certaines opérations comme le calcul 3D intensif ne sont pas toujours possible avec une application hybride. L'avantage est que l'application est à 95% faite avec  des technologies « Web » telles que l'HTML , CSS et Javascript. Les solutions de génération d'applications hybride produisent des applications Android et iOS mais avec un bémol, le SDK natif doit être installé sur la machine. La génération d'une application hybride pour iOS doit se faire sur un ordinateur Mac même si le développeur écrit aucune ligne de code Swift.

Les solutions permettant des développer des applications hybrides sont entre autres :

- [Apache Cordova](https://cordova.apache.org/) et tous ses dérivées comme [Ionic](https://ionicframework.com/) ou [Monaca](https://monaca.io/)
- Capacitor (Ionic)

![Cordova](cordova.png "h-12")
![Ionic](ionic.png "h-12")

- Les solutions en ligne (développement depuis le web) comme [GoodBarber](https://fr.goodbarber.com/)

![GoodBarber](goodbarber.png "h-12")
