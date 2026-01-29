---
name: python-patterns
description: Modern Python patterns for FastAPI, Pydantic v2, async, and project structure. Stack: FastAPI + uv + ruff + pyright.
---

# Python Development Patterns

Modern Python patterns for building robust, performant APIs with FastAPI and the modern Python toolchain.

## When to Activate

- Writing new Python code
- Building FastAPI endpoints
- Designing Pydantic models
- Structuring Python projects
- Writing async code

## Stack

| Tool | Purpose |
|------|---------|
| **FastAPI** | API framework (async-first) |
| **Pydantic v2** | Validation & serialization (Rust-powered) |
| **uv** | Package management & virtual envs |
| **ruff** | Linting + formatting (replaces flake8, black, isort) |
| **pyright** | Static type checking |

## Project Structure

Organize by **domain**, not file type:

```
src/
├── auth/
│   ├── router.py          # API endpoints
│   ├── schemas.py         # Pydantic models
│   ├── models.py          # DB models
│   ├── service.py         # Business logic
│   └── dependencies.py    # DI dependencies
├── users/
│   ├── router.py
│   ├── schemas.py
│   ├── models.py
│   └── service.py
├── core/
│   ├── config.py          # Settings via Pydantic
│   ├── database.py        # DB connection
│   └── security.py        # Auth utilities
├── main.py
└── pyproject.toml
```

## Pydantic v2 Patterns

### Schema Design

```python
from pydantic import BaseModel, Field, ConfigDict

class UserBase(BaseModel):
    model_config = ConfigDict(strict=True)

    email: str = Field(..., examples=["user@example.com"])
    name: str = Field(..., min_length=1, max_length=100)

class UserCreate(UserBase):
    password: str = Field(..., min_length=8)

class UserResponse(UserBase):
    id: int
    model_config = ConfigDict(from_attributes=True)
```

### Settings with Pydantic

```python
from pydantic_settings import BaseSettings
from functools import lru_cache

class Settings(BaseSettings):
    database_url: str
    secret_key: str
    debug: bool = False

    model_config = ConfigDict(env_file=".env")

@lru_cache
def get_settings() -> Settings:
    return Settings()
```

## FastAPI Patterns

### Dependency Injection

```python
from typing import Annotated
from fastapi import Depends

# Per-request dependency
async def get_db() -> AsyncGenerator[AsyncSession, None]:
    async with async_session() as session:
        yield session

# Type alias for clean signatures
DB = Annotated[AsyncSession, Depends(get_db)]
CurrentUser = Annotated[User, Depends(get_current_user)]

@router.get("/users/{user_id}")
async def get_user(user_id: int, db: DB, user: CurrentUser) -> UserResponse:
    return await UserService(db).get(user_id)
```

### Lifecycle Scoping

```python
from contextlib import asynccontextmanager

@asynccontextmanager
async def lifespan(app: FastAPI):
    # Startup: expensive singletons
    app.state.redis = await aioredis.from_url(settings.redis_url)
    yield
    # Shutdown: cleanup
    await app.state.redis.close()

app = FastAPI(lifespan=lifespan)
```

### Router Organization

```python
# auth/router.py
from fastapi import APIRouter

router = APIRouter(prefix="/auth", tags=["auth"])

@router.post("/login")
async def login(credentials: LoginRequest, db: DB) -> TokenResponse:
    ...

# main.py
app.include_router(auth.router)
app.include_router(users.router)
```

## Async Patterns

### When to Use async vs sync

```python
# async: I/O operations (DB, HTTP, file reads)
async def fetch_user(db: AsyncSession, user_id: int) -> User:
    result = await db.execute(select(User).where(User.id == user_id))
    return result.scalar_one()

# sync: CPU-light tasks (parsing, validation)
def validate_token(token: str) -> dict:
    return jwt.decode(token, SECRET_KEY, algorithms=["HS256"])
```

### HTTP Client

```python
import httpx

async def call_external_api(url: str) -> dict:
    async with httpx.AsyncClient(timeout=5.0) as client:
        response = await client.get(url)
        response.raise_for_status()
        return response.json()
```

## Performance Tips

- Use `ORJSONResponse` for faster JSON serialization
- Set `response_model_exclude_unset=True` for large optional models
- Async DB pool: `pool_size=concurrency/2`, `max_overflow=same`
- Use `@lru_cache` for expensive config/singleton creation
- Internal service timeouts: 0.5–1.0s with circuit breakers

## uv Commands

```bash
# Init project
uv init myproject
cd myproject

# Add dependencies
uv add fastapi uvicorn[standard] pydantic-settings
uv add --dev pytest pytest-asyncio httpx ruff pyright

# Run
uv run uvicorn src.main:app --reload

# Run scripts
uv run pytest
uv run ruff check .
uv run ruff format .
uv run pyright
```

## ruff Configuration

```toml
# pyproject.toml
[tool.ruff]
target-version = "py312"
line-length = 88

[tool.ruff.lint]
select = ["E", "F", "I", "N", "UP", "B", "SIM", "ASYNC"]

[tool.ruff.lint.isort]
known-first-party = ["src"]
```

## pyright Configuration

```toml
# pyproject.toml
[tool.pyright]
pythonVersion = "3.12"
typeCheckingMode = "standard"
reportMissingImports = true
reportMissingTypeStubs = false
```
