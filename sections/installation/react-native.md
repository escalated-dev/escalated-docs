## 1. Install the package

```bash
git clone https://github.com/escalated-dev/escalated-react-native.git
cd escalated-react-native
npm install
npm run typecheck
```

Install the local source package into your app. The source package is not published on npm.

## 2. Install peer dependencies

```bash
$ npx expo install @react-navigation/native @react-navigation/bottom-tabs @react-navigation/native-stack react-native-screens react-native-safe-area-context
```

## 3. Wrap your app

```tsx
import { EscalatedProvider } from '@escalated-dev/escalated-react-native';

export default function App() {
  return (
    <EscalatedProvider config={{ apiBaseUrl: 'https://yourapp.com/support/api/v1' }}>
      <NavigationContainer>
        {/* Your app navigation */}
      </NavigationContainer>
    </EscalatedProvider>
  );
}
```

> **Note:** The React Native package is a customer-facing UI library. Agent and admin interfaces are handled through the web application.
