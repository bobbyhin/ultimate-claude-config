---
description: Comprehensive Flutter/Dart code review for patterns, state management, performance, and security. Invokes the dart-reviewer agent.
---

# Flutter/Dart Code Review

This command invokes the **dart-reviewer** agent for comprehensive Flutter/Dart-specific code review.

## What This Command Does

1. **Identify Dart Changes**: Find modified `.dart` files via `git diff`
2. **Run Static Analysis**: Execute `dart analyze`
3. **Security Scan**: Check for hardcoded secrets, insecure HTTP, input validation
4. **Pattern Review**: Verify state management, widget structure, MVVM compliance
5. **Performance Check**: Widget rebuild optimization, async correctness
6. **Generate Report**: Categorize issues by severity

## When to Use

Use `/dart-review` when:
- After writing or modifying Dart/Flutter code
- Before committing Dart changes
- Reviewing pull requests with Flutter code
- Checking state management patterns
- Optimizing widget performance

## Review Categories

### CRITICAL (Must Fix)
- Hardcoded API keys or secrets
- Insecure HTTP connections (non-HTTPS)
- SQL injection in local databases
- Missing input validation
- Unhandled exceptions in critical paths
- Memory leaks (undisposed controllers/streams)

### HIGH (Should Fix)
- Missing null safety handling
- Business logic inside widgets
- State management anti-patterns
- Missing error states in async operations
- Disposing controllers not in `dispose()`
- Missing `Key` in list items

### MEDIUM (Consider)
- Missing `const` constructors
- Large build methods (>50 lines)
- Missing trailing commas
- Widget not extracted (deeply nested)
- Missing loading/error states in UI
- `print()` statements in production code

## Automated Checks Run

```bash
# Static analysis
dart analyze

# Format check
dart format --set-exit-if-changed .

# Run tests
flutter test
```

## Approval Criteria

| Status | Condition |
|--------|-----------|
| Approve | No CRITICAL or HIGH issues |
| Warning | Only MEDIUM issues (merge with caution) |
| Block | CRITICAL or HIGH issues found |

## Integration with Other Commands

- Use `/dart-test` first to ensure tests pass
- Use `/dart-fix` if analyzer errors occur
- Use `/dart-review` before committing
- Use `/code-review` for non-Dart specific concerns

## Related

- Agent: `agents/dart-reviewer.md`
- Skills: `skills/dart-patterns/`, `skills/dart-testing/`
