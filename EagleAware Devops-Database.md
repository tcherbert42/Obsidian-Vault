# App Repo
- Auto build flutter .apk or .ipa everytime we finish code review and push to main

**NEED a services folder for the app repo since SQLite/other services we are using will have to work with the app.** 
- This is where the SQLite implementation will go.. 

# Database 
Local Storage with SQLite
- NEED to figure out schema/er diagram for database
- NEED to figure out 
- Do not need to host SQLite server or anything, it is stored locally on the user's phone when they use the app. 
- Will be a .db file in the flutter directory, we will be using **sqflite**.

- Flutter/App screen to view scrollable aggregate esp32 logs will have to populate from the SQLite database via a query that will feed that list.
	- Does the data persist? If the database is locally on the users phone, we will have to run the esp32 first, have the logs sent to the SQLite database on the phone, and then finally populate the scrollable list in flutter. 

### sqflite
- Use the "sqflite" package with flutter. 

```dart
import 'package:sqflite/sqflite.dart';
import 'package:path/path.dart';

class DatabaseHelper {
  static Database? _database;

  // This opens the connection (or creates the file on the phone)
  Future<Database> get database async {
    if (_database != null) return _database!;
    _database = await _initDatabase();
    return _database!;
  }

  _initDatabase() async {
    String path = join(await getDatabasesPath(), 'stalker_detector.db');
    return await openDatabase(path, version: 1, onCreate: _onCreate);
  }

  // This creates the table structure
  Future _onCreate(Database db, int version) async {
    await db.execute('''
      CREATE TABLE logs(
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        mac_address TEXT,
        timestamp TEXT,
        signal_strength INTEGER
      )
    ''');
  }
}
```

# Code Reviews!
Nobody expects you to know what their code is/how to fix it. You will learn, just need them to explain it to you, etc. 
- First Code review will be default screen branch merge to main. 
- ask gem what to look for in a default screen PR

**What makes a good code review?**

## Unit Testing - Unit testing framework?
Flutter test

### TestFlight
- Build and deploy to TestFlight with a workflow?
- Look more into TestFlight

%%### Firebase
MAY NOT USE FIREBASE?
**Push Notifications:** 
- Use **FireBase Cloud Messaging (FCM)**. This is how our ESP32 (via a small backend or direct call) can tell the user's phone "Hey, someone is following you."
Hosting:
- If we build a web-based dashboard for your logs, Firebase Hosting is free and fast. 
Authentication: 
- If we want users to log in so their "whitelists" are saved across devices, Firebase Auth is incredibly simple to set up. %%