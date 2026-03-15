---
name: extract-widget
description: Extract a widget subtree into its own class file
argument-hint: "[source-file] [line-range] [WidgetName] [--shared]"
---
Extract a widget subtree into a new StatelessWidget class:

Arguments from $ARGUMENTS: $1 = source file, $2 = line range (e.g., 45-80), $3 = WidgetName, $4 = optional --shared flag

1. **Read source** — read $1 and identify the widget subtree at lines $2

2. **Analyze dependencies** — determine what the subtree needs:
   - Variables/fields referenced from the parent widget
   - Theme/context usage
   - Controller references (if any — avoid in shared widgets)
   - Imports required

3. **Determine constructor params** — create required constructor parameters for all data the subtree needs from its parent. Use specific types, not controllers.

4. **Detect project structure** — find `lib/modules/` and `lib/shared/widgets/` paths

5. **Create widget file**:
   - If `--shared`: create in `lib/shared/widgets/{snake_case_name}.dart`
   - Otherwise: create in `lib/modules/{current_module}/widgets/{snake_case_name}.dart`
   - StatelessWidget with const constructor, super.key
   - Use project color constants for all colors
   - Add const where possible

6. **Update source file** — replace the original subtree with the new widget instantiation, passing required params. Add const if all params are compile-time constants.

7. **Add import** — add the import for the new widget file to the source file

8. **Analyze** — run `flutter analyze` to verify extraction is correct

9. **Report** — show the new widget file path and the diff in the source file
