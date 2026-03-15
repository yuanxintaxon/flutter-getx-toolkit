---
name: test-module
description: Generate unit tests for an existing module's controller
argument-hint: "[module-name]"
---

Generate unit tests for the module specified in $ARGUMENTS:

1. **Locate the controller** at `lib/modules/$1/$1_controller.dart`
   - If it doesn't exist, report an error and stop

2. **Read the controller** and identify:
   - All `.obs` reactive properties (initial values to verify)
   - All public methods (behavior to test)
   - Dependencies (`Get.find<T>()` calls — need mocking in setUp)
   - Workers (`ever`, `debounce`, `interval` — need disposal testing)
   - `Get.arguments` usage (need test cases for valid and invalid args)

3. **Scan for existing test helpers** — check `test/helpers/` for shared fixtures or utilities

4. **Create the test file** at `test/modules/$1/$1_controller_test.dart`:
   - Import `flutter_test`, `get`, the controller, and any test helpers found
   - `setUp`: `Get.testMode = true`, register dependencies via `Get.put()`, create controller via `Get.put()`
   - `tearDown`: `Get.reset()`
   - Test groups:
     - **Initial state**: verify all `.obs` defaults after init
     - **Public methods**: one test per method, verify state changes
     - **Edge cases**: empty inputs, invalid args, boundary values
   - For controllers that use `Get.arguments`, test with valid and invalid arguments

5. **Run the new tests**: `flutter test test/modules/$1/`
   - If failures occur, fix them
   - Report final pass/fail count

6. **Pattern reference** — scan existing test files in `test/modules/` and follow the same style
