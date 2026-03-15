---
paths:
  - "lib/modules/**/*.dart"
---
Every module in lib/modules/{name}/ must have:
- {name}_binding.dart — {Name}Binding extends Bindings, registers controller via Get.lazyPut()
- {name}_controller.dart — {Name}Controller extends GetxController
- {name}_view.dart — {Name}View extends GetView<{Name}Controller>
- widgets/ directory for module-specific widgets

Module widgets: prefer passing data via constructor params over Get.find().
Place Obx() inside itemBuilder (not wrapping the entire ListView.builder) for granular rebuilds.
Use relative imports within the module. Use ../../ for cross-module.
