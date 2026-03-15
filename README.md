# flutter-getx-toolkit

A Claude Code plugin for Flutter + GetX projects. Install once, get scaffolding skills, review agents, and architecture rules across all your GetX projects.

## Install

```bash
claude mcp add-plugin flutter-getx-toolkit /path/to/flutter-getx-toolkit
```

Or add to your project's `.claude/settings.json`:

```json
{
  "plugins": ["path/to/flutter-getx-toolkit"]
}
```

## What's Included

### Skills (8 slash commands)

| Command | Description |
|---------|-------------|
| `/new-module [name]` | Scaffold binding + controller + view + widgets/ |
| `/new-widget [name]` | Create a shared reusable widget |
| `/add-route [path] [Module]` | Add route to both route files |
| `/extract-widget [file] [lines] [Name]` | Extract widget subtree to its own file |
| `/test-module [name]` | Generate unit tests for a controller |
| `/generate-binding [name]` | Create a binding for an existing controller |
| `/cleanup-deps` | Find/remove unused pubspec dependencies |
| `/full-audit` | Run all review agents, consolidated report |

### Review Agents (7 automated reviewers)

| Agent | Focus |
|-------|-------|
| `memory-leak-reviewer` | Undisposed controllers, streams, timers |
| `perf-reviewer` | GC pressure, rebuild scope, lazy loading |
| `security-reviewer` | Hardcoded secrets, insecure HTTP, data exposure |
| `getx-validator` | Bindings, lifecycle, reactive state, routes |
| `ui-reviewer` | Theme compliance, CachedNetworkImage, const |
| `test-runner` | Test execution + coverage gap detection |
| `routes-lint` | Route file consistency (fast, uses haiku) |

### Rules (4 path-scoped guardrails)

| Rule | Applies To |
|------|-----------|
| `modules` | `lib/modules/**/*.dart` — binding/controller/view triad |
| `shared-widgets` | `lib/shared/widgets/**/*.dart` — no controllers |
| `data-models` | `lib/data/**/*.dart` — immutable, no GetX |
| `performance` | All view + widget files — build() allocation, Obx scope |

### Hooks

| Hook | Trigger | Action |
|------|---------|--------|
| `dart-format` | After Write/Edit on `.dart` files | Auto-runs `dart format` |

## Setup for Auto-Format Hook

Copy the hook config into your project's `.claude/settings.local.json`:

```json
{
  "hooks": {
    "PostToolUse": [
      {
        "matcher": "Write|Edit",
        "hooks": [
          {
            "type": "command",
            "command": "filepath=$(cat - | jq -r '.tool_input.file_path // .tool_input.path // empty') && if echo \"$filepath\" | grep -q '\\.dart$'; then dart format \"$filepath\" 2>/dev/null; fi"
          }
        ]
      }
    ]
  }
}
```

## Project Structure Expected

The toolkit assumes your Flutter/GetX project follows this layout:

```
lib/
├── app/
│   ├── routes/
│   │   ├── app_routes.dart    # Route path constants
│   │   └── app_pages.dart     # GetPage list
│   └── theme/                 # AppColors, AppTheme, etc.
├── modules/
│   └── {feature}/
│       ├── {feature}_binding.dart
│       ├── {feature}_controller.dart
│       ├── {feature}_view.dart
│       └── widgets/
├── shared/
│   └── widgets/               # Controller-free reusable widgets
└── data/
    ├── models/                # Immutable POJOs
    ├── local/                 # Local fallback data
    └── services/              # API services
```

## Customization

- **Colors class**: Skills auto-detect your `AppColors` (or equivalent). Name your color constants class consistently.
- **String constants**: If you use `AppStrings`, the ui-reviewer will check for hardcoded strings.
- **Test helpers**: Place shared test fixtures in `test/helpers/` — the test-module skill will discover and use them.

## License

MIT
