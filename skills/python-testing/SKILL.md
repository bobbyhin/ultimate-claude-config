---
name: python-testing
description: Modern Python testing with pytest, fixtures, parametrize, async testing, and coverage. Integrated with ruff and pyright.
---

# Python Testing Patterns

Modern testing practices using pytest with the full Python toolchain (uv, ruff, pyright).

## When to Activate

- Writing tests for Python code
- Setting up test infrastructure
- Testing FastAPI endpoints
- Testing async code
- Improving test coverage

## Test Structure

```
tests/
├── conftest.py            # Shared fixtures
├── test_auth/
│   ├── conftest.py        # Auth-specific fixtures
│   ├── test_login.py
│   └── test_register.py
├── test_users/
│   ├── test_crud.py
│   └── test_permissions.py
└── test_integration/
    └── test_api.py
```

## Fixtures

### Basic Fixtures

```python
import pytest

@pytest.fixture
def user_data() -> dict:
    return {"email": "test@example.com", "name": "Test User"}

@pytest.fixture
async def db_session() -> AsyncGenerator[AsyncSession, None]:
    async with async_session() as session:
        yield session
        await session.rollback()
```

### Scoped Fixtures

```python
@pytest.fixture(scope="session")
def app() -> FastAPI:
    """One app instance per test session."""
    return create_app(settings=test_settings)

@pytest.fixture(scope="module")
async def client(app: FastAPI) -> AsyncGenerator[AsyncClient, None]:
    """HTTP client per test module."""
    async with AsyncClient(app=app, base_url="http://test") as ac:
        yield ac
```

### Factory Fixtures

```python
@pytest.fixture
def make_user(db_session: AsyncSession):
    async def _make_user(**kwargs) -> User:
        defaults = {"email": "test@example.com", "name": "Test"}
        defaults.update(kwargs)
        user = User(**defaults)
        db_session.add(user)
        await db_session.commit()
        return user
    return _make_user
```

## Parametrize

### Basic Parametrize

```python
@pytest.mark.parametrize("email,valid", [
    ("user@example.com", True),
    ("user+tag@example.com", True),
    ("", False),
    ("no-at-sign", False),
    ("@no-local.com", False),
])
def test_validate_email(email: str, valid: bool):
    if valid:
        assert validate_email(email) is None
    else:
        with pytest.raises(ValidationError):
            validate_email(email)
```

### Parametrize with IDs

```python
@pytest.mark.parametrize("status_code,expected", [
    pytest.param(200, "ok", id="success"),
    pytest.param(404, "not_found", id="missing"),
    pytest.param(500, "error", id="server-error"),
])
def test_status_mapping(status_code: int, expected: str):
    assert map_status(status_code) == expected
```

## Async Testing

### Setup

```toml
# pyproject.toml
[tool.pytest.ini_options]
asyncio_mode = "auto"
```

### Async Tests

```python
import pytest

async def test_create_user(client: AsyncClient, db_session: AsyncSession):
    response = await client.post("/users", json={
        "email": "new@example.com",
        "name": "New User",
        "password": "securepass123"
    })
    assert response.status_code == 201
    data = response.json()
    assert data["email"] == "new@example.com"

    # Verify in DB
    user = await db_session.get(User, data["id"])
    assert user is not None
```

## FastAPI Testing

### TestClient with Dependency Override

```python
from httpx import AsyncClient, ASGITransport

@pytest.fixture
async def client(app: FastAPI) -> AsyncGenerator[AsyncClient, None]:
    # Override dependencies
    app.dependency_overrides[get_db] = lambda: test_db_session
    app.dependency_overrides[get_current_user] = lambda: test_user

    transport = ASGITransport(app=app)
    async with AsyncClient(transport=transport, base_url="http://test") as ac:
        yield ac

    app.dependency_overrides.clear()
```

### Testing Auth

```python
@pytest.fixture
def auth_headers(test_user: User) -> dict:
    token = create_access_token({"sub": str(test_user.id)})
    return {"Authorization": f"Bearer {token}"}

async def test_protected_endpoint(client: AsyncClient, auth_headers: dict):
    response = await client.get("/users/me", headers=auth_headers)
    assert response.status_code == 200
```

## Mocking

```python
from unittest.mock import AsyncMock, patch

async def test_external_api_call():
    mock_response = AsyncMock()
    mock_response.json.return_value = {"result": "ok"}
    mock_response.status_code = 200

    with patch("src.services.httpx.AsyncClient.get", return_value=mock_response):
        result = await call_external_api("http://example.com")
        assert result == {"result": "ok"}
```

## Running Tests

```bash
# Run all tests
uv run pytest

# Verbose with output
uv run pytest -v -s

# Specific file/test
uv run pytest tests/test_auth/test_login.py::test_login_success

# With coverage
uv run pytest --cov=src --cov-report=term-missing

# Parallel (install pytest-xdist)
uv run pytest -n auto

# Only failed tests from last run
uv run pytest --lf
```

## Quality Pipeline

```bash
# Full check sequence
uv run ruff check .          # Lint
uv run ruff format --check . # Format check
uv run pyright               # Type check
uv run pytest --cov=src      # Tests + coverage
```

## Coverage Targets

| Code Type | Target |
|-----------|--------|
| Critical business logic | 100% |
| API endpoints | 90%+ |
| General code | 80%+ |
| Generated/config code | Exclude |

## conftest.py Best Practices

- Put shared fixtures in `tests/conftest.py`
- Use domain-specific conftest for isolated fixtures
- Prefer factory fixtures over static data
- Use `scope="session"` for expensive setup (app, DB engine)
- Use `scope="function"` (default) for test isolation
- Always rollback DB transactions in fixtures
