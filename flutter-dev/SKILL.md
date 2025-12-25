---
name: flutter-dev
description: Build and debug Flutter/Dart apps with Riverpod (codegen), Freezed, GoRouter, and fl_lib. Use when implementing Flutter features, running apps, hot reload/restart, or debugging UI.
---

# Flutter Dev Tools

## When to use
- Use when the user is working on Flutter/Dart features, running the app, hot reload/restart, or debugging UI.
- Use when requests mention Riverpod, Freezed, GoRouter, fl_lib, or Flutter widget structure.

## Instructions
1) **Setup**: Ensure the project root is added via `dart___add_roots`. List devices with `dart___list_devices` before launching.
2) **Run & lifecycle**: Use `dart___launch_app` to run on a device. Use `dart___hot_reload` for UI changes (preserves state) and `dart___hot_restart` for logic/state resets. Avoid `flutter run` via shell. Stop apps with `dart___stop_app`.
3) **Debug & inspect**: Connect DTD with `dart___connect_dart_tooling_daemon` when needed. Use `dart___get_widget_tree`, `dart___get_runtime_errors`, and `dart___get_app_logs`.
4) **Testing & maintenance**: Run tests with `dart___run_tests`. Manage deps via `dart___pub`. Analyze/fix with `dart___analyze_files` and `dart___dart_fix`.
5) **Code generation**: `dart run build_runner build --delete-conflicting-outputs` (one-time) or `dart run build_runner watch --delete-conflicting-outputs` (watch).

## Requirements
### Architecture & tech stack
1) **State Management**: Must use **Riverpod** with code generation (`@riverpod`).
2) **Data Models**: Must use **Freezed** for immutable data classes and unions.
3) **Dependency Injection**: Must use **GetIt** and **Injectable** for service location.
4) **Routing**: Must use **GoRouter** for navigation (declarative routing).
5) **Common Library**: Must utilize **fl_lib** as the foundation. See [General Setup](topics/fl_lib.md), [Stores](topics/fl_lib_stores.md), [Widgets](topics/fl_lib_widgets.md), [Utils](topics/fl_lib_utils.md), and [Extensions](topics/fl_lib_extensions.md). Core includes `Loggers`, `Dio`, and `AppLinks`.
6) **Database**: Must use **SQLite** for structured data storage; use `PrefStore` (from fl_lib) for simple key-value/settings storage.
7) **Widget State Structure (Stateful/Stateless)**: Follow [Structure Details](topics/state_structure.md) and split widget classes into UI, Actions, and Utils extensions.

## Project Structure
- core/ - Core services and singletons
  - config/ - App configuration
  - di/ - Dependency injection setup (GetIt/Injectable)
  - routing/ - GoRouter configuration
  - utils/ - General utilities
- data/ - Data models and storage
  - consts/ - Constant definitions
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

## Additional guidelines
- **Formatting**: Do NOT run `dart format`. Follow the project's existing code style.
- **Deprecations**: Replace all `Color.withOpacity` usage with `Color.withValues` (Flutter 3.27+).
- **Testing**: `utils` classes require unit test coverage.

## Example prompts
- "Run the flutter app on the iOS simulator"
- "Hot reload the app to show the new colors"
- "Create a new Riverpod provider for user authentication using code gen"
- "Implement a settings page using fl_lib's PrefStore and AdaptiveList"
- "Add a SQLite table for storing todo items"
- "Add a new route for the profile page using GoRouter"
- "Fix analysis errors in the project"
- "Generate a Freezed model for User with name and age fields"
