---
paths:
  - "lib/data/**/*.dart"
---
Models (lib/data/models/): all fields final, const constructors, required for mandatory fields, defaults for optional booleans. No GetX dependency.

Local fallback data (lib/data/local/): private constructor LocalX._(), static const members, typed lists.

Services (lib/data/services/): handle API calls, return model instances. Encapsulate HTTP logic.
