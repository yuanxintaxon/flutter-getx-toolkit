---
paths:
  - "lib/modules/**/*_view.dart"
  - "lib/modules/**/widgets/**/*.dart"
  - "lib/shared/widgets/**/*.dart"
---
Performance rules for widget files:

- **No allocation in build()** — BoxDecoration, TextStyle, EdgeInsets, BorderRadius, Shadow objects must be static const or final class-level fields, never created inline in build()
- **Obx() smallest subtree** — wrap only the widget that reads .obs, never an entire Scaffold or Column
- **const everywhere** — add const to constructors and widget instantiations wherever possible
- **RepaintBoundary** — wrap expensive static subtrees (BackdropFilter, complex gradients) that sit near frequently-rebuilding siblings
- **CachedNetworkImage** — always specify explicit width and height to avoid layout thrashing
- **ListView.builder** — use .builder() (or .separated()) instead of Column + map/for when list exceeds 5 items; set itemExtent or prototypeItem when items have uniform height
- **Computed lists** — cache derived/filtered lists in the controller (updated via workers), never create new lists in getters that Obx() reads every rebuild
