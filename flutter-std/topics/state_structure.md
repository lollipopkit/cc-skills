# Widget State Structure (Stateful/Stateless)

To maintain clean and manageable code, split widget classes into three parts using `extensions` within the same file. This applies to both `StatefulWidget` (`State` class) and `StatelessWidget` (the widget class), separating UI from logic and event handling.

## Structure

1.  **UI**: The main `State` class containing the `build()` method and widget definitions.
2.  **Actions**: An extension on the `State` class for event handlers (e.g., `_onTap`, `_submit`).
3.  **Utils**: An extension on the `State` class for private helper methods and business logic.

## Example (StatefulWidget)

```dart
import 'package:flutter/material.dart';

class MyPage extends StatefulWidget {
  const MyPage({super.key});

  @override
  State<MyPage> createState() => _MyPageState();
}

// 1. UI - Main State Class
class _MyPageState extends State<MyPage> {
  final _controller = TextEditingController();

  @override
  void dispose() {
    _controller.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('My Page')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Column(
          children: [
            TextField(
              controller: _controller,
              decoration: const InputDecoration(labelText: 'Enter text'),
            ),
            const SizedBox(height: 20),
            ElevatedButton(
              onPressed: _onSubmit, // Reference to Actions extension
              child: const Text('Submit'),
            ),
          ],
        ),
      ),
    );
  }
}

// 2. Actions - Event Handlers
extension _MyPageActions on _MyPageState {
  void _onSubmit() {
    final text = _controller.text;
    if (_validateInput(text)) { // Reference to Utils extension
      _showSuccessDialog(text);
    } else {
      _showErrorSnackBar();
    }
  }

  void _showSuccessDialog(String text) {
    showDialog(
      context: context,
      builder: (_) => AlertDialog(
        title: const Text('Success'),
        content: Text('You entered: $text'),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('OK'),
          ),
        ],
      ),
    );
  }
}

// 3. Utils - Helper Methods & Logic
extension _MyPageUtils on _MyPageState {
  bool _validateInput(String text) {
    return text.isNotEmpty && text.length > 3;
  }

  void _showErrorSnackBar() {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Input must be at least 4 characters')),
    );
  }
}
```

## Example (StatelessWidget)

```dart
import 'package:flutter/material.dart';

class MyStatelessPage extends StatelessWidget {
  const MyStatelessPage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: const Text('My Stateless Page')),
      body: Center(
        child: ElevatedButton(
          onPressed: () => _onSubmit(context), // Reference to Actions extension
          child: const Text('Submit'),
        ),
      ),
    );
  }
}

// 2. Actions - Event Handlers
extension _MyStatelessPageActions on MyStatelessPage {
  void _onSubmit(BuildContext context) {
    if (_validateInput('ok')) { // Reference to Utils extension
      _showSuccessDialog(context);
    } else {
      _showErrorSnackBar(context);
    }
  }

  void _showSuccessDialog(BuildContext context) {
    showDialog(
      context: context,
      builder: (_) => AlertDialog(
        title: const Text('Success'),
        content: const Text('Submitted.'),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: const Text('OK'),
          ),
        ],
      ),
    );
  }
}

// 3. Utils - Helper Methods & Logic
extension _MyStatelessPageUtils on MyStatelessPage {
  bool _validateInput(String text) {
    return text.isNotEmpty;
  }

  void _showErrorSnackBar(BuildContext context) {
    ScaffoldMessenger.of(context).showSnackBar(
      const SnackBar(content: Text('Invalid input')),
    );
  }
}
```
