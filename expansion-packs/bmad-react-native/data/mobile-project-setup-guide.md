# Mobile Project Setup Guide

## Complete Walkthrough: React Native App from Zero to Running

This guide provides a comprehensive walkthrough for setting up a React Native mobile project from scratch, covering both React Native CLI and Expo approaches.

## Prerequisites

### System Requirements

#### macOS (iOS + Android Development)
```bash
# Required tools
- Xcode 13+ (from App Store)
- Node.js 18+ (LTS recommended)
- Watchman (for file watching)
- Java Development Kit 17+
- Android Studio

# Install via Homebrew
brew install node
brew install watchman
brew install --cask adoptopenjdk/openjdk/adoptopenjdk17
```

#### Windows (Android Development)
```bash
# Required tools
- Node.js 18+ (from nodejs.org)
- Java Development Kit 17+
- Android Studio
- Git for Windows

# Install via Chocolatey (optional)
choco install nodejs
choco install adoptopenjdk17
choco install androidstudio
```

#### Linux (Android Development)
```bash
# Ubuntu/Debian
sudo apt update
sudo apt install nodejs npm openjdk-17-jdk
curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
sudo apt update && sudo apt install yarn

# Install Android Studio manually from developer.android.com
```

### Development Environment Setup

#### Android Studio Configuration
1. **Install Android Studio**
   - Download from [developer.android.com](https://developer.android.com/studio)
   - Follow installation wizard
   - Install Android SDK, Android SDK Platform, Android Virtual Device

2. **Configure Android SDK**
   ```bash
   # Add to ~/.bashrc, ~/.zshrc, or ~/.bash_profile
   export ANDROID_HOME=$HOME/Library/Android/sdk  # macOS
   export ANDROID_HOME=$HOME/Android/Sdk          # Linux
   export ANDROID_HOME=%LOCALAPPDATA%\Android\Sdk # Windows

   export PATH=$PATH:$ANDROID_HOME/emulator
   export PATH=$PATH:$ANDROID_HOME/platform-tools
   ```

3. **Create Virtual Device**
   - Open Android Studio → AVD Manager
   - Create Virtual Device → Choose device (e.g., Pixel 4)
   - Select system image (API 30+)
   - Finish and start emulator

#### iOS Setup (macOS only)
1. **Install Xcode** (from App Store)
2. **Install iOS Simulator**
   ```bash
   # Verify installation
   xcrun simctl list devices
   ```
3. **Install CocoaPods**
   ```bash
   sudo gem install cocoapods
   ```

## Project Setup Options

### Option 1: Expo Managed Workflow (Recommended for Beginners)

#### When to Choose Expo:
- **Rapid prototyping and MVP development**
- **Team lacks native development experience**
- **Standard app requirements (no exotic native features)**
- **Want OTA updates out of the box**

#### Setup Steps:
```bash
# 1. Install Expo CLI globally (optional)
npm install -g @expo/cli

# 2. Create new project
npx create-expo-app MyMobileApp
cd MyMobileApp

# 3. Start development server
npx expo start

# 4. Install Expo Go app on your device
# iOS: App Store → "Expo Go"
# Android: Google Play → "Expo Go"

# 5. Scan QR code from terminal to open on device
```

#### Project Structure (Expo):
```
MyMobileApp/
├── app.json              # Expo configuration
├── App.js                # Main app component
├── package.json          # Dependencies
├── assets/               # Images, fonts, etc.
│   ├── images/
│   └── fonts/
├── components/           # Reusable components
├── screens/             # Screen components
├── navigation/          # Navigation setup
├── services/           # API calls, storage
├── utils/              # Helper functions
└── constants/          # App constants
```

### Option 2: React Native CLI (Full Control)

#### When to Choose CLI:
- **Need custom native modules**
- **App size optimization is critical**
- **Full control over build process**
- **Enterprise apps with specific requirements**

#### Setup Steps:
```bash
# 1. Install React Native CLI
npm install -g react-native-cli

# 2. Create new project
npx react-native init MyMobileApp
cd MyMobileApp

# 3. Start Metro bundler
npx react-native start

# 4. Run on platform (separate terminals)
# iOS:
npx react-native run-ios

# Android (ensure emulator is running):
npx react-native run-android
```

#### Project Structure (React Native CLI):
```
MyMobileApp/
├── android/             # Android native code
├── ios/                 # iOS native code
├── src/                 # JavaScript source
│   ├── components/      # Reusable components
│   ├── screens/         # Screen components
│   ├── navigation/      # Navigation setup
│   ├── services/        # API, storage
│   ├── utils/          # Helpers
│   ├── types/          # TypeScript definitions
│   └── constants/      # App constants
├── __tests__/          # Test files
├── package.json        # Dependencies
├── metro.config.js     # Metro bundler config
├── babel.config.js     # Babel configuration
└── index.js           # Entry point
```

### Option 3: Expo Bare Workflow (Best of Both Worlds)

#### When to Choose Bare:
- **Started with Expo but need native modules**
- **Want Expo tooling with native flexibility**
- **Planning to eject eventually**

#### Setup Steps:
```bash
# Option A: Start with bare template
npx create-expo-app --template bare-minimum

# Option B: Eject from managed workflow
cd MyExpoApp
npx expo eject

# 3. Install dependencies
npm install

# 4. Install iOS dependencies (macOS only)
cd ios && pod install && cd ..

# 5. Start development
npx expo start

# 6. Run on platforms
npx expo run:ios
npx expo run:android
```

## Essential Dependencies

### Core Dependencies
```json
{
  "dependencies": {
    "react": "18.2.0",
    "react-native": "0.72.6",
    "@react-navigation/native": "^6.1.7",
    "@react-navigation/stack": "^6.3.17",
    "@react-navigation/bottom-tabs": "^6.5.8",
    "react-native-screens": "^3.25.0",
    "react-native-safe-area-context": "^4.7.2"
  },
  "devDependencies": {
    "@types/react": "^18.2.24",
    "@types/react-native": "^0.72.3",
    "typescript": "^5.2.2",
    "@react-native-community/eslint-config": "^3.2.0",
    "prettier": "^3.0.3"
  }
}
```

### State Management Options
```bash
# Redux Toolkit (Complex apps)
npm install @reduxjs/toolkit react-redux

# Zustand (Lightweight)
npm install zustand

# Context API (Built-in, simple state)
# No installation needed

# React Query (Server state)
npm install @tanstack/react-query
```

### UI Component Libraries
```bash
# React Native Elements
npm install react-native-elements react-native-vector-icons

# NativeBase
npm install native-base react-native-svg react-native-safe-area-context

# React Native Paper (Material Design)
npm install react-native-paper

# Expo Vector Icons (Expo projects)
npx expo install @expo/vector-icons
```

## Platform-Specific Code Organization

### File-Based Platform Separation
```bash
# Platform-specific files
Button.ios.js        # iOS implementation
Button.android.js    # Android implementation
Button.js           # Shared/fallback implementation

# Usage in code - automatic platform detection
import Button from './Button'; // Automatically picks correct platform
```

### Platform-Specific Styles
```javascript
import { Platform, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  button: {
    padding: 10,
    // Platform-specific styles
    ...Platform.select({
      ios: {
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.1,
        shadowRadius: 4,
      },
      android: {
        elevation: 4,
      },
    }),
  },
  text: {
    fontSize: Platform.OS === 'ios' ? 16 : 14,
    fontFamily: Platform.select({
      ios: 'Helvetica',
      android: 'Roboto',
    }),
  },
});
```

### Platform-Specific Components
```javascript
// components/PlatformButton/index.js
import { Platform } from 'react-native';
import IOSButton from './IOSButton';
import AndroidButton from './AndroidButton';

const PlatformButton = Platform.select({
  ios: IOSButton,
  android: AndroidButton,
});

export default PlatformButton;
```

## Development Tools Setup

### TypeScript Configuration
```bash
# Install TypeScript
npm install -D typescript @types/react @types/react-native

# Generate tsconfig.json
npx tsc --init
```

#### tsconfig.json for React Native:
```json
{
  "compilerOptions": {
    "target": "es2017",
    "lib": ["es2017", "es2018", "es5"],
    "allowJs": true,
    "skipLibCheck": true,
    "esModuleInterop": true,
    "allowSyntheticDefaultImports": true,
    "strict": true,
    "forceConsistentCasingInFileNames": true,
    "moduleResolution": "node",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "noEmit": true,
    "jsx": "react-jsx"
  },
  "include": [
    "src/**/*",
    "App.tsx",
    "index.js"
  ],
  "exclude": [
    "node_modules",
    "babel.config.js",
    "metro.config.js",
    "jest.config.js"
  ]
}
```

### ESLint & Prettier Setup
```bash
# Install ESLint and Prettier
npm install -D eslint prettier @react-native-community/eslint-config

# Install additional ESLint plugins
npm install -D eslint-plugin-react-hooks eslint-plugin-react-native
```

#### .eslintrc.js:
```javascript
module.exports = {
  root: true,
  extends: '@react-native-community',
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint'],
  overrides: [
    {
      files: ['*.ts', '*.tsx'],
      rules: {
        '@typescript-eslint/no-shadow': ['error'],
        'no-shadow': 'off',
        'no-undef': 'off',
      },
    },
  ],
};
```

#### .prettierrc.js:
```javascript
module.exports = {
  arrowParens: 'avoid',
  bracketSameLine: true,
  bracketSpacing: false,
  singleQuote: true,
  trailingComma: 'all',
  tabWidth: 2,
  semi: true,
};
```

### Debugging Setup

#### React Native Debugger (Recommended)
```bash
# macOS
brew install --cask react-native-debugger

# Windows
# Download from: https://github.com/jhen0409/react-native-debugger/releases

# Linux
# Download AppImage from releases page
```

#### Flipper (Facebook's Debugging Tool)
```bash
# Download from: https://fbflipper.com/
# Automatically integrates with React Native 0.62+

# Enable in your app (already enabled by default)
# No additional setup required for basic functionality
```

## Testing Setup

### Jest Configuration
```bash
# Install testing dependencies
npm install -D jest @testing-library/react-native @testing-library/jest-native

# For Expo projects
npx expo install jest-expo jest @types/jest
```

#### jest.config.js:
```javascript
module.exports = {
  preset: 'react-native',
  setupFilesAfterEnv: [
    '@testing-library/jest-native/extend-expect',
    '<rootDir>/jest-setup.js',
  ],
  transformIgnorePatterns: [
    'node_modules/(?!(react-native|@react-native|@react-navigation)/)',
  ],
  collectCoverageFrom: [
    'src/**/*.{js,jsx,ts,tsx}',
    '!src/**/*.d.ts',
    '!src/**/__tests__/**',
  ],
};
```

### E2E Testing (Detox)
```bash
# Install Detox
npm install -D detox

# Initialize Detox configuration
npx detox init
```

## Build Configuration

### Metro Configuration (metro.config.js)
```javascript
const { getDefaultConfig } = require('metro-config');

module.exports = (async () => {
  const {
    resolver: { sourceExts, assetExts },
  } = await getDefaultConfig();
  
  return {
    transformer: {
      babelTransformerPath: require.resolve('react-native-svg-transformer'),
    },
    resolver: {
      assetExts: assetExts.filter(ext => ext !== 'svg'),
      sourceExts: [...sourceExts, 'svg'],
    },
  };
})();
```

### Android Build Configuration

#### android/app/build.gradle key sections:
```gradle
android {
    compileSdkVersion rootProject.ext.compileSdkVersion
    buildToolsVersion rootProject.ext.buildToolsVersion

    defaultConfig {
        applicationId "com.yourdomain.yourapp"
        minSdkVersion rootProject.ext.minSdkVersion
        targetSdkVersion rootProject.ext.targetSdkVersion
        versionCode 1
        versionName "1.0"
    }

    buildTypes {
        debug {
            debuggable true
        }
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}
```

### iOS Build Configuration

#### ios/YourApp/Info.plist key sections:
```xml
<key>CFBundleDisplayName</key>
<string>Your App Name</string>
<key>CFBundleIdentifier</key>
<string>com.yourdomain.yourapp</string>
<key>CFBundleVersion</key>
<string>1</string>
<key>CFBundleShortVersionString</key>
<string>1.0</string>
```

## Environment Configuration

### Environment Variables Setup
```bash
# Install react-native-config
npm install react-native-config

# Create environment files
touch .env .env.development .env.staging .env.production
```

#### .env.development:
```bash
API_URL=https://dev-api.yourapp.com
DEBUG_MODE=true
SENTRY_DSN=your_development_sentry_dsn
```

#### .env.production:
```bash
API_URL=https://api.yourapp.com
DEBUG_MODE=false
SENTRY_DSN=your_production_sentry_dsn
```

### Config Usage in Code:
```javascript
import Config from 'react-native-config';

const API_URL = Config.API_URL;
const DEBUG_MODE = Config.DEBUG_MODE === 'true';
```

## Verification Checklist

### ✅ Development Environment Ready
- [ ] Node.js 18+ installed and working
- [ ] Package manager (npm/yarn) working
- [ ] Android Studio installed and SDK configured
- [ ] iOS development tools installed (macOS only)
- [ ] Emulator/Simulator can be launched
- [ ] React Native CLI or Expo CLI installed

### ✅ Project Successfully Created
- [ ] Project created using chosen method (Expo/CLI)
- [ ] Dependencies installed without errors
- [ ] Development server starts successfully
- [ ] App loads in emulator/simulator
- [ ] Hot reload is working
- [ ] Debugger can connect

### ✅ Development Tools Working
- [ ] TypeScript compiling (if used)
- [ ] ESLint/Prettier configured
- [ ] Tests can run
- [ ] Git repository initialized
- [ ] Environment variables loading

## Troubleshooting Common Setup Issues

### Metro Bundler Issues
```bash
# Clear Metro cache
npx react-native start --reset-cache

# Clear all caches
cd android && ./gradlew clean && cd ..
rm -rf node_modules && npm install
```

### iOS Build Issues
```bash
# Clear Xcode derived data
rm -rf ~/Library/Developer/Xcode/DerivedData

# Reinstall pods
cd ios && rm -rf Pods Podfile.lock && pod install && cd ..
```

### Android Build Issues
```bash
# Clean Android build
cd android && ./gradlew clean && cd ..

# Verify Android SDK path
echo $ANDROID_HOME

# Check emulator is running
adb devices
```

### Package Installation Issues
```bash
# Clear npm cache
npm cache clean --force

# Delete node_modules and reinstall
rm -rf node_modules package-lock.json
npm install

# For macOS users with permission issues
sudo chown -R $(whoami) ~/.npm
```

## Next Steps

After completing this setup:

1. **Read [Mobile Development Workflow](./mobile-development-workflow.md)** for day-to-day development practices
2. **Review [React Native Patterns](./react-native-patterns.md)** for coding best practices
3. **Check [Mobile Best Practices 2025](./mobile-best-practices-2025.md)** for current recommendations
4. **Reference [React Native vs Expo Decision Framework](./react-native-vs-expo-decision-framework.md)** if reconsidering your approach

Your mobile development environment is now ready for building React Native applications!