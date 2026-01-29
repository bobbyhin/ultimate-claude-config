---
name: dart-patterns
description: Flutter/Dart state management, MVVM architecture, Riverpod, freezed, and performance patterns
---

# Flutter/Dart Patterns

## When to Activate
- Project contains `pubspec.yaml`
- Working with `.dart` files
- Flutter or Dart project detected

## Toolchain

```bash
# Format
dart format .

# Analyze (lint + type check)
dart analyze

# Auto-fix lint issues
dart fix --apply

# Run app
flutter run

# Package management
flutter pub add <package>
flutter pub get
```

## Project Structure (Feature-Based)

```
lib/
├── src/
│   ├── features/
│   │   ├── auth/
│   │   │   ├── data/              # Repositories, data sources
│   │   │   ├── domain/            # Models, entities
│   │   │   ├── application/       # Service/business logic
│   │   │   └── presentation/      # Widgets, controllers, screens
│   │   ├── products/
│   │   └── settings/
│   ├── common_widgets/            # Shared widgets
│   ├── routing/                   # GoRouter or Navigator config
│   └── utils/                     # Helpers, extensions
├── main.dart
test/
├── unit/
├── widget/
└── integration_test/
```

## State Management

### Riverpod (Recommended for structured apps)
```dart
// Define a provider
@riverpod
class AuthNotifier extends _$AuthNotifier {
  @override
  AuthState build() => const AuthState.unauthenticated();

  Future<void> login(String email, String password) async {
    state = const AuthState.loading();
    try {
      final user = await ref.read(authRepositoryProvider).login(email, password);
      state = AuthState.authenticated(user);
    } catch (e) {
      state = AuthState.error(e.toString());
    }
  }
}

// Use in widget
class LoginScreen extends ConsumerWidget {
  @override
  Widget build(BuildContext context, WidgetRef ref) {
    final authState = ref.watch(authNotifierProvider);
    return authState.when(
      unauthenticated: () => LoginForm(),
      loading: () => CircularProgressIndicator(),
      authenticated: (user) => HomeScreen(user: user),
      error: (message) => ErrorWidget(message),
    );
  }
}
```

### BLoC (Enterprise / Large teams)
```dart
// Event
sealed class AuthEvent {}
class LoginRequested extends AuthEvent {
  final String email;
  final String password;
  LoginRequested({required this.email, required this.password});
}

// BLoC
class AuthBloc extends Bloc<AuthEvent, AuthState> {
  final AuthRepository _authRepo;

  AuthBloc(this._authRepo) : super(AuthInitial()) {
    on<LoginRequested>(_onLoginRequested);
  }

  Future<void> _onLoginRequested(
    LoginRequested event,
    Emitter<AuthState> emit,
  ) async {
    emit(AuthLoading());
    try {
      final user = await _authRepo.login(event.email, event.password);
      emit(AuthAuthenticated(user));
    } catch (e) {
      emit(AuthError(e.toString()));
    }
  }
}
```

## MVVM Architecture (Official Recommendation)

```dart
// Model
@freezed
class User with _$User {
  const factory User({
    required String id,
    required String name,
    required String email,
  }) = _User;

  factory User.fromJson(Map<String, dynamic> json) => _$UserFromJson(json);
}

// Repository (Data Layer)
class UserRepository {
  final ApiClient _client;
  UserRepository(this._client);

  Future<User> getUser(String id) async {
    final response = await _client.get('/users/$id');
    return User.fromJson(response.data);
  }
}

// ViewModel (Presentation Layer)
class UserViewModel extends ChangeNotifier {
  final UserRepository _repo;
  User? _user;
  bool _loading = false;

  User? get user => _user;
  bool get loading => _loading;

  UserViewModel(this._repo);

  Future<void> loadUser(String id) async {
    _loading = true;
    notifyListeners();
    _user = await _repo.getUser(id);
    _loading = false;
    notifyListeners();
  }
}
```

## Immutability Patterns

```dart
// Use freezed for immutable data classes
@freezed
class AppState with _$AppState {
  const factory AppState({
    required User user,
    required List<Product> products,
    @Default(false) bool isLoading,
  }) = _AppState;
}

// Update immutably with copyWith
final newState = state.copyWith(isLoading: true);
```

## Async Patterns

```dart
// Use FutureBuilder for async UI
FutureBuilder<User>(
  future: userRepository.getUser(id),
  builder: (context, snapshot) {
    if (snapshot.connectionState == ConnectionState.waiting) {
      return CircularProgressIndicator();
    }
    if (snapshot.hasError) {
      return Text('Error: ${snapshot.error}');
    }
    return UserCard(user: snapshot.data!);
  },
)

// Use StreamBuilder for reactive data
StreamBuilder<List<Message>>(
  stream: chatRepository.messagesStream(chatId),
  builder: (context, snapshot) {
    if (!snapshot.hasData) return CircularProgressIndicator();
    return ListView.builder(
      itemCount: snapshot.data!.length,
      itemBuilder: (_, i) => MessageTile(snapshot.data![i]),
    );
  },
)
```

## Analysis Options

```yaml
# analysis_options.yaml
include: package:flutter_lints/flutter.yaml

analyzer:
  strict-casts: true
  strict-raw-types: true
  errors:
    missing_return: error
    dead_code: warning

linter:
  rules:
    - prefer_const_constructors
    - prefer_const_literals_to_create_immutables
    - avoid_print
    - prefer_final_locals
    - require_trailing_commas
    - use_key_in_widget_constructors
```

## Performance Tips

- Use `const` constructors to avoid unnecessary rebuilds
- Place `Consumer`/`BlocBuilder` deep in widget tree
- Use `ListView.builder` instead of `ListView` for long lists
- Avoid expensive operations in `build()` method
- Use `RepaintBoundary` to isolate expensive repaints
- Cache network images with `cached_network_image` package
