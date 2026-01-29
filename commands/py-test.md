---
description: Enforce TDD workflow for Python. Write pytest tests first, then implement. Verify 80%+ coverage.
---

# Python TDD Command

This command enforces test-driven development for Python using pytest.

## What This Command Does

1. **Define Interfaces**: Scaffold function/class signatures
2. **Write Tests**: Create pytest tests with parametrize (RED)
3. **Run Tests**: Verify tests fail for the right reason
4. **Implement Code**: Write minimal code to pass (GREEN)
5. **Refactor**: Improve while keeping tests green
6. **Check Coverage**: Ensure 80%+ coverage

## When to Use

Use `/py-test` when:
- Implementing new Python functions
- Building FastAPI endpoints
- Adding test coverage to existing code
- Fixing bugs (write failing test first)
- Building critical business logic

## TDD Cycle

```
RED     → Write failing pytest test
GREEN   → Implement minimal code to pass
REFACTOR → Improve code, tests stay green
REPEAT  → Next test case
```

## Test Patterns

### Parametrize

```python
@pytest.mark.parametrize("input,expected", [
    ("valid@email.com", True),
    ("", False),
    ("no-at", False),
])
def test_validate_email(input: str, expected: bool):
    assert validate_email(input) == expected
```

### Async Tests

```python
async def test_create_user(client: AsyncClient):
    response = await client.post("/users", json={
        "email": "test@example.com",
        "name": "Test"
    })
    assert response.status_code == 201
```

### Fixtures

```python
@pytest.fixture
async def db_session() -> AsyncGenerator[AsyncSession, None]:
    async with async_session() as session:
        yield session
        await session.rollback()
```

## Coverage Commands

```bash
# Run with coverage
uv run pytest --cov=src --cov-report=term-missing

# HTML report
uv run pytest --cov=src --cov-report=html

# Fail under threshold
uv run pytest --cov=src --cov-fail-under=80
```

## Coverage Targets

| Code Type | Target |
|-----------|--------|
| Critical business logic | 100% |
| API endpoints | 90%+ |
| General code | 80%+ |
| Generated/config code | Exclude |

## TDD Best Practices

**DO:**
- Write test FIRST, before any implementation
- Run tests after each change
- Use `parametrize` for comprehensive coverage
- Test behavior, not implementation details
- Include edge cases (empty, None, boundary values)

**DON'T:**
- Write implementation before tests
- Skip the RED phase
- Use `time.sleep` in tests
- Mock everything (test real behavior when possible)
- Ignore flaky tests

## Related Commands

- `/py-fix` - Fix errors
- `/py-review` - Review code after implementation
- `/verify` - Full verification loop

## Related

- Skill: `skills/python-testing/`
- Skill: `skills/tdd-workflow/`
