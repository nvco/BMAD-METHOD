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

## Material Design System

### Typography
- **Roboto**: Primary typeface for Android
- **Type Scale**: Predefined sizes for consistency
- **Font Weights**: Regular (400), Medium (500), Bold (700)

**Material Type Scale**:
- Headline 1: 96sp (Light)
- Headline 2: 60sp (Light)
- Headline 3: 48sp (Regular)
- Headline 4: 34sp (Regular)
- Headline 5: 24sp (Regular)
- Headline 6: 20sp (Medium)
- Subtitle 1: 16sp (Regular)
- Subtitle 2: 14sp (Medium)
- Body 1: 16sp (Regular)
- Body 2: 14sp (Regular)
- Button: 14sp (Medium, All Caps)
- Caption: 12sp (Regular)
- Overline: 10sp (Regular, All Caps)

### Color System
- **Primary**: Main brand color
- **Primary Variant**: Darker/lighter primary
- **Secondary**: Accent color
- **Secondary Variant**: Darker/lighter secondary
- **Background**: App background color
- **Surface**: Component backgrounds
- **Error**: Error states and messages
- **On-[Color]**: Text/icons on colored backgrounds

### Spacing and Layout
- **Baseline Grid**: 8dp grid system
- **Keylines**: 16dp margins, 72dp for list items
- **Touch Targets**: Minimum 48dp
- **Elevation**: 0dp to 24dp for layering

## Android-Specific Components

### Material Components
- **FloatingActionButton (FAB)**: Primary action button
- **Snackbar**: Brief messages about app processes
- **BottomSheet**: Slide-up panel for additional options
- **Cards**: Contained units of content
- **Chips**: Compact elements representing input, attribute, or action
- **App Bar**: Top navigation and actions
- **Navigation View**: Side navigation drawer

### System Integration
- **Notifications**: Rich notifications with actions
- **Widgets**: Home screen app widgets
- **App Shortcuts**: Quick actions from app icon
- **Share Sheet**: System sharing interface
- **Adaptive Icons**: Support for themed icons (Android 13+)

## Android Permissions

### Runtime Permissions (API 23+)
- Request permissions when needed, not at startup
- Provide clear rationale before requesting
- Handle permission denial gracefully
- Check permissions before accessing protected features

### Common Permissions
- **Camera**: CAMERA permission
- **Location**: ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION
- **Storage**: Scoped storage (Android 11+), legacy external storage
- **Contacts**: READ_CONTACTS, WRITE_CONTACTS
- **Phone**: CALL_PHONE, READ_PHONE_STATE
- **Microphone**: RECORD_AUDIO
- **Notification**: POST_NOTIFICATIONS (Android 13+)

## Performance Considerations

### Android-Specific Optimizations
- **ProGuard/R8**: Code shrinking and obfuscation
- **App Bundle**: Dynamic delivery and smaller downloads
- **ANR Prevention**: Keep main thread responsive
- **Memory Management**: Handle low memory situations
- **Battery Optimization**: Doze mode and app standby

### Background Processing
- **Foreground Services**: Long-running tasks
- **WorkManager**: Deferred, reliable work
- **JobScheduler**: System-managed background work
- **Doze Mode**: Idle device optimization

## React Native Implementation Notes

### Android-Specific Components
```javascript
// Android-specific components
import { 
  ToastAndroid, 
  BackHandler, 
  PermissionsAndroid,
  DrawerLayoutAndroid 
} from 'react-native';

// Android Toast
ToastAndroid.show('Message', ToastAndroid.SHORT);

// Handle hardware back button
BackHandler.addEventListener('hardwareBackPress', () => {
  // Handle back press
  return true; // Prevent default behavior
});

// Request permissions
const requestCameraPermission = async () => {
  const granted = await PermissionsAndroid.request(
    PermissionsAndroid.PERMISSIONS.CAMERA,
    {
      title: 'Camera Permission',
      message: 'App needs camera access to take photos',
      buttonNeutral: 'Ask Me Later',
      buttonNegative: 'Cancel',
      buttonPositive: 'OK',
    }
  );
  return granted === PermissionsAndroid.RESULTS.GRANTED;
};
```

### Material Design Styling
```javascript
// Material Design colors and styling
const styles = StyleSheet.create({
  materialButton: {
    backgroundColor: '#6200EE', // Material Purple
    borderRadius: 4,
    elevation: 2, // Android shadow
    paddingVertical: 12,
    paddingHorizontal: 24,
  },
  materialCard: {
    backgroundColor: '#FFFFFF',
    borderRadius: 8,
    elevation: 4,
    margin: 16,
    padding: 16,
  },
  materialText: {
    fontFamily: Platform.OS === 'android' ? 'Roboto' : 'System',
    fontSize: 16,
    lineHeight: 24,
  },
});
```

### Navigation Patterns
```javascript
// Bottom navigation (Material Design)
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import MaterialIcons from 'react-native-vector-icons/MaterialIcons';

const Tab = createBottomTabNavigator();

function BottomTabNavigator() {
  return (
    <Tab.Navigator
      screenOptions={({ route }) => ({
        tabBarIcon: ({ focused, color, size }) => {
          let iconName;
          if (route.name === 'Home') {
            iconName = 'home';
          } else if (route.name === 'Settings') {
            iconName = 'settings';
          }
          return <MaterialIcons name={iconName} size={size} color={color} />;
        },
        tabBarActiveTintColor: '#6200EE',
        tabBarInactiveTintColor: 'gray',
      })}
    >
      <Tab.Screen name="Home" component={HomeScreen} />
      <Tab.Screen name="Settings" component={SettingsScreen} />
    </Tab.Navigator>
  );
}
```

## Android Version Support

### API Level Considerations
- **Minimum SDK**: API 21 (Android 5.0) recommended
- **Target SDK**: Latest stable API level
- **Compile SDK**: Latest available API level

### Version-Specific Features
- **Android 6.0 (API 23)**: Runtime permissions
- **Android 8.0 (API 26)**: Background execution limits
- **Android 9.0 (API 28)**: Network security config
- **Android 10 (API 29)**: Scoped storage
- **Android 11 (API 30)**: Package visibility
- **Android 12 (API 31)**: Material You, splash screens
- **Android 13 (API 33)**: Notification permissions, themed icons

## Accessibility

### Android Accessibility Services
- **TalkBack**: Screen reader for Android
- **Switch Access**: Navigation using switches
- **Voice Access**: Voice-controlled navigation
- **High Contrast Text**: Enhanced text visibility

### Implementation
```javascript
// Accessibility props for Android
<TouchableOpacity
  accessible={true}
  accessibilityLabel="Save document"
  accessibilityHint="Saves the current document"
  accessibilityRole="button"
>
  <Text>Save</Text>
</TouchableOpacity>
```

## Common Android Pitfalls in React Native

1. **Hardware Back Button**: Not handling Android back button properly
2. **Permission Issues**: Not requesting runtime permissions
3. **APK Size**: Large APK files affecting download rates
4. **Battery Optimization**: Apps killed by aggressive battery optimization
5. **Fragment State**: Not handling activity lifecycle properly
6. **Keyboard Issues**: Keyboard covering input fields
7. **Network Security**: HTTP blocked on API 28+
8. **Splash Screen**: Not implementing proper splash screen (Android 12+)

## Google Play Store Guidelines

### App Quality
- Follow Material Design principles
- Support multiple screen sizes and densities
- Handle configuration changes properly
- Implement proper error handling

### Store Listing Requirements
- Provide app descriptions in supported languages
- Include screenshots for phones and tablets
- Create feature graphic and app icon
- Follow content policy guidelines

### Technical Requirements
- Target recent API levels (within 1-2 years)
- Use Android App Bundle for distribution
- Sign app with upload key
- Test on multiple devices and Android versions

## Performance Optimization

### Android-Specific Optimizations
- **Hermes Engine**: Use Hermes for better performance
- **ProGuard/R8**: Enable code shrinking and obfuscation
- **Image Optimization**: Use appropriate image formats and sizes
- **Memory Management**: Handle memory pressure events
- **Network Optimization**: Cache responses and minimize requests

### Debugging Tools
- **Android Studio Profiler**: CPU, memory, network profiling
- **Systrace**: System-level performance analysis
- **Method Tracing**: Detailed method call analysis
- **Layout Inspector**: View hierarchy debugging