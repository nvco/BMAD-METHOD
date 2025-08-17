# Mobile Development Troubleshooting Guide

## React Native Common Issues

### Metro Bundler Issues

#### Problem: Metro bundler fails to start
```bash
# Error: Metro has encountered an error
# Solution: Reset Metro cache
npx react-native start --reset-cache

# Or clear watchman and node_modules
watchman watch-del-all
rm -rf node_modules
npm install
```

#### Problem: Module not found errors
```bash
# Error: Unable to resolve module
# Solutions:
1. Check file path and case sensitivity
2. Clear Metro cache: npx react-native start --reset-cache
3. Reset node_modules: rm -rf node_modules && npm install
4. Check package.json dependencies
```

### iOS-Specific Issues

#### Problem: Build fails with Xcode errors
```bash
# Common solutions:
1. Clean build folder: Product → Clean Build Folder
2. Delete derived data: ~/Library/Developer/Xcode/DerivedData
3. Reset iOS Simulator: Device → Erase All Content and Settings
4. Check iOS deployment target matches project settings
```

#### Problem: App crashes on iOS device but works in simulator
```bash
# Debugging steps:
1. Check device logs in Xcode: Window → Devices and Simulators
2. Verify provisioning profiles and certificates
3. Check for 64-bit compatibility issues
4. Test with different iOS versions
```

#### Problem: CocoaPods issues
```bash
# Solutions:
cd ios
pod deintegrate
pod cache clean --all
pod install

# If still failing:
sudo gem install cocoapods
cd ios && pod repo update
pod install
```

### Android-Specific Issues

#### Problem: Android build fails with Gradle errors
```bash
# Common solutions:
1. Clean project: cd android && ./gradlew clean
2. Update Gradle wrapper: ./gradlew wrapper --gradle-version=7.5.1
3. Check Android SDK and build tools versions
4. Clear Gradle cache: rm -rf ~/.gradle/caches
```

#### Problem: Unable to connect to Metro on Android device
```bash
# Solutions:
1. Enable USB debugging
2. Run: adb reverse tcp:8081 tcp:8081
3. Check device is connected: adb devices
4. Shake device and select "Dev Settings" → "Debug server host"
   Enter: localhost:8081
```

#### Problem: Android app crashes on startup
```bash
# Debugging steps:
1. Check logcat: adb logcat *:E
2. Verify targetSdkVersion and compileSdkVersion
3. Check for missing permissions in AndroidManifest.xml
4. Ensure Hermes is properly configured
```

## Performance Issues

### Slow List Rendering
```javascript
// Problem: Large lists causing performance issues
// Solution: Use FlatList with optimization props
<FlatList
  data={data}
  renderItem={renderItem}
  keyExtractor={keyExtractor}
  // Performance optimizations
  removeClippedSubviews={true}
  maxToRenderPerBatch={10}
  updateCellsBatchingPeriod={100}
  windowSize={10}
  initialNumToRender={10}
  getItemLayout={getItemLayout} // If fixed height
/>
```

### Memory Leaks
```javascript
// Problem: Memory usage keeps increasing
// Solutions:
1. Clean up event listeners in useEffect cleanup
useEffect(() => {
  const subscription = EventEmitter.addListener('event', handler);
  return () => subscription.remove();
}, []);

2. Remove navigation listeners
useEffect(() => {
  const unsubscribe = navigation.addListener('focus', handler);
  return unsubscribe;
}, [navigation]);

3. Cancel async operations
useEffect(() => {
  let cancelled = false;
  
  const fetchData = async () => {
    const result = await api.getData();
    if (!cancelled) {
      setData(result);
    }
  };
  
  fetchData();
  return () => { cancelled = true; };
}, []);
```

### Slow Animations
```javascript
// Problem: Animations are choppy
// Solutions:
1. Use native driver
Animated.timing(value, {
  toValue: 1,
  duration: 1000,
  useNativeDriver: true, // Enable this
}).start();

2. Use react-native-reanimated for complex animations
import Animated, { useSharedValue, withTiming } from 'react-native-reanimated';

3. Avoid animating layout properties
// Bad: animating width/height
// Good: animating transform: [{ scale }]
```

## Navigation Issues

### Navigation State Issues
```javascript
// Problem: Navigation state not updating correctly
// Solution: Use navigation.reset for complete state reset
navigation.reset({
  index: 0,
  routes: [{ name: 'Home' }],
});

// Problem: Back button not working on Android
// Solution: Handle hardware back button
import { BackHandler } from 'react-native';

useEffect(() => {
  const backHandler = BackHandler.addEventListener('hardwareBackPress', () => {
    // Handle back press
    return true; // Prevent default behavior
  });
  
  return () => backHandler.remove();
}, []);
```

### Deep Linking Issues
```javascript
// Problem: Deep links not working
// Solutions:
1. Configure URL schemes properly in Info.plist (iOS) and AndroidManifest.xml
2. Test with adb command:
adb shell am start -W -a android.intent.action.VIEW -d "yourapp://screen" com.yourapp

3. Handle initial URL and URL changes:
import { Linking } from 'react-native';

const handleInitialURL = async () => {
  const url = await Linking.getInitialURL();
  if (url) handleDeepLink(url);
};

const handleURLChange = (url) => {
  handleDeepLink(url);
};

Linking.addEventListener('url', handleURLChange);
```

## Network and API Issues

### API Request Failures
```javascript
// Problem: Network requests failing
// Solutions:
1. Check network permissions (Android)
2. Use HTTPS (required on newer Android versions)
3. Handle network errors properly:

const apiCall = async () => {
  try {
    const response = await fetch(url, {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      },
    });
    
    if (!response.ok) {
      throw new Error(`HTTP ${response.status}: ${response.statusText}`);
    }
    
    return await response.json();
  } catch (error) {
    if (error.message === 'Network request failed') {
      // Handle offline scenario
    }
    throw error;
  }
};
```

### CORS Issues (Development)
```javascript
// Problem: CORS errors during development
// Solutions:
1. Configure Metro to proxy requests
2. Use a development server with CORS enabled
3. For testing, disable web security (not for production):
// metro.config.js
module.exports = {
  server: {
    port: 8081,
    // Add CORS headers for development
  },
};
```

## State Management Issues

### Redux/Context Issues
```javascript
// Problem: Components not re-rendering when state changes
// Solutions:
1. Ensure proper selector usage with Redux
const user = useSelector(state => state.user); // Correct
const { user } = useSelector(state => state); // May not trigger re-render

2. Use proper dependencies in useEffect
useEffect(() => {
  // Some effect
}, [dependency1, dependency2]); // Include all dependencies

3. Check for state mutations
// Bad: mutating state directly
state.user.name = 'New Name';

// Good: creating new state
return {
  ...state,
  user: {
    ...state.user,
    name: 'New Name'
  }
};
```

## Device-Specific Issues

### iPhone X+ Safe Area Issues
```javascript
// Problem: Content hidden behind notch or home indicator
// Solution: Use react-native-safe-area-context
import { SafeAreaProvider, SafeAreaView } from 'react-native-safe-area-context';

const App = () => (
  <SafeAreaProvider>
    <SafeAreaView style={{ flex: 1 }}>
      <YourContent />
    </SafeAreaView>
  </SafeAreaProvider>
);
```

### Android Hardware Back Button
```javascript
// Problem: Back button exits app instead of navigating
// Solution: Handle in navigation or specific screens
import { useFocusEffect } from '@react-navigation/native';
import { BackHandler } from 'react-native';

useFocusEffect(
  useCallback(() => {
    const onBackPress = () => {
      if (canGoBack) {
        navigation.goBack();
        return true;
      }
      return false;
    };

    const subscription = BackHandler.addEventListener('hardwareBackPress', onBackPress);
    return () => subscription.remove();
  }, [canGoBack, navigation])
);
```

## Debugging Tools and Techniques

### React Native Debugger
```bash
# Install and setup
npm install -g react-native-debugger

# Enable for iOS
npx react-native run-ios --configuration Debug

# For Android, shake device and select "Debug"
```

### Flipper Debugging
```bash
# Install Flipper desktop app
# Add to your project:
npm install react-native-flipper --save-dev

# iOS: Add to Podfile
pod 'FlipperKit', :configurations => ['Debug']

# Android: Already included in RN 0.62+
```

### Performance Profiling
```javascript
// Use React DevTools Profiler
import { Profiler } from 'react';

const onRenderCallback = (id, phase, actualDuration) => {
  console.log('Render stats:', { id, phase, actualDuration });
};

<Profiler id="UserList" onRender={onRenderCallback}>
  <UserList />
</Profiler>

// Use Performance Monitor
import { unstable_trace as trace } from 'scheduler/tracing';

trace('UserList render', performance.now(), () => {
  // Component rendering
});
```

### Network Debugging
```javascript
// Enable network inspector
if (__DEV__) {
  require('react-native-network-logger').startNetworkLogging();
}

// Or use Flipper Network plugin
// Automatically captures all network requests
```

## Platform-Specific Debugging

### iOS Debugging
```bash
# Xcode Console for device logs
# Instruments for performance profiling
# Simulator → Device → Photos to add test images

# Common Xcode shortcuts:
# Cmd+R: Run
# Cmd+.: Stop
# Cmd+Shift+K: Clean build folder
```

### Android Debugging
```bash
# ADB commands for debugging:
adb logcat                    # View logs
adb shell dumpsys meminfo    # Memory usage
adb shell dumpsys batterystats # Battery usage
adb devices                  # List connected devices
adb reverse tcp:8081 tcp:8081 # Port forwarding

# Android Studio Profiler:
# CPU, Memory, Network, Energy profiling
```

## Common Error Messages and Solutions

### "Metro has encountered an error"
- Clear Metro cache: `npx react-native start --reset-cache`
- Delete node_modules and reinstall
- Check for syntax errors in JavaScript files

### "Unable to resolve module"
- Check import paths and file names
- Verify package installation: `npm list package-name`
- Clear Metro cache and restart

### "Build failed with Gradle errors"
- Clean Android project: `cd android && ./gradlew clean`
- Update Android Gradle Plugin version
- Check Java version compatibility

### "CocoaPods could not find compatible versions"
- Update CocoaPods: `sudo gem install cocoapods`
- Update pod repo: `pod repo update`
- Clear CocoaPods cache: `pod cache clean --all`

### "App crashes on launch"
- Check device logs for crash details
- Verify app permissions in manifest files
- Test on different devices/OS versions
- Check for compatibility issues with third-party libraries

## Performance Monitoring in Production

### Crash Reporting
```javascript
// Firebase Crashlytics
import crashlytics from '@react-native-firebase/crashlytics';

// Log custom errors
crashlytics().recordError(new Error('Custom error'));

// Set user attributes
crashlytics().setUserId('user123');
```

### Performance Monitoring
```javascript
// Firebase Performance
import perf from '@react-native-firebase/perf';

// Trace custom operations
const trace = await perf().startTrace('user_list_load');
await loadUserList();
await trace.stop();
```

### Memory Monitoring
```javascript
// Monitor memory usage
import { Platform } from 'react-native';

if (Platform.OS === 'ios') {
  // Use native memory monitoring
} else {
  // Android memory monitoring
  const memInfo = await NativeModules.MemoryInfo.getMemoryInfo();
  console.log('Memory usage:', memInfo);
}
```