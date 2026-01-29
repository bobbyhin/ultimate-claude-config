---
name: debug
description: Systematic debugging with root cause analysis
argument-hint: [issue description]
---

## 1. Gather Symptoms

Ask these 5 questions before investigating:

1. **Expected behavior** - What should happen?
2. **Actual behavior** - What happens instead?
3. **Error messages** - Any errors? (paste or describe)
4. **Timeline** - When did this start? Ever worked?
5. **Reproduction** - How do you trigger it?

## 2. Reproduce the Issue

- Find minimal steps to reproduce
- Note: environment, inputs, frequency
- If can't reproduce, gather more evidence first

## 3. Gather Evidence

```bash
# Check recent changes
git log --oneline -10
git diff HEAD~3

# Check error logs
# (adapt to your stack)
```

- Check error logs and stack traces
- Review recent git changes that may have caused it
- Check related test failures

## 4. Narrow Down Root Cause

- Use `git bisect` to find the breaking commit
- Binary search: comment out code to isolate
- Add targeted console.log / debug prints
- Check inputs/outputs at each layer

## 5. Form and Test Hypothesis

- State: "Expected X but got Y because Z"
- Make ONE change at a time
- Verify fix resolves the issue
- If hypothesis wrong, document what was eliminated

## 6. Apply Fix

- Make minimal, targeted change
- Preserve existing functionality
- Remove all debug code

## 7. Prevent Regression

- Write test that reproduces the original bug
- Ensure test fails WITHOUT fix, passes WITH fix
- Run full test suite to confirm no side effects

## 8. Document

Create `.reports/debug-{issue}.md` with:
- Root cause summary
- What was tried and eliminated
- Final fix applied
- Test added

Never guess-and-check. Always understand WHY before fixing.
