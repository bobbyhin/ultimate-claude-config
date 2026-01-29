# Flutter/Dart Testing

## When to Activate
- Project contains `pubspec.yaml`
- Writing or modifying `.dart` test files
- Running `flutter test`

## Test Types

| Type | Speed | Scope | Package |
|------|-------|-------|---------|
| Unit | Fast | Single function/class | `test` |
| Widget | Medium | Single widget | `flutter_test` |
| Integration | Slow | Full app or large flow | `integration_test` |

## Project Structure

```
test/
├── unit/
│   ├── models/
│   │   └── user_test.dart
│   └── services/
│       └── auth_service_test.dart
├── widget/
│   ├── screens/
│   │   └── login_screen_test.dart
│   └── components/
│       └── user_card_test.dart
integration_test/
└── app_test.dart
```

## Unit Tests

```dart
import 'package:test/test.dart';

void main() {
  group('User', () {
    test('should create from JSON', () {
      final json = {'id': '1', 'name': 'Alice', 'email': 'alice@test.com'};
      final user = User.fromJson(json);

      expect(user.id, '1');
      expect(user.name, 'Alice');
      expect(user.email, 'alice@test.com');
    });

    test('should throw on invalid JSON', () {
      final json = {'id': '1'}; // missing required fields
      expect(() => User.fromJson(json), throwsA(isA<TypeError>()));
    });
  });
}
```

## Widget Tests

```dart
import 'package:flutter_test/flutter_test.dart';

void main() {
  testWidgets('LoginScreen shows email and password fields', (tester) async {
    await tester.pumpWidget(
      MaterialApp(home: LoginScreen()),
    );

    // Find widgets
    expect(find.byType(TextField), findsNWidgets(2));
    expect(find.text('Login'), findsOneWidget);

    // Interact
    await tester.enterText(find.byKey(Key('email')), 'test@test.com');
    await tester.enterText(find.byKey(Key('password')), 'password123');
    await tester.tap(find.text('Login'));
    await tester.pumpAndSettle();

    // Verify
    expect(find.text('Welcome'), findsOneWidget);
  });

  testWidgets('shows error on invalid email', (tester) async {
    await tester.pumpWidget(
      MaterialApp(home: LoginScreen()),
    );

    await tester.enterText(find.byKey(Key('email')), 'invalid');
    await tester.tap(find.text('Login'));
    await tester.pumpAndSettle();

    expect(find.text('Invalid email'), findsOneWidget);
  });
}
```

## Integration Tests

```dart
// integration_test/app_test.dart
import 'package:flutter_test/flutter_test.dart';
import 'package:integration_test/integration_test.dart';
import 'package:my_app/main.dart' as app;

void main() {
  IntegrationTestWidgetsFlutterBinding.ensureInitialized();

  testWidgets('full login flow', (tester) async {
    app.main();
    await tester.pumpAndSettle();

    // Login
    await tester.enterText(find.byKey(Key('email')), 'user@test.com');
    await tester.enterText(find.byKey(Key('password')), 'pass123');
    await tester.tap(find.text('Login'));
    await tester.pumpAndSettle();

    // Verify navigation to home
    expect(find.text('Home'), findsOneWidget);
    expect(find.text('Welcome, User'), findsOneWidget);
  });
}
```

## Mocking with Mocktail

```dart
import 'package:mocktail/mocktail.dart';

// Create mock
class MockAuthRepository extends Mock implements AuthRepository {}

void main() {
  late MockAuthRepository mockAuthRepo;

  setUp(() {
    mockAuthRepo = MockAuthRepository();
  });

  test('login returns user on success', () async {
    // Arrange
    final expectedUser = User(id: '1', name: 'Alice', email: 'alice@test.com');
    when(() => mockAuthRepo.login('alice@test.com', 'pass'))
        .thenAnswer((_) async => expectedUser);

    final service = AuthService(mockAuthRepo);

    // Act
    final result = await service.login('alice@test.com', 'pass');

    // Assert
    expect(result, expectedUser);
    verify(() => mockAuthRepo.login('alice@test.com', 'pass')).called(1);
  });

  test('login throws on invalid credentials', () async {
    when(() => mockAuthRepo.login(any(), any()))
        .thenThrow(AuthException('Invalid credentials'));

    final service = AuthService(mockAuthRepo);

    expect(
      () => service.login('bad@test.com', 'wrong'),
      throwsA(isA<AuthException>()),
    );
  });
}
```

## BLoC Testing

```dart
import 'package:bloc_test/bloc_test.dart';

void main() {
  late MockAuthRepository mockAuthRepo;

  setUp(() {
    mockAuthRepo = MockAuthRepository();
  });

  blocTest<AuthBloc, AuthState>(
    'emits [loading, authenticated] on successful login',
    build: () {
      when(() => mockAuthRepo.login(any(), any()))
          .thenAnswer((_) async => testUser);
      return AuthBloc(mockAuthRepo);
    },
    act: (bloc) => bloc.add(
      LoginRequested(email: 'test@test.com', password: 'pass'),
    ),
    expect: () => [
      AuthLoading(),
      AuthAuthenticated(testUser),
    ],
  );

  blocTest<AuthBloc, AuthState>(
    'emits [loading, error] on failed login',
    build: () {
      when(() => mockAuthRepo.login(any(), any()))
          .thenThrow(AuthException('Failed'));
      return AuthBloc(mockAuthRepo);
    },
    act: (bloc) => bloc.add(
      LoginRequested(email: 'test@test.com', password: 'wrong'),
    ),
    expect: () => [
      AuthLoading(),
      isA<AuthError>(),
    ],
  );
}
```

## Running Tests

```bash
# Unit + widget tests
flutter test

# With coverage
flutter test --coverage

# Specific file
flutter test test/unit/models/user_test.dart

# Integration tests
flutter test integration_test/

# Integration on device
flutter test integration_test/app_test.dart -d <device_id>
```

## Quality Pipeline

```bash
# Full check
dart format --set-exit-if-changed .
dart analyze
flutter test --coverage

# Coverage report
genhtml coverage/lcov.info -o coverage/html
open coverage/html/index.html
```

## Best Practices

- Write widget tests for all screens and key components
- Use `setUp` and `tearDown` for test isolation
- Mock external dependencies (API, database) with Mocktail
- Use `pumpAndSettle()` to wait for animations
- Use `Key` widgets for reliable finders in tests
- Test error states and edge cases, not just happy path
- Target 80%+ code coverage
- Use `group()` to organize related tests
