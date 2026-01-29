---
description: Comprehensive Python code review for FastAPI patterns, type safety, async correctness, and security. Invokes the py-reviewer agent.
---

# Python Code Review

This command invokes the **py-reviewer** agent for comprehensive Python-specific code review.

## What This Command Does

1. **Identify Changes**: Find modified `.py` files via `git diff`
2. **Run Static Analysis**: Execute `ruff check`, `pyright`
3. **FastAPI Review**: Check dependency injection, async patterns, Pydantic usage
4. **Security Scan**: Check for injection, secrets, unsafe deserialization
5. **Pattern Review**: Verify code follows Python best practices
6. **Generate Report**: Categorize issues by severity

## When to Use

Use `/py-review` when:
- After writing or modifying Python code
- Before committing Python changes
- Reviewing pull requests with Python code
- Building FastAPI endpoints
- Working with Pydantic models

## Review Categories

### CRITICAL (Must Fix)
- SQL/Command injection vulnerabilities
- Hardcoded secrets or credentials
- Unsafe `eval()` or `pickle` usage
- Missing authentication on endpoints
- Sync I/O blocking the event loop

### HIGH (Should Fix)
- Missing type annotations on public functions
- Sync function doing I/O (should be async)
- Pydantic v1 patterns (should use v2)
- Missing error handling on external calls
- No input validation on endpoints

### MEDIUM (Consider)
- Missing docstrings on public API
- Non-idiomatic Python patterns
- Overly broad exception handling
- Missing `response_model` on endpoints
- Fixtures not properly scoped

## Automated Checks Run

```bash
# Lint
uv run ruff check .

# Type check
uv run pyright

# Security (if installed)
uv run bandit -r src/

# Dependency audit
uv pip audit
```

## Approval Criteria

| Status | Condition |
|--------|-----------|
| Approve | No CRITICAL or HIGH issues |
| Warning | Only MEDIUM issues (merge with caution) |
| Block | CRITICAL or HIGH issues found |

## Related Commands

- `/py-test` - Ensure tests pass first
- `/py-fix` - Fix errors found in review
- `/code-review` - For non-Python specific concerns

## Related

- Agent: `agents/py-reviewer.md`
- Skills: `skills/python-patterns/`, `skills/python-testing/`
