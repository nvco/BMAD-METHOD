# Mobile Development Workflow

## Day-to-Day Development Process for React Native Projects

This guide outlines the optimal workflow for daily React Native development, covering everything from starting your development session to deploying updates.

## Daily Development Workflow

### 1. Start Development Session

#### Environment Startup Checklist
```bash
# 1. Start emulator/simulator first (before Metro)
# Android
emulator -avd Pixel_4_API_30

# iOS (macOS only)
open -a Simulator

# 2. Verify device is ready
adb devices                    # Android
xcrun simctl list devices      # iOS

# 3. Start Metro bundler
npx expo start                 # Expo projects
# OR
npx react-native start        # React Native CLI projects

# 4. Install/update app on device (if needed)
npx expo run:android          # Expo
npx expo run:ios              # Expo
# OR
npx react-native run-android  # CLI
npx react-native run-ios      # CLI
```

#### Quick Start Script (package.json)
```json
{
  "scripts": {
    "dev:android": "npx react-native run-android",
    "dev:ios": "npx react-native run-ios",
    "dev:expo": "npx expo start",
    "clean:metro": "npx react-native start --reset-cache",
    "clean:android": "cd android && ./gradlew clean && cd ..",
    "clean:ios": "rm -rf ios/build && cd ios && rm -rf Pods Podfile.lock && pod install && cd ..",
    "clean:all": "rm -rf node_modules && npm install",
    "test": "jest",
    "test:watch": "jest --watch",
    "lint": "eslint . --ext .js,.jsx,.ts,.tsx",
    "type-check": "tsc --noEmit"
  }
}
```

### 2. Feature Development Cycle

#### A. Planning Phase (Before Coding)
```bash
# 1. Check current state
git status
git pull origin main

# 2. Create feature branch
git checkout -b feature/user-authentication

# 3. Review requirements and design
# - Check Figma/design files
# - Review user stories or PRD
# - Identify platform-specific requirements
```

#### B. Implementation Phase
```bash
# 1. Start with component structure
mkdir src/screens/AuthScreen
touch src/screens/AuthScreen/index.tsx
touch src/screens/AuthScreen/styles.ts
touch src/screens/AuthScreen/hooks.ts

# 2. Implement platform-agnostic logic first
# 3. Add platform-specific code as needed
# 4. Test frequently on both platforms
```

#### C. Testing During Development
```bash
# Run tests continuously
npm run test:watch

# Type checking
npm run type-check

# Linting
npm run lint

# Manual testing on multiple devices
# - iOS Simulator (different device sizes)
# - Android Emulator (different API levels)
# - Physical devices (when possible)
```

### 3. Cross-Platform Development Best Practices

#### Platform Testing Strategy
```javascript
// Test matrix for each feature
const TESTING_MATRIX = {
  ios: {
    simulator: ['iPhone 14', 'iPhone SE', 'iPad Air'],
    versions: ['iOS 15', 'iOS 16', 'iOS 17'],
    testing_points: ['UI layout', 'Navigation', 'Permissions', 'Performance']
  },
  android: {
    emulator: ['Pixel 4', 'Nexus 5X', 'Tablet'],
    versions: ['API 28', 'API 30', 'API 33'],
    testing_points: ['UI layout', 'Navigation', 'Permissions', 'Performance']
  }
};
```

#### Code Organization for Cross-Platform
```bash
# Feature-based structure
src/
├── features/
│   ├── authentication/
│   │   ├── components/
│   │   │   ├── LoginForm.tsx
│   │   │   ├── LoginForm.ios.tsx    # iOS-specific
│   │   │   └── LoginForm.android.tsx # Android-specific
│   │   ├── hooks/
│   │   │   └── useAuth.ts
│   │   ├── services/
│   │   │   └── authService.ts
│   │   └── types/
│   │       └── auth.types.ts
│   └── navigation/
├── shared/
│   ├── components/         # Reusable UI components
│   ├── services/          # API clients, storage
│   ├── utils/             # Helper functions
│   ├── hooks/             # Custom hooks
│   └── constants/         # App constants
└── platform/
    ├── ios/               # iOS-specific code
    └── android/           # Android-specific code
```

### 4. Hot Reload and Fast Refresh Workflow

#### Optimizing Development Speed
```javascript
// Enable Fast Refresh for optimal development experience
// In your component files, follow these patterns:

// ✅ Good - Fast Refresh friendly
const UserProfile = ({ userId }) => {
  const [user, setUser] = useState(null);
  
  useEffect(() => {
    fetchUser(userId).then(setUser);
  }, [userId]);
  
  return <UserProfileView user={user} />;
};

// ❌ Avoid - Breaks Fast Refresh
export default ({ userId }) => {
  // Anonymous components don't work well with Fast Refresh
};
```

#### Fast Refresh Best Practices
```bash
# When Fast Refresh stops working:
# 1. Check console for syntax errors
# 2. Ensure components are named (not anonymous)
# 3. Restart Metro if needed
r + Enter  # In Metro terminal to reload

# Force refresh when needed
Cmd+R (iOS Simulator)
R+R (Android Emulator)
```

### 5. Debugging Workflow

#### Debug Tools Setup
```bash
# 1. React Native Debugger (preferred)
# Start before launching app
react-native-debugger

# 2. Flipper (Facebook's tool)
# Automatically connects to running app

# 3. Chrome DevTools (basic)
# Open Chrome → chrome://inspect → select your app

# 4. Console debugging in app
# Shake device → Debug → "Debug JS Remotely"
```

#### Common Debugging Scenarios
```javascript
// 1. Network debugging
console.log('API Request:', { url, method, data });
// Use Flipper Network tab for detailed inspection

// 2. State debugging
console.log('Component state:', JSON.stringify(state, null, 2));
// Use React DevTools for component tree

// 3. Performance debugging
import { systrace } from 'react-native';
systrace.beginEvent('ExpensiveOperation');
// ... expensive operation
systrace.endEvent();

// 4. Native debugging
// iOS: Xcode → Debug → View Debugging → Capture View Hierarchy
// Android: Layout Inspector in Android Studio
```

#### Platform-Specific Debugging
```bash
# iOS Debugging
# 1. Xcode logs
xcrun simctl spawn booted log stream --predicate 'process == "YourApp"'

# 2. Device logs (physical device)
# Xcode → Window → Devices and Simulators → select device → Open Console

# Android Debugging
# 1. Logcat
adb logcat -s ReactNative:V -s ReactNativeJS:V

# 2. Specific tag filtering
adb logcat -s "YourAppTag:*"

# 3. View crash logs
adb shell dumpsys dropbox --print
```

### 6. Code Quality Workflow

#### Pre-commit Workflow
```bash
# Install Husky for git hooks
npm install -D husky lint-staged

# Add to package.json
{
  "husky": {
    "hooks": {
      "pre-commit": "lint-staged"
    }
  },
  "lint-staged": {
    "*.{js,jsx,ts,tsx}": [
      "eslint --fix",
      "prettier --write",
      "git add"
    ]
  }
}
```

#### Daily Quality Checks
```bash
# Morning routine (after git pull)
npm run type-check     # TypeScript errors
npm run lint          # Code style issues
npm run test         # Unit tests
npm run clean:metro   # Clear Metro cache if issues

# Before committing
npm run test         # Run all tests
npm run lint         # Final lint check
npm run type-check   # Final type check
git add .
git commit -m "feat: add user authentication"
```

### 7. Performance Monitoring Workflow

#### Daily Performance Checks
```javascript
// 1. Monitor bundle size
import { Alert } from 'react-native';

// In development, log bundle stats
if (__DEV__) {
  console.log('Bundle loaded at:', new Date().toISOString());
}

// 2. Monitor memory usage
import { DeviceInfo } from 'react-native';
const memoryInfo = await DeviceInfo.getUsedMemory();
console.log('Memory usage:', memoryInfo);

// 3. Track render performance
import { unstable_trace as trace } from 'scheduler/tracing';

const ExpensiveComponent = () => {
  return trace('ExpensiveComponent render', performance.now(), () => {
    return <ComplexUI />;
  });
};
```

#### Performance Testing Routine
```bash
# Weekly performance testing
# 1. Profile with Hermes (Android)
npx react-native run-android --variant=release

# 2. iOS Instruments profiling
# Build release version in Xcode → Product → Profile

# 3. Bundle analysis
npx react-native bundle --platform android --dev false --entry-file index.js --bundle-output android-bundle.js --analyze
```

### 8. Build and Release Workflow

#### Development Build Testing
```bash
# 1. Test release builds locally
# iOS
npx react-native run-ios --configuration Release

# Android
npx react-native run-android --variant=release

# 2. Test different environments
APP_ENV=staging npx react-native run-android
APP_ENV=production npx react-native run-ios
```

#### Pre-release Checklist
```bash
# ✅ Functionality testing
- [ ] All features work on both platforms
- [ ] Navigation flows complete
- [ ] Form validation working
- [ ] Error handling tested
- [ ] Offline functionality (if applicable)

# ✅ Performance testing
- [ ] App starts quickly (< 3 seconds)
- [ ] Smooth scrolling and animations
- [ ] Memory usage acceptable
- [ ] No memory leaks detected
- [ ] Battery usage reasonable

# ✅ Platform-specific testing
- [ ] iOS: Haptic feedback, Face ID/Touch ID
- [ ] Android: Back button, deep links
- [ ] Push notifications working
- [ ] Camera/location permissions
- [ ] App store guidelines compliance
```

### 9. Troubleshooting Common Daily Issues

#### Metro Bundler Issues
```bash
# Symptoms: App won't reload, white screen, bundle errors
# Solutions:
npx react-native start --reset-cache
rm -rf node_modules && npm install
killall node  # Kill all Node processes

# Nuclear option
watchman watch-del-all
rm -rf node_modules
rm -rf /tmp/metro-*
npm install
npx react-native start --reset-cache
```

#### Platform-Specific Issues
```bash
# iOS: Build failures
rm -rf ios/build
cd ios && rm -rf Pods Podfile.lock && pod install && cd ..

# Android: Gradle issues
cd android && ./gradlew clean && cd ..
rm -rf android/.gradle

# Both: Permission issues
# Check Android permissions in AndroidManifest.xml
# Check iOS permissions in Info.plist
```

#### Development Server Issues
```bash
# Port conflicts
lsof -ti:8081 | xargs kill -9  # Kill process on port 8081
npx react-native start --port 8088  # Use different port

# Device connection issues
adb devices                    # Check Android devices
adb reverse tcp:8081 tcp:8081  # Port forwarding for Android
```

### 10. Collaboration Workflow

#### Team Development Best Practices
```bash
# Daily sync process
git pull origin main
npm install  # Update dependencies
npx react-native start --reset-cache  # Fresh start

# Feature branch workflow
git checkout -b feature/new-feature
# ... develop feature ...
git add .
git commit -m "feat: implement new feature"
git push origin feature/new-feature
# Create pull request

# Code review checklist
- [ ] Works on both iOS and Android
- [ ] No TypeScript errors
- [ ] Tests added/updated
- [ ] No console.log statements in production code
- [ ] Follows project coding standards
- [ ] Performance impact considered
```

#### Shared Development Environment
```javascript
// .env.shared (team configuration)
METRO_PORT=8081
FLIPPER_ENABLED=true
DEV_MENU_ENABLED=true
FAST_REFRESH_ENABLED=true

// Team debugging settings
const DEBUG_CONFIG = {
  logLevel: __DEV__ ? 'verbose' : 'error',
  enableFlipperIntegration: __DEV__,
  enableNetworkInspector: __DEV__,
  enableReduxDevTools: __DEV__,
};
```

### 11. Productivity Tips

#### Keyboard Shortcuts (Development)
```bash
# Metro bundler shortcuts
r + Enter     # Reload app
d + Enter     # Toggle Developer Menu
j + Enter     # Open debugger (Chrome)
i + Enter     # Run on iOS simulator
a + Enter     # Run on Android emulator

# Simulator shortcuts
Cmd+R         # Reload (iOS)
Cmd+D         # Developer menu (iOS)
Cmd+Shift+H   # Home button (iOS)
Cmd+Shift+S   # Screenshot (iOS)

# Android Emulator
Ctrl+M        # Developer menu
R+R           # Reload
Ctrl+Shift+P  # Power button
F2            # Rename variable (Android Studio)
```

#### Development Efficiency Tools
```javascript
// 1. Auto-import helpers (VS Code)
// Install "React Native Tools" extension

// 2. Snippet libraries
// Create custom snippets for common patterns
{
  "React Native Functional Component": {
    "prefix": "rnfc",
    "body": [
      "import React from 'react';",
      "import { View, Text, StyleSheet } from 'react-native';",
      "",
      "const ${1:ComponentName} = () => {",
      "  return (",
      "    <View style={styles.container}>",
      "      <Text>${2:Hello World}</Text>",
      "    </View>",
      "  );",
      "};",
      "",
      "const styles = StyleSheet.create({",
      "  container: {",
      "    flex: 1,",
      "    justifyContent: 'center',",
      "    alignItems: 'center',",
      "  },",
      "});",
      "",
      "export default ${1:ComponentName};"
    ]
  }
}

// 3. Live templates for common patterns
// - API service functions
// - Navigation setup
// - State management boilerplate
```

## Workflow Optimization

### Weekly Routine
- **Monday**: Update dependencies, check for security vulnerabilities
- **Wednesday**: Performance review, memory profiling
- **Friday**: Clean builds, test on physical devices

### Monthly Routine
- Update React Native version (if stable)
- Review and update development tools
- Clean up unused dependencies
- Archive old feature branches

### Quarterly Routine
- Major dependency updates
- Performance audit
- Security audit
- Development environment refresh

This workflow ensures consistent, efficient, and high-quality React Native development across teams and projects.