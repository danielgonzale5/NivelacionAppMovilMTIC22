# MisionTIC Team Management

Flutter app to organise students into pairs and track attendance at their work sessions. Users sign in, create groups of two students, and log each session with which student attended. Data syncs in real time through Firebase.

Built for the leveling stage of MisionTIC 2022 (Colombia's national software training program), December 2021. The course provided a starter template; the assignment was to complete the app and make its widget and integration tests pass.

## Features

- **Authentication:** email and password sign-up and login with Firebase Authentication.
- **Groups:** create a group with an ID and two students, stored in Cloud Firestore.
- **Sessions:** log a session for a group with the date and each student's attendance.
- **Live lists:** groups and sessions update in real time from Firestore streams.
- **Light and dark theme:** toggled in the app and remembered with `shared_preferences`.

## Architecture

```
lib/
├── data/
│   ├── model/            Group, Sesion (Firestore document mapping)
│   └── repositories/     local preferences
├── domain/
│   └── controller/       GetX controllers: authentication, Firestore, theme
└── ui/
    ├── pages/            login, sign-up, content, add group, add session
    ├── widgets/          app bar, group and session tiles
    └── theme/
```

State management and dependency injection use [GetX](https://pub.dev/packages/get): controllers are registered once and retrieved with `Get.find()` from the pages.

## Tests

- **Widget test** (`test/widget_test.dart`): opens the groups screen with a mocked Firestore controller, fills in the add-group form and checks the new group card appears.
- **Integration tests** (`integration_test/app_test.dart`): end to end on a device or emulator, logging in, creating a group, and creating a group plus a session. They expect a Firebase user `a@a.com` with password `123456`.

## Running it

Requirements: Flutter 2.8 (Dart 2.12 to 2.x) and your own Firebase project with Authentication (email/password) and Cloud Firestore enabled. The Firebase configuration files are not included in this repository.

```bash
flutter pub get
flutterfire configure        # or add google-services.json / GoogleService-Info.plist by hand
flutter run
flutter test                 # widget test
flutter test integration_test/app_test.dart   # needs a device and the test user
```

## Relevant areas

- Mobile development with Flutter and Dart, using GetX for state management.
- Firebase Authentication and Cloud Firestore with real-time streams.
- Automated testing: widget and end-to-end integration tests.
