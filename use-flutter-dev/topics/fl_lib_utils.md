# fl_lib Utils

fl_lib provides a robust set of utility classes for ID generation, cryptography, and UI/System integration.

## ID Generation

### SnowflakeLite
A lightweight, high-performance ID generator based on the Snowflake algorithm (timestamp + sequence).
- **Structure**: 66 bits (54 bit timestamp + 12 bit sequence).
- **Format**: Radix-36 string (alphanumeric).
- **Use Case**: Primary keys, sortable unique IDs.

```dart
// Generate
final id = SnowflakeLite.generate();

// Decode
final (timestamp, seq) = SnowflakeLite.decode(id)!;
```

### ShortId
Generates shorter, URL-friendly IDs based on timestamp and randomness.
- **Format**: Custom base64-like string (a-Z, 0-9, -, +).
- **Use Case**: Public facing IDs, shareable links.

```dart
final shortId = ShortId.generate();
```

## Cryptography

### Cryptor
A secure encryption utility class designed for sensitive data storage.
- **Algorithm**: AES-GCM (Authenticated Encryption).
- **Key Derivation**: PBKDF2 (SHA-256, 100k iterations).
- **Structure**: `Header` + `Salt` + `Nonce` + `Ciphertext` + `AuthTag`.

```dart
// Encrypt
final encrypted = Cryptor.encrypt('my_secret_data', 'my_password');

// Decrypt
final decrypted = Cryptor.decrypt(encrypted, 'my_password');

// Verification
final isEnc = Cryptor.isEncrypted(someString);

// Test Helper
final randPwd = Cryptor.generatePassword();
```

## UI & System Utils

### FontUtils
Helper for dynamic font loading.

```dart
// Load font from a local file path
await FontUtils.loadFrom('/path/to/font.ttf');
```

### SystemUIs
Manages system UI overlays and window configurations for different platforms.

```dart
// Android: Transparent Navigation Bar (Edge-to-Edge)
SystemUIs.setTransparentNavigationBar(context);

// Toggle Status Bar
SystemUIs.switchStatusBar(hide: true); // Immersive Sticky
SystemUIs.switchStatusBar(hide: false); // Edge-to-Edge

// Desktop: Window Initialization
await SystemUIs.initDesktopWindow(
  hideTitleBar: true,
  size: Size(800, 600),
  position: Offset.zero,
);
```
