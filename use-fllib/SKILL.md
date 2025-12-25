---
name: use-fllib
description: Use fl_lib stores, widgets, utils, and extensions in Flutter apps. Use when requests mention fl_lib APIs or integration.
---

# Use fl_lib

## When to use
- Use when the user asks about fl_lib setup, localization, or Paths init.
- Use when requests mention PrefStore, SecureStore, HiveStore, AdaptiveReorderableList, Input, SizedLoading, or fl_lib extensions/utils.

## Instructions
1) **Setup**: Follow [General Setup](topics/fl_lib.md) for dependency, Paths init, and localization wiring.
2) **Stores**: Use the right store for the data type; see [Stores](topics/fl_lib_stores.md). Prefer PrefStore for settings, SecureStore for secrets, HiveStore for structured caching.
3) **Widgets**: Prefer fl_lib widgets for common UI patterns; see [Widgets](topics/fl_lib_widgets.md).
4) **Utils & extensions**: Use provided helpers for IDs, crypto, UI/system, and convenience APIs; see [Utils](topics/fl_lib_utils.md) and [Extensions](topics/fl_lib_extensions.md).
5) **Library changes**: If modifying fl_lib itself, run `./export_all.dart` in the fl_lib root.

## Requirements
### fl_lib usage
1) **Foundation**: Use fl_lib as the common library when it is already part of the project.
2) **Storage**: Use PrefStore for key-value settings and SecureStore for sensitive data; use HiveStore for local structured caching.

## Example prompts
- "Wire fl_lib localization and Paths init in main.dart"
- "Store auth tokens using SecureStore and preferences using PrefStore"
- "Build a responsive grid with AdaptiveReorderableList"
- "Use fl_lib context extensions to show a loading dialog"
- "Generate IDs with SnowflakeLite and ShortId"
