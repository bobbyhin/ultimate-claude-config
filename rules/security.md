# Security Guidelines

## Mandatory Security Checks

Before ANY commit:
- [ ] No hardcoded secrets (API keys, passwords, tokens)
- [ ] All user inputs validated
- [ ] SQL injection prevention (parameterized queries)
- [ ] XSS prevention (sanitized HTML)
- [ ] CSRF protection enabled
- [ ] Authentication/authorization verified
- [ ] Rate limiting on all endpoints
- [ ] Error messages don't leak sensitive data

## Secret Management

### TypeScript/JavaScript
```typescript
// NEVER: Hardcoded secrets
const apiKey = "sk-proj-xxxxx"

// ALWAYS: Environment variables
const apiKey = process.env.OPENAI_API_KEY

if (!apiKey) {
  throw new Error('OPENAI_API_KEY not configured')
}
```

### Python
```python
# NEVER: Hardcoded secrets
api_key = "sk-proj-xxxxx"

# ALWAYS: pydantic-settings
from pydantic_settings import BaseSettings

class Settings(BaseSettings):
    openai_api_key: str

    model_config = SettingsConfigDict(env_file=".env")

settings = Settings()
```

### Go
```go
// NEVER: Hardcoded secrets
apiKey := "sk-proj-xxxxx"

// ALWAYS: Environment variables
apiKey := os.Getenv("OPENAI_API_KEY")
if apiKey == "" {
    log.Fatal("OPENAI_API_KEY not configured")
}
```

## SQL Injection Prevention

### TypeScript/JavaScript
```typescript
// NEVER: String concatenation
const query = `SELECT * FROM users WHERE id = '${id}'`

// ALWAYS: Parameterized queries
const result = await db.query('SELECT * FROM users WHERE id = $1', [id])
```

### Python
```python
# NEVER: f-string in query
cursor.execute(f"SELECT * FROM users WHERE id = '{id}'")

# ALWAYS: Parameterized queries
cursor.execute("SELECT * FROM users WHERE id = %s", (id,))

# BEST: SQLAlchemy ORM
user = await session.get(User, id)
```

### Go
```go
// NEVER: fmt.Sprintf in query
db.Query(fmt.Sprintf("SELECT * FROM users WHERE id = '%s'", id))

// ALWAYS: Parameterized queries
db.QueryRow("SELECT * FROM users WHERE id = $1", id)
```

## Security Response Protocol

If security issue found:
1. STOP immediately
2. Use **security-reviewer** agent
3. Fix CRITICAL issues before continuing
4. Rotate any exposed secrets
5. Review entire codebase for similar issues
