# Coding Style

## Immutability (CRITICAL)

ALWAYS create new objects, NEVER mutate:

### TypeScript/JavaScript
```javascript
// WRONG: Mutation
function updateUser(user, name) {
  user.name = name  // MUTATION!
  return user
}

// CORRECT: Immutability
function updateUser(user, name) {
  return {
    ...user,
    name
  }
}
```

### Python
```python
# WRONG: Mutation
def update_user(user: dict, name: str) -> dict:
    user["name"] = name  # MUTATION!
    return user

# CORRECT: Immutability
def update_user(user: dict, name: str) -> dict:
    return {**user, "name": name}

# BEST: Frozen dataclass
@dataclass(frozen=True)
class User:
    name: str
    email: str

updated = replace(user, name="new_name")
```

### Go
```go
// WRONG: Mutation via pointer
func updateUser(u *User, name string) {
    u.Name = name  // MUTATION!
}

// CORRECT: Return new value
func updateUser(u User, name string) User {
    u.Name = name
    return u
}
```

## File Organization

MANY SMALL FILES > FEW LARGE FILES:
- High cohesion, low coupling
- 200-400 lines typical, 800 max
- Extract utilities from large components
- Organize by feature/domain, not by type

## Error Handling

ALWAYS handle errors comprehensively:

### TypeScript/JavaScript
```typescript
try {
  const result = await riskyOperation()
  return result
} catch (error) {
  console.error('Operation failed:', error)
  throw new Error('Detailed user-friendly message')
}
```

### Python
```python
try:
    result = await risky_operation()
    return result
except SpecificError as e:
    logger.error("Operation failed: %s", e)
    raise AppError("Detailed user-friendly message") from e
```

### Go
```go
result, err := riskyOperation()
if err != nil {
    return fmt.Errorf("operation failed: %w", err)
}
```

## Input Validation

ALWAYS validate user input:

### TypeScript/JavaScript
```typescript
import { z } from 'zod'

const schema = z.object({
  email: z.string().email(),
  age: z.number().int().min(0).max(150)
})

const validated = schema.parse(input)
```

### Python
```python
from pydantic import BaseModel, Field

class UserInput(BaseModel):
    email: EmailStr
    age: int = Field(ge=0, le=150)

validated = UserInput.model_validate(data)
```

### Go
```go
type UserInput struct {
    Email string `json:"email" validate:"required,email"`
    Age   int    `json:"age" validate:"gte=0,lte=150"`
}

err := validate.Struct(input)
```

## Code Quality Checklist

Before marking work complete:
- [ ] Code is readable and well-named
- [ ] Functions are small (<50 lines)
- [ ] Files are focused (<800 lines)
- [ ] No deep nesting (>4 levels)
- [ ] Proper error handling
- [ ] No debug statements (console.log / print() / fmt.Println)
- [ ] No hardcoded values
- [ ] No mutation (immutable patterns used)
