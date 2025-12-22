# fl_lib Stores

fl_lib provides three types of stores for different persistence needs: `PrefStore`, `SecureStore`, and `HiveStore`.
All stores implement the `Store` interface, providing a unified API for data access.

## Store Interface
The core interface for all stores. Key features include:
- **Unified API**: `get<T>`, `set<T>`, `remove`, `clear`, `keys`.
- **Type Safety**: Automatic conversion support via `StoreFromObj` and `StoreToObj`.
- **Reactive**: `getAll()` stream support.
- **Metadata**: Tracks `lastUpdateTs` automatically (optional).

## PrefStore
A wrapper around `SharedPreferences` for storing simple key-value pairs (settings, flags, etc.).

### Initialization
Must be initialized before use, typically in `main.dart`.
```dart
await PrefStore.shared.init(prefix: 'my_app_');
```

### Usage
Define properties using `PrefProp` or `PrefPropDefault` for type safety.
Recommended pattern: Define all prefs in a static class or extension.

```dart
// Define properties
abstract class Prefs {
  // Simple property, nullable
  static const userToken = PrefProp<String>('user_token');
  
  // Property with default value, non-nullable
  static const isDarkMode = PrefPropDefault<bool>('is_dark_mode', false);
  
  // Custom object with JSON serialization
  static final userProfile = PrefProp<UserProfile>(
    'user_profile',
    fromObj: (json) => UserProfile.fromJson(json),
    toObj: (obj) => obj.toJson(),
  );
}

// Read
final isDark = Prefs.isDarkMode.get(); // Returns bool
final token = Prefs.userToken.get();   // Returns String?

// Write
await Prefs.isDarkMode.set(true);
await Prefs.userToken.set('xyz-123');

// Listen (Reactive)
return ValueListenableBuilder(
  valueListenable: Prefs.isDarkMode.listenable(),
  builder: (context, value, child) {
    return Text('Dark Mode: $value');
  },
);
```

### Supported Types
- Native: `bool`, `double`, `int`, `String`, `List<String>`.
- JSON: `Map<String, dynamic>` is automatically JSON encoded/decoded.
- Custom: Use `fromObj` and `toObj` converters.

## SecureStore
Uses `flutter_secure_storage` to store sensitive data (passwords, tokens).
Includes built-in `JSON` support extensions.

### Usage
Access via `SecureStore` static methods or `SecureProp`.

```dart
// Define secure property
static const apiToken = SecureProp('api_token');

// Read/Write
await apiToken.write('secret_token');
final token = await apiToken.read();

// Direct usage with JSON extensions
await SecureStore.storage.writeJson(
  'user_creds', 
  credsObj, 
  (c) => c.toJson(),
);

final creds = await SecureStore.storage.readJson(
  'user_creds', 
  (json) => Credentials.fromJson(json),
);
```

### Built-in Props
- `SecureStoreProps.bakPwd`: Backup password.
- `SecureStoreProps.hivePwd`: Encryption key for HiveStore (managed automatically).

## HiveStore
A NoSQL-like store using `hive_ce` (Community Edition).
**Key Feature**: Automatic encryption management via `SecureStore`.

### Initialization
```dart
final myStore = HiveStore('my_box');
await myStore.init(); // Handles encryption key generation/retrieval automatically
```

### Usage
Use `HiveProp` or `HivePropDefault`.

```dart
final cacheProp = myStore.propertyDefault<int>('cache_count', 0);

// Read/Write
cacheProp.put(42);
final count = cacheProp.fetch(); // or .get()

// List Property
final logs = myStore.listProperty<String>('logs');
logs.put(['log1', 'log2']);
```

### Encryption Logic
1. `HiveStore` checks `SecureStore` for an existing encryption key.
2. If missing, generates a new secure key.
3. Saves the key to `SecureStore` (under `SecureStoreProps.hivePwd`).
4. Opens the Hive box using this key.
5. Auto-migrates from unencrypted to encrypted if an old unencrypted box exists.
