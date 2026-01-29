---
description: Fix Dart analyzer errors, lint issues, and Flutter runtime errors. Invokes the dart-error-resolver agent.
---

# Fix Dart/Flutter Errors

This command invokes the **dart-error-resolver** agent to fix Dart and Flutter errors systematically.

## Instructions

Fix errors in this priority order:

### Step 1: Auto-Fix Lint Issues
```bash
dart fix --apply
dart format .
```

### Step 2: Analyze Remaining Issues
```bash
dart analyze
```

### Step 3: Fix Analyzer Errors
Fix manually by category:
- **Type errors**: Wrong types, missing casts, null safety violations
- **Missing imports**: Add required imports
- **Deprecated APIs**: Replace with current alternatives
- **Dead code**: Remove unused variables, imports, parameters

### Step 4: Fix Runtime Errors
If app crashes at runtime:
- **Null errors**: Add null checks, use `?` and `??` operators
- **State errors**: Fix widget lifecycle issues
- **Build errors**: Fix widget tree construction

### Step 5: Verify
```bash
dart analyze    # Should show: No issues found!
flutter test    # All tests should pass
```

## Common Errors

| Error | Fix |
|-------|-----|
| `Undefined name` | Add import or define the symbol |
| `The argument type 'X' can't be assigned to 'Y'` | Fix type mismatch or add cast |
| `A value of type 'X?' can't be assigned to 'Y'` | Add null check (`!` or `??`) |
| `Missing concrete implementation` | Implement all abstract methods |
| `Unused import` | Remove the import |
| `prefer_const_constructors` | Add `const` keyword |
| `use_key_in_widget_constructors` | Add `Key? key` parameter |
| `require_trailing_commas` | Add trailing comma |
| `avoid_print` | Use `debugPrint()` or `logger` |

## Strategy

- Fix one error at a time, verify after each fix
- Auto-fix first (`dart fix --apply`), then manual fixes
- Type errors before runtime errors
- Never suppress warnings without justification

## Related

- Agent: `agents/dart-error-resolver.md`
- Skills: `skills/dart-patterns/`, `skills/dart-testing/`
