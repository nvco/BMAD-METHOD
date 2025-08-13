# React Native iOS Troubleshooting Guide

## Development Environment Issues

### Metro Bundler Problems

**Issue: Metro won't start or keeps crashing**
```bash
# Clear Metro cache
npx react-native start --reset-cache

# Clear npm/yarn cache
npm start -- --reset-cache
# or
yarn start --reset-cache

# Nuclear option - clear everything
rm -rf node_modules
rm package-lock.json # or yarn.lock
npm install # or yarn install
```

**Issue: "Unable to resolve module" errors**
```bash
# Clear Metro resolver cache
rm -rf /tmp/metro-*

# Clear React Native cache
rm -rf ~/.metro

# Restart Metro with cache reset
npx react-native start --reset-cache
```

**Issue: Metro keeps watching deleted files**
```bash
# Clear watchman cache
watchman watch-del-all

# Reset Metro cache
npx react-native start --reset-cache
```

### iOS Simulator Issues

**Issue: Simulator is slow or unresponsive**
- Device > Erase All Content and Settings
- Hardware > Restart
- Close and reopen Simulator app
- Reduce motion in Accessibility settings

**Issue: App won't install on simulator**
```bash
# Reset simulator
xcrun simctl erase all

# Rebuild and reinstall
npx react-native run-ios --reset-cache
```

**Issue: Simulator shows white screen**
- Check Metro bundler is running
- Check for JavaScript errors in debug console
- Try reloading the app (Cmd+R)
- Check if app is actually installed

### Xcode and Build Issues

**Issue: Build fails with "Command PhaseScriptExecution failed"**
```bash
# Clean Xcode build folder
cd ios
xcodebuild clean

# Reset CocoaPods
rm -rf Pods
rm Podfile.lock
pod install
```

**Issue: "No development team selected" error**
1. Open `ios/YourApp.xcworkspace` in Xcode
2. Select your project in navigator
3. Go to Signing & Capabilities
4. Select your development team

**Issue: Duplicate symbol errors**
```bash
# Usually caused by duplicate React installations
rm -rf node_modules
rm package-lock.json
npm install

# Clean iOS build
cd ios
rm -rf build
xcodebuild clean
```

## Runtime Errors

### JavaScript Errors

**Issue: "undefined is not an object" errors**
- Check for typos in property names
- Verify imports are correct
- Check if variables are properly initialized
- Use optional chaining (?.) for potentially undefined objects

**Issue: "Cannot read property of undefined"**
```javascript
// Bad
const name = user.profile.name;

// Good
const name = user?.profile?.name;

// Or with default
const name = user?.profile?.name || 'Unknown';
```

**Issue: Network request failures**
```javascript
// Add proper error handling
const fetchData = async () => {
  try {
    const response = await fetch(url);
    if (!response.ok) {
      throw new Error(`HTTP error! status: ${response.status}`);
    }
    const data = await response.json();
    return data;
  } catch (error) {
    console.error('Fetch error:', error);
    throw error;
  }
};
```

### State Management Issues

**Issue: State updates not reflected in UI**
```javascript
// Bad - mutating state directly
state.items.push(newItem);

// Good - creating new state
setState(prevState => ({
  ...prevState,
  items: [...prevState.items, newItem]
}));
```

**Issue: Infinite re-renders**
```javascript
// Bad - dependency changes every render
useEffect(() => {
  fetchData();
}, [{ id: userId }]); // Object recreated every render

// Good - stable dependencies
useEffect(() => {
  fetchData();
}, [userId]);
```

### Navigation Issues

**Issue: Navigation prop is undefined**
```javascript
// Make sure screen is part of navigator
// Or use navigation hook
import { useNavigation } from '@react-navigation/native';

const MyComponent = () => {
  const navigation = useNavigation();
  // Use navigation here
};
```

**Issue: Can't navigate to screen**
- Check screen is registered in navigator
- Verify screen name spelling
- Check navigation stack structure
- Ensure navigation is available in context

## Performance Issues

### Slow Rendering

**Issue: UI feels sluggish**
```javascript
// Use React DevTools Profiler to identify issues
// Enable performance monitor
import { DevSettings } from 'react-native';
DevSettings.addMenuItem('Show Perf Monitor', () => {
  require('react-native/Libraries/Performance/RCTRenderingPerf').toggle();
});
```

**Issue: FlatList performance problems**
```javascript
// Optimize FlatList props
<FlatList
  data={data}
  renderItem={renderItem}
  keyExtractor={keyExtractor}
  getItemLayout={getItemLayout} // If fixed item height
  removeClippedSubviews={true}
  maxToRenderPerBatch={10}
  windowSize={10}
  initialNumToRender={10}
/>
```

**Issue: Memory leaks**
```javascript
// Clean up subscriptions and listeners
useEffect(() => {
  const subscription = eventEmitter.addListener('event', handler);
  
  return () => {
    subscription.remove();
  };
}, []);
```

### Bundle Size Issues

**Issue: Large bundle size**
```bash
# Analyze bundle
npx react-native bundle --platform ios --dev false --entry-file index.js --bundle-output bundle.js --assets-dest assets --sourcemap-output sourcemap.js

# Check what's in the bundle
npm install -g react-native-bundle-visualizer
react-native-bundle-visualizer
```

## iOS-Specific Issues

### Native Module Problems

**Issue: Native module not found**
```bash
# Relink native modules (RN < 0.60)
npx react-native unlink module-name
npx react-native link module-name

# For RN >= 0.60 with auto-linking
cd ios
rm -rf Pods
pod install
```

**Issue: CocoaPods issues**
```bash
# Update CocoaPods
sudo gem install cocoapods

# Clean and reinstall
cd ios
rm -rf Pods
rm Podfile.lock
pod deintegrate
pod install
```

### Device-Specific Issues

**Issue: App crashes on specific iOS versions**
- Check deployment target in Xcode
- Review API usage for version compatibility
- Test on devices with target iOS version
- Check crash logs in Xcode Console

**Issue: Layout issues on different screen sizes**
```javascript
// Use SafeAreaView for notch devices
import { SafeAreaView } from 'react-native-safe-area-context';

const MyScreen = () => (
  <SafeAreaView style={{ flex: 1 }}>
    {/* Your content */}
  </SafeAreaView>
);
```

**Issue: Status bar issues**
```javascript
// Control status bar appearance
import { StatusBar } from 'react-native';

<StatusBar barStyle="dark-content" backgroundColor="#ffffff" />
```

## Debugging Techniques

### Using Flipper

1. Install Flipper desktop app
2. Enable Flipper in your app:
```bash
npx react-native run-ios
```
3. Use Flipper to inspect:
   - Network requests
   - Redux state
   - Layout
   - Logs

### Using React DevTools

```bash
# Install React DevTools
npm install -g react-devtools

# Start React DevTools
react-devtools

# In your app, open developer menu and select "Debug with Chrome"
```

### Console Debugging

```javascript
// Use console methods strategically
console.log('Debug info:', data);
console.warn('Warning:', warning);
console.error('Error:', error);

// Remove console logs in production
if (__DEV__) {
  console.log('Development only log');
}
```

### Remote Debugging

1. Enable remote debugging in developer menu
2. Open Chrome DevTools
3. Use debugger statements:
```javascript
const handlePress = () => {
  debugger; // Execution will pause here
  // Your code
};
```

## Common Error Messages and Solutions

**"Task :app:installDebug FAILED"**
- Close any running emulators/simulators
- Clean project and rebuild
- Check if device has enough storage

**"Unable to load script from assets 'index.android.bundle'"**
- Make sure Metro bundler is running
- Clear Metro cache
- Check network connectivity

**"Element type is invalid"**
- Check all imports are correct
- Verify component names
- Check for circular dependencies

**"Module not found: Can't resolve"**
- Check file paths and extensions
- Verify module is installed
- Clear Metro cache

**"Cannot read property 'navigate' of undefined"**
- Ensure component is wrapped in NavigationContainer
- Use useNavigation hook for functional components
- Check navigation prop is passed correctly

## Performance Monitoring

### Using Flipper Performance Plugin

1. Open Flipper
2. Enable Performance plugin
3. Monitor:
   - Frame rate
   - Memory usage
   - CPU usage
   - Network requests

### Manual Performance Checks

```javascript
// Monitor render cycles
const renderCount = useRef(0);
renderCount.current++;
console.log(`Component rendered ${renderCount.current} times`);

// Check for unnecessary re-renders
const whyDidYouRender = (prevProps, nextProps) => {
  Object.keys(nextProps).forEach(key => {
    if (prevProps[key] !== nextProps[key]) {
      console.log(`${key} changed:`, prevProps[key], '->', nextProps[key]);
    }
  });
};
```

## Preventive Measures

### Development Best Practices

1. **Use TypeScript** for better error catching
2. **Enable ESLint** with React Native rules
3. **Write tests** for critical functionality
4. **Use error boundaries** to catch JavaScript errors
5. **Monitor performance** regularly during development
6. **Test on real devices** before releasing

### Code Quality Tools

```bash
# Install ESLint with React Native config
npm install --save-dev eslint @react-native-community/eslint-config

# Install Prettier
npm install --save-dev prettier

# Install TypeScript
npm install --save-dev typescript @types/react @types/react-native
```

### Testing Setup

```bash
# Install testing dependencies
npm install --save-dev jest @testing-library/react-native @testing-library/jest-native

# Run tests
npm test
```

Remember: Most React Native iOS issues can be resolved by clearing caches, restarting services, and following error messages carefully. When in doubt, start with the basics: clean, rebuild, and restart.