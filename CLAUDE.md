# Flutter GetX Toolkit

Reusable Claude Code plugin for Flutter + GetX projects.

## Architecture
- `lib/modules/{feature}/` — each has {Feature}Binding + {Feature}Controller + {Feature}View + widgets/
- `lib/shared/widgets/` — stateless, controller-free reusable widgets
- `lib/data/models/` — immutable POJOs with const constructors
- `lib/app/routes/` — app_routes.dart (constants) + app_pages.dart (GetPage list) — always update BOTH

## Key Conventions
- Views: `GetView<T>` (or `StatelessWidget` when controller uses a dynamic tag), Controllers: `GetxController`, Bindings: `Bindings`
- Reactive: `.obs` properties, `Obx()` in views — never setState/StatefulWidget
- Colors: always use centralized color constants — never raw Color() or Colors.x in views
- Strings: use centralized string constants for UI text — never hardcode user-facing strings in views
- Permanent controllers (cross-feature): `Get.put(permanent: true)` in a shell/root binding
- Utility classes: private constructor `ClassName._();`
- Obx() should wrap the smallest possible widget subtree, placed inside itemBuilder when in ListView.builder

## Do NOT
- Create controllers without corresponding bindings
- Use `Get.find()` in a view when `controller` (from GetView) is available
- Add route to only one of app_routes.dart / app_pages.dart
- Hardcode colors — add to centralized constants first
- Hardcode UI strings — add to centralized constants first
- Use setState or StatefulWidget in modules
