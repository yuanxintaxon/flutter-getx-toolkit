---
paths:
  - "lib/shared/widgets/**/*.dart"
---
Shared widgets must:
- Extend StatelessWidget (not GetView) — no controller dependencies
- Accept all data via constructor parameters
- Use centralized color constants (e.g., AppColors.*) for all colors
- Use const constructors with super.key
- Be reusable across any module without coupling to specific controllers
