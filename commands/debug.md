---
name: debug
description: Systematically debug issues with root cause analysis
---

1. Reproduce the issue:
   - Get exact error message or unexpected behavior
   - Find minimal steps to reproduce
   - Note: environment, inputs, frequency

2. Gather evidence:
   - Check error logs and stack traces
   - Review recent git changes (git log, git diff)
   - Check related test failures

3. Narrow down root cause:
   - Binary search: comment out code to isolate
   - Add targeted console.log / debug prints
   - Check inputs/outputs at each layer

4. Form and test hypothesis:
   - State expected vs actual behavior
   - Make ONE change at a time
   - Verify fix resolves the issue

5. Apply fix:
   - Make minimal, targeted change
   - Preserve existing functionality
   - Remove all debug code

6. Prevent regression:
   - Write test that reproduces the original bug
   - Ensure test fails without fix, passes with fix
   - Run full test suite to confirm no side effects

Never guess-and-check. Always understand WHY before fixing.
