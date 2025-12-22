# fl_lib Widgets

fl_lib provides a rich collection of production-ready widgets, focusing on responsiveness, adaptability, and common UI patterns.

## AdaptiveReorderableList
A powerful, responsive multi-column reorderable list that adapts to screen width.

### Features
- **Responsive Layout**: Automatically calculates column count based on available width.
- **Dual Layout Modes**:
  - `useMasonry: true` (default): Waterfall/Masonry layout (minimizes vertical gaps).
  - `useMasonry: false` (or `rowMajor: true`): Aligned row-major grid (preserves order).
- **Animations**:
  - `animationDuration`: Insert/Remove animations.
  - `dropAnimationDuration`: Drag-and-drop settle animations.
  - `insertCurve` / `removeCurve`: Customizable curves.
- **Drag & Drop**: Long-press to drag. Includes feedback opacity (`draggingChildOpacity`).
- **Separators**: Supports `AdaptiveReorderableList.separated` constructor.

### Usage
```dart
AdaptiveReorderableList.builder<String>(
  items: myItems,
  itemKey: (item) => item.id,
  itemBuilder: (context, item, index, animation) {
     return SizeTransition(
       sizeFactor: animation,
       child: MyCard(item),
     );
  },
  onReorderComplete: (newItems) {
    setState(() => myItems = newItems);
  },
  // Optional customizations
  maxColumns: 4,
  columnWidth: 300,
  crossAxisSpacing: 16,
  mainAxisSpacing: 16,
)
```

## Input
A high-level wrapper around `TextField` designed to reduce boilerplate.

### Key Features
- **Auto-Card Wrapping**: By default, wraps input in a `CardX` for consistent styling. Use `noWrap: true` to disable.
- **Password Toggle**: If `obscureText: true`, automatically adds a visibility toggle icon.
- **Reactive IME**: Respects global IME suggestions setting via `PrefProps.imeSuggestions`.
- **Context Menu**: Uses `AdaptiveTextSelectionToolbar` by default.

### Usage
```dart
Input(
  label: 'Password',
  obscureText: true,
  icon: Icons.lock,
  onChanged: (val) => print(val),
  // Validators/Error text
  errorText: _errorMsg,
  // Custom actions
  onSubmitted: (val) => _submit(),
)
```

## SizedLoading
Standardized loading indicators to ensure consistency across the app.

### Predefined Sizes
- `SizedLoading.small`: 25x25 (e.g., inside buttons)
- `SizedLoading.medium`: 45x45 (e.g., card loading)
- `SizedLoading.large`: 65x65 (e.g., page loading)

### Custom Usage
```dart
// Custom size with padding
SizedLoading(30, padding: 5)

// Custom builder (e.g., linear)
SizedLoading(
  100, 
  builder: SizedLoading.linearBuilder
)
```

## Other Notable Widgets

### Layout & Containers
- **AdaptiveList**: Similar to reorderable list but static.
- **CardX**: An extended `Card` widget with better defaults for the design system.
- **Split**: A split-view widget for resizable panes.
- **VirtualWindowFrame**: For desktop apps, handles custom window frame rendering.

### Interactive
- **Btn**: Standardized buttons (implementations in `src/view/widget/btn`).
- **Choice**: Chip-like selection widgets.
- **ColorPicker**: A simple color selection widget.
- **SlideTrans**: Slide transition wrapper.

### Content
- **Markdown**: Wrapper for `flutter_markdown` with custom styling.
- **Tag**: Tag/Badge component.
- **Turnstile**: Cloudflare Turnstile integration widget.
