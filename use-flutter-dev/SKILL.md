---
name: use-flutter-dev
description: Develop, debug, and manage Flutter applications using specialized Dart/Flutter tools. Enforces Riverpod (code gen), Freezed, fl_lib, GetIt/Injectable, GoRouter, and SQLite architecture.
---

# Use Flutter Dev Tools

## Architecture & Tech Stack Requirements
1) **State Management**: Must use **Riverpod** with code generation (`@riverpod`).
2) **Data Models**: Must use **Freezed** for immutable data classes and unions.
3) **Dependency Injection**: Must use **GetIt** and **Injectable** for service location.
4) **Routing**: Must use **GoRouter** for navigation (declarative routing).
5) **Common Library**: Must utilize **fl_lib** (github: lollipopkit/fl_lib) as the foundation.
   - **Setup & Usage**: [General Setup](topics/fl_lib.md)
   - **Stores**: [Store Details](topics/fl_lib_stores.md) - `PrefStore` (settings), `SecureStore` (sensitive), `HiveStore` (NoSQL).
   - **Widgets**: [Widget Details](topics/fl_lib_widgets.md) - `AdaptiveReorderableList`, `Input`, `SizedLoading`, etc.
   - **Utils**: [Utils Details](topics/fl_lib_utils.md) - `SnowflakeLite` (IDs), `Cryptor` (encryption), `SystemUIs`.
   - **Extensions**: [Extension Details](topics/fl_lib_extensions.md) - Rich extensions for `BuildContext`, `DateTime`, `String`, `Widget`, etc.
   - **Core**: `Loggers`, `Dio`, `AppLinks`.
6) **Database**: Must use **SQLite** for structured data storage.
   - Use `PrefStore` (from fl_lib) for simple key-value/settings storage.

## Project Structure
- core/ - Core services and singletons
   - config/ - App configuration
   - di/ - Dependency injection setup (GetIt/Injectable)
   - routing/ - GoRouter configuration
   - utils/ - General utilities
- data/ - Data models and storage
  - models/ - Freezed data models
  - providers/ - Riverpod providers (using code generation)
  - repos/ - Data access layer
  - services/ - External services (API, Database, etc.)
- views/ - UI components and pages
  - pages/ - Main pages
  - widgets/ - Reusable widgets
  - pops/ - Popups and dialogs
- app.dart - App entry point widget
- main.dart - Main entry file

## Additional Guidelines
- Follow code style and formatting rules in `.vscode/settings.json`. Do not auto-format code if it conflicts.
- `utils` classes require unit test coverage.

## Instructions
1) **Setup**: 
   - Ensure the project root is added via `dart___add_roots`.
   - List available devices with `dart___list_devices` before launching apps.

2) **Running & Lifecycle**:
   - Use `dart___launch_app` to run applications on a specific device.
   - **Crucial**: Use `dart___hot_reload` for quick UI changes (preserves state) and `dart___hot_restart` for app logic/state resets. 
   - Avoid `flutter run` via shell; use the dedicated tools to maintain control.
   - Stop apps using `dart___stop_app` with the correct PID.

3) **Debugging & Inspection**:
   - Connect to the Dart Tooling Daemon (`dart___connect_dart_tooling_daemon`) if needed for advanced inspection.
   - Inspect the UI structure using `dart___get_widget_tree`.
   - Check for runtime errors using `dart___get_runtime_errors`.
   - View logs with `dart___get_app_logs`.

4) **Testing & Maintenance**:
   - Run tests using `dart___run_tests` (supports filtering, tags, and specialized reporting).
   - Manage packages (add/get/upgrade) using `dart___pub`.
   - Analyze code health with `dart___analyze_files` and fix issues with `dart___dart_fix`.
    - **Code Generation**: Run `dart run build_runner build --delete-conflicting-outputs` when modifying Riverpod providers or Freezed models.

## Example prompts
- "Run the flutter app on the iOS simulator"
- "Hot reload the app to show the new colors"
- "Create a new Riverpod provider for user authentication using code gen"
- "Implement a settings page using fl_lib's PrefStore and AdaptiveList"
- "Add a SQLite table for storing todo items"
- "Add a new route for the profile page using GoRouter"
- "Fix analysis errors in the project"
- "Generate a Freezed model for User with name and age fields"
