---
name: new-module
description: Scaffold a complete GetX feature module with binding, controller, view, and widgets/ directory
argument-hint: "[module-name]"
---
Create a new GetX module from $ARGUMENTS (snake_case name):

1. **Detect project structure** — find the modules directory (usually `lib/modules/`)
2. **Detect route files** — find `app_routes.dart` and `app_pages.dart` under `lib/app/routes/`
3. **Detect theme** — find `AppColors` class for scaffold background color

4. Create `lib/modules/$1/` and `lib/modules/$1/widgets/`

5. Create `{name}_binding.dart`:
   ```dart
   class {Name}Binding extends Bindings {
     @override
     void dependencies() {
       Get.lazyPut(() => {Name}Controller());
     }
   }
   ```

6. Create `{name}_controller.dart`:
   ```dart
   class {Name}Controller extends GetxController {
     @override
     void onInit() {
       super.onInit();
       // TODO: initialize
     }
   }
   ```

7. Create `{name}_view.dart`:
   ```dart
   class {Name}View extends GetView<{Name}Controller> {
     const {Name}View({super.key});

     @override
     Widget build(BuildContext context) {
       return Scaffold(
         // Use AppColors if available, otherwise Theme
         backgroundColor: /* AppColors.backgroundDark or Theme.of(context).scaffoldBackgroundColor */,
         body: const Center(child: Text('{Name}')),
       );
     }
   }
   ```

8. Add route to `app_routes.dart`: `static const {name} = '/{kebab-name}';`
9. Add `GetPage` entry to `app_pages.dart` with binding and view imports
10. Run `flutter analyze` to verify
11. Suggest running `/test-module $1` to generate unit tests
