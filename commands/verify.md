# Verification Command

Run comprehensive verification on current codebase state.

## Instructions

### Step 0: Detect Project Type

Check for marker files and select the correct toolchain:

| Marker | Type | Build | Lint | Types | Test |
|--------|------|-------|------|-------|------|
| `pyproject.toml` | Python | — | `uv run ruff check .` | `uv run pyright` | `uv run pytest` |
| `go.mod` | Go | `go build ./...` | `golangci-lint run` | `go vet ./...` | `go test ./...` |
| `pubspec.yaml` | Dart/Flutter | `flutter build` | `dart analyze` | `dart analyze` | `flutter test` |
| `tsconfig.json` | TypeScript | `npm run build` | `npx eslint .` | `npx tsc --noEmit` | `npm test` |
| `package.json` | JavaScript | `npm run build` | `npx eslint .` | — | `npm test` |

If multiple markers exist, run checks for ALL detected languages.

### Step 1: Build Check
- Run the build command for the detected project type
- Python: skip (no build step)
- If it fails, report errors and STOP

### Step 2: Type Check
- Python: `uv run pyright`
- Go: `go vet ./...`
- Dart/Flutter: `dart analyze`
- TypeScript: `npx tsc --noEmit`
- Report all errors with file:line

### Step 3: Lint Check
- Python: `uv run ruff check .`
- Go: `golangci-lint run ./...`
- Dart/Flutter: `dart analyze` (combined with type check)
- TypeScript/JavaScript: `npx eslint .`
- Report warnings and errors

### Step 4: Test Suite
- Python: `uv run pytest`
- Go: `go test ./...`
- Dart/Flutter: `flutter test`
- TypeScript/JavaScript: `npm test`
- Report pass/fail count
- Report coverage percentage

### Step 5: Code Quality Audit
- Python: search for `print()` and `breakpoint()` in source files
- Go: search for `fmt.Println` debug statements
- Dart/Flutter: search for `print()` in lib/ files
- TypeScript/JavaScript: search for `console.log` in source files
- Report locations

### Step 6: Git Status
- Show uncommitted changes
- Show files modified since last commit

## Output

Produce a concise verification report:

```
VERIFICATION: [PASS/FAIL]
Project:  [Python/Go/Dart/TypeScript/JavaScript]

Build:    [OK/FAIL/SKIP]
Types:    [OK/X errors]
Lint:     [OK/X issues]
Tests:    [X/Y passed, Z% coverage]
Secrets:  [OK/X found]
Logs:     [OK/X debug statements]

Ready for PR: [YES/NO]
```

If any critical issues, list them with fix suggestions.

## Arguments

$ARGUMENTS can be:
- `quick` - Only build + types
- `full` - All checks (default)
- `pre-commit` - Checks relevant for commits
- `pre-pr` - Full checks plus security scan
