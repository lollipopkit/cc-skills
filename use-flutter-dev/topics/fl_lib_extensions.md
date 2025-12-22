# fl_lib Extensions

fl_lib provides a comprehensive set of Dart extensions to reduce boilerplate and enhance developer productivity.

## BuildContext Extensions
Found in `src/core/ext/ctx/common.dart` and `dialog.dart`.

### Navigation & Theme
```dart
context.pop();             // Safer Navigator.pop
context.canPop;            // Check if can pop
context.theme;             // Theme.of(context)
context.isDark;            // Check brightness
context.mediaQuery;        // MediaQuery.of(context)
context.windowSize;        // MediaQuery.sizeOf(context) (Optimized)
context.libL10n;           // Access library localization
```

### Responsive Design
Using `responsive_framework`:
```dart
context.responsiveBreakpoints; // Raw data
context.isMobile;              // Phone or Mobile breakpoint
context.isDesktop;             // Desktop or Tablet breakpoint
```

### Dialogs & Overlays
```dart
// Show a consistent rounded dialog
await context.showRoundDialog(
  title: 'Hello',
  child: Text('Content'),
  actions: [TextButton(child: Text('OK'))], // Or use Btnx.cancelOks
);

// Show loading dialog with async task
await context.showLoadingDialog(
  fn: () async => await doSomething(),
);

// Show password input dialog
final pwd = await context.showPwdDialog(title: 'Enter Password');

// Show pickers
final selected = await context.showPickDialog(
  items: ['A', 'B', 'C'],
  multi: true,
);
```

## Widget Extensions
Found in `src/core/ext/widget.dart`. Use these for cleaner UI code.

```dart
Text('Hello')
  .center()                    // Center(child: ...)
  .paddingAll(8)               // Padding(padding: EdgeInsets.all(8), child: ...)
  .paddingSymmetric(horizontal: 16)
  .expanded(flex: 2)           // Expanded(flex: 2, child: ...)
  .tap(onTap: () => print('tapped')); // InkWell wrapper with throttle
  
// Sliver conversion
Container().sliver();          // SliverToBoxAdapter(child: ...)
```

## String Extensions
Found in `src/core/ext/string.dart`.

### Manipulation & Validation
```dart
'hello'.capitalize;        // "Hello"
'#FF0000'.fromColorHex;    // Color(0xFFFF0000)
'https://example.com'.isUrl; 
'https://example.com'.launchUrl();
```

### Path & File
```dart
'/path/to'.joinPath('file.txt');
'/path/to/file.txt'.getFileName(); // "file.txt"
'/path/to/file.txt'.getFileName(withoutExtension: true); // "file"
```

### DateTime Parsing
```dart
'2023-01-01'.parseDateTime();
'1672531200000'.parseTimestamp();
```

### Image Provider
```dart
'https://img.com/a.png'.imageProvider; // Handles Network, Asset, and File automatically
```

## Collection Extensions
Found in `src/core/ext/iter.dart`.

```dart
// List
[1, 2, 3].joinWith(0);        // [1, 0, 2, 0, 3]

// Iterable Null Safety
list.firstOrNull;
list.firstWhereOrNull((e) => e > 5);
list.nullOrEmpty;             // Checks if null or empty
```

## DateTime Extensions
Found in `src/core/ext/datetime.dart`.

```dart
final now = DateTime.now();
now.hourMinute;     // "14:30"
now.ymd();          // "2023-05-20"
now.hms();          // "14:30:45"
now.simple();       // Smart format: "14:30", "Yesterday 14:30", or "5-20"
DateTimeX.timestamp; // Current millis
```

## Riverpod & State Extensions
Found in `src/core/ext/ctx/common.dart`.

```dart
// In ConsumerState
refSafe;        // Returns ref only if mounted
contextSafe;    // Returns context only if mounted
setStateSafe(() {}); // setState only if mounted
```
