---
name: generate-binding
description: Generate a GetX Binding class for an existing controller that lacks one
argument-hint: "[module-name]"
---
Generate a binding for the module specified in $ARGUMENTS:

1. **Locate the controller** at `lib/modules/$1/$1_controller.dart`
   - If it doesn't exist, report an error and stop

2. **Read the controller** and identify:
   - The controller class name (e.g., `{Name}Controller`)
   - Dependencies it uses via `Get.find<T>()` — these need registration too
   - Whether it should be `Get.lazyPut` (default) or `Get.put` (if used with permanent or fenix)

3. **Check for existing binding** — if `lib/modules/$1/$1_binding.dart` already exists, report and stop

4. **Create `lib/modules/$1/$1_binding.dart`**:
   ```dart
   import 'package:get/get.dart';
   import '{name}_controller.dart';

   class {Name}Binding extends Bindings {
     @override
     void dependencies() {
       Get.lazyPut(() => {Name}Controller());
       // Also register any dependencies found in step 2
     }
   }
   ```

5. **Update route registration** — if a `GetPage` for this module exists in `app_pages.dart` without a binding, add the binding reference

6. Run `flutter analyze` to verify
