## 1. Add the dependency

```yaml
# pubspec.yaml
dependencies:
  escalated:
    git:
      url: https://github.com/escalated-dev/escalated-flutter.git
```

## 2. Install packages

```bash
$ flutter pub get
```

## 3. Wrap your app

```dart
import 'package:escalated/escalated.dart';

void main() {
  runApp(
    EscalatedPlugin(
      config: EscalatedConfig(
        apiBaseUrl: 'https://yourapp.com/support/api/v1',
      ),
      child: MyApp(),
    ),
  );
}
```

> **Note:** The Flutter package is a customer-facing UI library. Agent and admin interfaces are handled through the web application.
