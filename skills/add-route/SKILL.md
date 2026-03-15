---
name: add-route
description: Add a new named route to both app_routes.dart and app_pages.dart
argument-hint: "[route-path] [ModuleName]"
---
Add a route using $ARGUMENTS ($1 = path, $2 = ModuleName):

1. **Locate route files** — find `app_routes.dart` and `app_pages.dart` (typically under `lib/app/routes/`)
2. Add `static const` to `AppRoutes` in `app_routes.dart`
3. Add import + `GetPage` entry to `AppPages.pages` in `app_pages.dart`
4. **BOTH files must be updated** — never just one
5. Run `flutter analyze` to verify
