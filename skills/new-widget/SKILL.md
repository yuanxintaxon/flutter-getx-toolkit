---
name: new-widget
description: Create a new shared reusable widget following project patterns
argument-hint: "[widget-name]"
---
Create a new shared reusable widget from $ARGUMENTS (snake_case name):

1. **Detect shared widgets dir** — find `lib/shared/widgets/` (create if missing)
2. **Detect theme class** — find `AppColors` or equivalent theme constants class
3. **Scan existing widgets** — read 1-2 existing shared widgets to match the project's style

4. Create `lib/shared/widgets/$1.dart`:
   - Import `material.dart` and the project's color constants
   - `StatelessWidget` with `const` constructor and `super.key`
   - Required data params, optional style params with defaults
   - Use project color constants (e.g., `AppColors.*`) for all colors — never raw `Color()` or `Colors.x`
   - Add `const` where possible

5. Run `flutter analyze` to verify
