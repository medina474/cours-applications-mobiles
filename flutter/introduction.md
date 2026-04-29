---
title: "Introduction"
---

Effacer le programme et commencer par le programme HelloWorld

https://flutter.dev/docs/development/ui/widgets-intro

Mise en page des éléments

https://flutter.dev/docs/development/ui/layout

Concepts

https://flutter.dev/docs/get-started/codelab

Lecteur de QrCode

https://pub.dev/packages/qrscan#-example-tab-

### Consommation d'une API Web

Ajouter la libraire http
dependencies:
http: <latest_version>

N'est plus diponible
https://inducesmile.com/google-flutter/how-to-populate-listview-with-json-api-data/

https://kodestat.gitbook.io/flutter/flutter-listview-with-json-or-list-data

```dart
body: FutureBuilder<List<Users>>(
        future: _fetchUsers(),
        builder: (context, snapshot) {

          if (!snapshot.hasData) return Center(child: CircularProgressIndicator());

          return ListView(
            children: snapshot.data
                .map((user) => ListTile(
                      title: Text(user.name),
                      subtitle: Text(user.email),
                      leading: CircleAvatar(
                        backgroundColor: Colors.red,
                        child: Text(user.name[0],
                            style: TextStyle(
                              fontSize: 18.0,
                              color: Colors.white,
                            )),
                      ),
                    ))
                .toList(),
          );
        },
      ),



      Tab bar
return Scaffold(
      appBar: AppBar(
        title: Text(widget.title),
      ),
      body: DefaultTabController(
        length: 3,
        child: Scaffold(
          appBar: AppBar(
            bottom: TabBar(
              tabs: [
                Tab(icon: Icon(Icons.directions_car)),
                Tab(icon: Icon(Icons.directions_transit)),
                Tab(icon: Icon(Icons.directions_bike)),
              ],
            ),
            title: Text(widget.title),
          ),
          body: TabBarView(
            children: [
              Icon(Icons.directions_car),
              Icon(Icons.directions_transit),
              Icon(Icons.directions_bike),
            ],
          ),
        ),
      ),
    );
```

https://flutter.dev/docs/cookbook/navigation/passing-data

https://pusher.com/tutorials/flutter-user-input
