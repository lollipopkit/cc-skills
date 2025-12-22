# fl_lib Setup & Usage

## Installation
Add the dependency to your `pubspec.yaml` pointing to the GitHub repository:

```yaml
dependencies:
  fl_lib:
    git:
      url: https://github.com/lppcg/fl_lib.git
      ref: main
```

## Initialization
Before running `runApp`, you must initialize the `Paths` utility:

```dart
void main() async {
  // Initialize fl_lib Paths
  await Paths.init();
  runApp(MyApp());
}
```

## Localization
Configure `localizationsDelegates` in your `MaterialApp` to include `LibLocalizations.delegate`. This ensures fl_lib's internal widgets and utilities are properly localized.

```dart
MaterialApp(
  localizationsDelegates: const [
    LibLocalizations.delegate,
    ...AppLocalizations.localizationsDelegates,
  ],
  supportedLocales: AppLocalizations.supportedLocales,
)
```

In your main app widget (e.g., in `didChangeDependencies`), call `context.setLibL10n()` to synchronize localization settings:

```dart
@override
void didChangeDependencies() {
  super.didChangeDependencies();
  context.setLibL10n();
}
```

## Maintenance
If you are modifying `fl_lib` itself (e.g., adding new files), remember to run the `./export_all.dart` script in the `fl_lib` root to update exports.
