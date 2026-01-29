---
description: Flutter TDD workflow with unit, widget, and integration tests. RED → GREEN → REFACTOR cycle.
---

# Flutter Test-Driven Development

Write tests before implementation following RED → GREEN → REFACTOR.

## Instructions

### Step 1: RED — Write Failing Tests

Determine test type:
- **Unit**: Logic, models, services → `test/unit/`
- **Widget**: UI components → `test/widget/`
- **Integration**: Full flows → `integration_test/`

```dart
// test/unit/models/user_test.dart
import 'package:test/test.dart';

void main() {
  group('User', () {
    test('should validate email format', () {
      expect(User.isValidEmail('test@test.com'), isTrue);
      expect(User.isValidEmail('invalid'), isFalse);
    });
  });
}
```

Run and confirm FAIL:
```bash
flutter test test/unit/models/user_test.dart
```

### Step 2: GREEN — Write Minimal Implementation

Implement just enough to pass:
```dart
class User {
  static bool isValidEmail(String email) {
    return RegExp(r'^[\w-\.]+@([\w-]+\.)+[\w-]{2,4}$').hasMatch(email);
  }
}
```

Run and confirm PASS:
```bash
flutter test test/unit/models/user_test.dart
```

### Step 3: REFACTOR — Improve Code

Clean up while keeping tests green:
```bash
dart format .
dart analyze
flutter test
```

### Step 4: Coverage Check

```bash
flutter test --coverage
# Target: 80%+
```

## Widget Test Example

```dart
testWidgets('Counter increments', (tester) async {
  await tester.pumpWidget(MaterialApp(home: CounterScreen()));

  expect(find.text('0'), findsOneWidget);

  await tester.tap(find.byIcon(Icons.add));
  await tester.pump();

  expect(find.text('1'), findsOneWidget);
});
```

## Mocking with Mocktail

```dart
class MockApi extends Mock implements ApiClient {}

void main() {
  late MockApi mockApi;

  setUp(() => mockApi = MockApi());

  test('fetches users', () async {
    when(() => mockApi.getUsers())
        .thenAnswer((_) async => [testUser]);

    final service = UserService(mockApi);
    final users = await service.getUsers();

    expect(users, hasLength(1));
    verify(() => mockApi.getUsers()).called(1);
  });
}
```

## Running Tests

```bash
# All tests
flutter test

# Specific file
flutter test test/unit/models/user_test.dart

# With coverage
flutter test --coverage

# Integration tests
flutter test integration_test/

# Watch mode (with test runner)
flutter test --reporter=expanded
```

## Coverage Targets

| Type | Target |
|------|--------|
| Models / Services | 90%+ |
| BLoC / Riverpod | 85%+ |
| Widgets | 80%+ |
| Overall | 80%+ |

## Related

- Skills: `skills/dart-patterns/`, `skills/dart-testing/`
- Commands: `/dart-fix`, `/dart-review`
