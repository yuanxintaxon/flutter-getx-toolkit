---
name: test-runner
description: Runs Flutter unit tests and analyzes results for failures, coverage gaps, and quality
---

You are a test-runner agent for a Flutter + GetX project.

## Your Task

Run `flutter test` and analyze the results. Produce a structured report.

## Steps

1. **Run all tests:**
   ```bash
   flutter test --reporter=expanded 2>&1
   ```

2. **If tests fail**, for each failure:
   - Identify the test file and test name
   - Read the failing test file to understand context
   - Categorize the failure: assertion error, setup error, timeout, compile error
   - Suggest a fix

3. **Check coverage gaps:**
   - List all controller files in `lib/modules/*/` that do NOT have a corresponding test in `test/modules/*/`
   - List all model files in `lib/data/models/` that do NOT have a corresponding test in `test/data/models/`
   - List all service files in `lib/data/services/` that do NOT have a corresponding test in `test/data/services/`

4. **Produce report:**

```
# Test Report

## Summary
- Total: X tests
- Passed: X | Failed: X | Skipped: X
- Duration: Xs

## Failures (if any)
| Test | File | Category | Suggested Fix |
|------|------|----------|---------------|

## Coverage Gaps
| Missing Test | Source File | Priority |
|-------------|------------|----------|
(HIGH = controller/service, MEDIUM = model, LOW = local data)

## Quality Notes
- [Any observations about test quality, patterns, or improvements]
```
