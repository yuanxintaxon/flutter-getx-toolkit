---
name: full-audit
description: Run all review agents and produce a consolidated audit report
argument-hint: ""
---
Run a comprehensive codebase audit using all available review agents:

1. **Launch agents in parallel** — invoke all available review agents simultaneously:
   - `memory-leak-reviewer` — resource disposal and leak detection
   - `perf-reviewer` — performance issues and GC pressure
   - `security-reviewer` — secrets, insecure URLs, data exposure
   - `getx-validator` — GetX architecture correctness
   - `ui-reviewer` — visual consistency and theme compliance
   - `test-runner` — unit test execution and coverage gap detection
   - `routes-lint` — route file consistency

2. **Collect results** — gather findings from all agents

3. **Consolidate report** — produce a unified report with these sections:

   ```
   # Audit Report

   ## Executive Summary
   Total findings: X critical, Y warnings, Z suggestions

   ## Critical Issues (must fix)
   [All CRITICAL/LEAK severity findings from any agent]

   ## Warnings (should fix)
   [All WARNING/HIGH/RISK/error severity findings]

   ## Suggestions (nice to have)
   [All INFO/MEDIUM/LOW/suggestion severity findings]

   ## Per-File Heatmap
   [Files sorted by number of findings, most issues first]
   file_path: N issues (breakdown by agent)

   ## Test Results
   - Total: X | Passed: X | Failed: X
   - Coverage gaps: [list of untested controllers/models]

   ## Top 5 Priorities
   [The 5 most impactful issues to fix first, with reasoning]
   ```

4. **Output** — present the consolidated report to the user
