# Android Development Guidelines

## Material Design Principles

### Core Concepts
- **Material Metaphor**: Surfaces and edges provide visual cues
- **Bold, Graphic, Intentional**: Typography, grids, space, scale, color
- **Motion Provides Meaning**: Animations should be meaningful and focused

### Navigation Patterns
- **Bottom Navigation**: 3-5 top-level destinations
- **Navigation Drawer**: 5+ destinations or secondary navigation
- **Top App Bar**: Contextual actions and navigation
- **Back Button**: System-level navigation

## Android-Specific Components

### Material Components
- **FloatingActionButton (FAB)**: Primary action button
- **Snackbar**: Brief messages about app processes
- **BottomSheet**: Slide-up panel for additional options
- **Cards**: Contained units of content
- **Chips**: Compact elements representing input, attribute, or action

### System Integration
- **Notifications**: Rich notifications with actions
- **Widgets**: Home screen app widgets
- **App Shortcuts**: Quick actions from app icon
- **Share Sheet**: System sharing interface

## Android Permissions

### Runtime Permissions
- Request permissions when needed, not at startup
- Provide clear rationale before requesting
- Handle permission denial gracefully
- Check permissions before accessing protected features

### Common Permissions
- **Camera**: CAMERA permission
- **Location**: ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION
- **Storage**: READ_EXTERNAL_STORAGE, WRITE_EXTERNAL_STORAGE (deprecated in Android 11+)
- **Contacts**: READ_CONTACTS, WRITE_CONTACTS
- **Phone**: CALL_PHONE, READ_PHONE_STATE

## Performance Considerations

### Android-Specific Optimizations
- **ProGuard/R8**: Code shrinking and obfuscation
- **App Bundle**: Dynamic delivery and smaller downloads
- **Baseline Profiles**: Improved app startup time
- **Render Thread**: Keep UI thread free

### Memory Management
- Monitor memory usage with Android Studio Profiler
- Handle low memory situations
- Optimize bitmap usage
- Clear references in onDestroy()

## Build Configuration

### Gradle Settings
```gradle
android {
    compileSdkVersion 34
    
    defaultConfig {
        minSdkVersion 21  // Android 5.0
        targetSdkVersion 34
        versionCode 1
        versionName "1.0"
    }
    
    buildTypes {
        release {
            minifyEnabled true
            proguardFiles getDefaultProguardFile('proguard-android-optimize.txt')
        }
    }
}
```

### Build Variants
- **Debug**: Development builds with debugging enabled
- **Release**: Production builds with optimizations
- **Flavors**: Different app versions (free/paid, staging/production)

## Google Play Store

### Publishing Requirements
- **App Bundle Format**: Preferred over APK
- **Target API Level**: Must target recent Android version
- **64-bit Support**: Required for native code
- **App Signing**: Play App Signing recommended

### Store Listing
- **Screenshots**: Multiple device types and orientations
- **Feature Graphic**: 1024x500px banner
- **App Icon**: 512x512px high-res icon
- **Description**: Short (80 chars) and full (4000 chars)

### Release Management
- **Internal Testing**: Limited to 100 testers
- **Closed Testing**: Targeted beta testing
- **Open Testing**: Public beta
- **Staged Rollout**: Gradual release to percentage of users

## Android-Specific React Native

### Platform-Specific Code
```javascript
import { Platform } from 'react-native';

if (Platform.OS === 'android') {
  // Android-specific code
}

// Or use Platform.select
const styles = StyleSheet.create({
  container: {
    marginTop: Platform.select({
      ios: 0,
      android: StatusBar.currentHeight,
    }),
  },
});
```

### Android-Only Props
- **elevation**: Shadow for Android (instead of iOS shadow props)
- **collapsable**: View optimization
- **renderToHardwareTextureAndroid**: Hardware acceleration
- **needsOffscreenAlphaCompositing**: Transparency rendering

### BackHandler
```javascript
import { BackHandler } from 'react-native';

useEffect(() => {
  const backHandler = BackHandler.addEventListener(
    'hardwareBackPress',
    () => {
      // Handle back button
      return true; // Prevent default
    }
  );
  
  return () => backHandler.remove();
}, []);
```

## Testing on Android

### Emulator Setup
- Use Android Virtual Device (AVD) Manager
- Test on multiple Android versions
- Test different screen sizes and densities
- Enable developer options for debugging

### Physical Device Testing
- Enable USB debugging
- Test on various manufacturers (Samsung, Google, OnePlus, etc.)
- Test on different Android versions
- Verify performance on low-end devices

## Common Issues and Solutions

### Build Issues
- **Clean and rebuild**: `cd android && ./gradlew clean`
- **Reset cache**: `npx react-native start --reset-cache`
- **Sync project**: In Android Studio, File → Sync Project

### Performance Issues
- Enable Hermes for better performance
- Use ProGuard/R8 in release builds
- Optimize images with WebP format
- Implement lazy loading for lists

### Compatibility Issues
- Check minimum SDK version requirements
- Handle different screen sizes with responsive design
- Test text scaling and font accessibility
- Verify hardware feature availability