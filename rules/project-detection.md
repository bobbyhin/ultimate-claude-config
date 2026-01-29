# Project Type Detection

## Auto-Detect Project Language

ALWAYS detect the project type before running build, lint, test, or review commands.

Check for these marker files in the project root:

| Marker File | Project Type | Toolchain |
|-------------|-------------|-----------|
| `pyproject.toml`, `requirements.txt` | Python | ruff, pyright, pytest, uv |
| `go.mod` | Go | go vet, golangci-lint, go test |
| `package.json` + `tsconfig.json` | TypeScript | tsc, eslint, vitest/jest |
| `package.json` (no tsconfig) | JavaScript | eslint, vitest/jest |

## Language-Specific Tool Mapping

### Python
```bash
# Lint
uv run ruff check .
uv run ruff format --check .

# Type check
uv run pyright

# Test
uv run pytest

# Package management
uv add <package>
```

### Go
```bash
# Lint
golangci-lint run ./...

# Build/Type check
go build ./...
go vet ./...

# Test
go test ./...
```

### TypeScript/JavaScript
```bash
# Build
npm run build  # or pnpm/yarn

# Lint
npx eslint .

# Type check (TS only)
npx tsc --noEmit

# Test
npm test
```

## Multi-Language Projects

If multiple markers exist (e.g., `pyproject.toml` + `package.json`):
- Run checks for ALL detected languages
- Report results per language
- A project passes only when ALL languages pass

## Agent Selection

When the user asks for help without specifying a language:
- Python project → prefer `py-reviewer`, `py-error-resolver` agents
- Go project → prefer `go-reviewer`, `go-build-resolver` agents
- TS/JS project → prefer `code-reviewer`, `build-error-resolver` agents
