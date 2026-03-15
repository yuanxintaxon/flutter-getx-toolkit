---
name: cleanup-deps
description: Find and remove unused pubspec dependencies
argument-hint: "[--dry-run | --apply]"
---
Audit pubspec.yaml dependencies against actual usage in lib/:

1. **Read dependencies** — parse all entries under `dependencies:` in `pubspec.yaml` (exclude flutter SDK itself)

2. **Scan imports** — search all `.dart` files under `lib/` for `import 'package:...'` statements; collect the set of actually-imported packages

3. **Scan dev imports** — search all `.dart` files under `test/` for packages only used in tests

4. **Cross-reference** — for each dependency, classify as:
   - **USED** — imported in lib/
   - **TEST_ONLY** — imported only in test/ (should be under dev_dependencies)
   - **UNUSED** — not imported anywhere
   - **TRANSITIVE** — not imported directly but is a build tool (flutter_launcher_icons, flutter_native_splash, build_runner, etc.) — keep these

5. **Report** — print a table:
   ```
   Package            Status      Location
   ──────────────────────────────────────────
   get                USED        dependencies
   cached_network_image USED      dependencies
   some_pkg           UNUSED      dependencies
   ```

6. **If `--apply`** (default is `--dry-run`):
   - Remove UNUSED packages from pubspec.yaml
   - Move TEST_ONLY packages to dev_dependencies
   - Run `flutter pub get`
   - Run `flutter analyze`
   - Report what was changed

7. **If `--dry-run`** — report only, do not modify files
