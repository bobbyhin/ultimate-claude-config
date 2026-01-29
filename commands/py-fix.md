---
description: Fix Python errors from ruff, pyright, and runtime. Invokes the py-error-resolver agent for minimal, surgical fixes.
---

# Python Fix

This command invokes the **py-error-resolver** agent to fix Python errors incrementally.

## What This Command Does

1. **Run Diagnostics**: Execute `ruff check`, `pyright`, and test suite
2. **Parse Errors**: Group by file and sort by severity
3. **Fix Incrementally**: One error at a time
4. **Verify Each Fix**: Re-run checks after each change
5. **Report Summary**: Show what was fixed and what remains

## When to Use

Use `/py-fix` when:
- `ruff check .` reports lint errors
- `pyright` shows type errors
- `uv run pytest` has failures
- Import errors after adding dependencies
- After pulling changes that break the project

## Diagnostic Commands Run

```bash
# Lint check
uv run ruff check .

# Auto-fix safe issues
uv run ruff check --fix .

# Format
uv run ruff format .

# Type check
uv run pyright

# Run tests
uv run pytest --tb=short
```

## Fix Strategy

1. **Ruff auto-fix first** - Safe automatic fixes (imports, formatting)
2. **Ruff manual fixes** - Issues that need code changes
3. **Pyright type errors** - Type annotations and mismatches
4. **Runtime errors** - Import, attribute, logic errors
5. **One fix at a time** - Verify each change
6. **Minimal changes** - Don't refactor, just fix

## Common Errors Fixed

| Error | Typical Fix |
|-------|-------------|
| `F401` unused import | Remove import |
| `I001` unsorted imports | `ruff check --fix` |
| `E501` line too long | Reformat |
| Missing type annotation | Add type hint |
| `reportMissingImports` | `uv add` missing package |
| `reportGeneralClassIssues` | Fix class/method signature |
| `ModuleNotFoundError` | `uv add` or fix import path |
| `AttributeError` | Fix attribute name or type |

## Stop Conditions

The agent will stop and report if:
- Same error persists after 3 attempts
- Fix introduces more errors
- Requires architectural changes
- Missing external dependencies that can't be resolved

## Related Commands

- `/py-test` - Run tests after fixes
- `/py-review` - Review code quality
- `/verify` - Full verification loop

## Related

- Agent: `agents/py-error-resolver.md`
- Skill: `skills/python-patterns/`
