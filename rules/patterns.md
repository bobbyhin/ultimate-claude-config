# Common Patterns

## API Response Format

### TypeScript/JavaScript
```typescript
interface ApiResponse<T> {
  success: boolean
  data?: T
  error?: string
  meta?: {
    total: number
    page: number
    limit: number
  }
}
```

### Python (FastAPI + Pydantic)
```python
from pydantic import BaseModel
from typing import Generic, TypeVar

T = TypeVar("T")

class ApiResponse(BaseModel, Generic[T]):
    success: bool
    data: T | None = None
    error: str | None = None
    meta: dict | None = None
```

### Go
```go
type ApiResponse[T any] struct {
    Success bool   `json:"success"`
    Data    T      `json:"data,omitempty"`
    Error   string `json:"error,omitempty"`
    Meta    *Meta  `json:"meta,omitempty"`
}
```

## Repository Pattern

### TypeScript/JavaScript
```typescript
interface Repository<T> {
  findAll(filters?: Filters): Promise<T[]>
  findById(id: string): Promise<T | null>
  create(data: CreateDto): Promise<T>
  update(id: string, data: UpdateDto): Promise<T>
  delete(id: string): Promise<void>
}
```

### Python
```python
from abc import ABC, abstractmethod

class Repository(ABC, Generic[T]):
    @abstractmethod
    async def find_all(self, filters: dict | None = None) -> list[T]: ...
    @abstractmethod
    async def find_by_id(self, id: str) -> T | None: ...
    @abstractmethod
    async def create(self, data: CreateDTO) -> T: ...
    @abstractmethod
    async def update(self, id: str, data: UpdateDTO) -> T: ...
    @abstractmethod
    async def delete(self, id: str) -> None: ...
```

### Go
```go
type Repository[T any] interface {
    FindAll(ctx context.Context, filters Filters) ([]T, error)
    FindByID(ctx context.Context, id string) (*T, error)
    Create(ctx context.Context, data CreateDTO) (*T, error)
    Update(ctx context.Context, id string, data UpdateDTO) (*T, error)
    Delete(ctx context.Context, id string) error
}
```

## Dependency Injection

### TypeScript/JavaScript (Custom Hooks)
```typescript
export function useDebounce<T>(value: T, delay: number): T {
  const [debouncedValue, setDebouncedValue] = useState<T>(value)

  useEffect(() => {
    const handler = setTimeout(() => setDebouncedValue(value), delay)
    return () => clearTimeout(handler)
  }, [value, delay])

  return debouncedValue
}
```

### Python (FastAPI Depends)
```python
from typing import Annotated
from fastapi import Depends

async def get_db() -> AsyncGenerator[AsyncSession, None]:
    async with async_session() as session:
        yield session

DB = Annotated[AsyncSession, Depends(get_db)]

@router.get("/users")
async def list_users(db: DB) -> list[UserOut]:
    ...
```

### Go (Constructor Injection)
```go
type UserService struct {
    repo UserRepository
    cache Cache
}

func NewUserService(repo UserRepository, cache Cache) *UserService {
    return &UserService{repo: repo, cache: cache}
}
```

## Skeleton Projects

When implementing new functionality:
1. Search for battle-tested skeleton projects
2. Use parallel agents to evaluate options:
   - Security assessment
   - Extensibility analysis
   - Relevance scoring
   - Implementation planning
3. Clone best match as foundation
4. Iterate within proven structure
