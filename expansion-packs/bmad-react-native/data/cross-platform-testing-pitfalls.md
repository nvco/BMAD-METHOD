# Cross-Platform Testing Pitfalls and Solutions

## Platform Differences That Affect Testing

### Navigation Behavior Differences
```javascript
// Pitfall: Different back button behavior
// iOS: Software back button in navigation bar
// Android: Hardware back button + software back button

// Solution: Test both navigation patterns
describe('Navigation Tests', () => {
  it('should handle iOS back button', () => {
    // Test software back button
    fireEvent.press(getByTestId('back-button'));
    expect(mockNavigation.goBack).toHaveBeenCalled();
  });
  
  it('should handle Android hardware back button', () => {
    // Mock hardware back button press
    const { BackHandler } = require('react-native');
    const backHandler = jest.spyOn(BackHandler, 'addEventListener');
    
    render(<ScreenComponent />);
    
    // Simulate hardware back button
    const backPressHandler = backHandler.mock.calls[0][1];
    const handled = backPressHandler();
    
    expect(handled).toBe(true); // Should handle the back press
  });
});
```

### Platform-Specific Component Behavior
```javascript
// Pitfall: Different behavior for same components
// Example: TouchableOpacity feedback differs between platforms

// Solution: Test platform-specific behavior
describe('TouchableOpacity Platform Tests', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });
  
  it('should provide haptic feedback on iOS', () => {
    Platform.OS = 'ios';
    const mockHapticFeedback = jest.fn();
    
    const { getByTestId } = render(
      <TouchableOpacity 
        testID="button"
        onPress={() => mockHapticFeedback()}
      >
        <Text>Press me</Text>
      </TouchableOpacity>
    );
    
    fireEvent.press(getByTestId('button'));
    
    if (Platform.OS === 'ios') {
      expect(mockHapticFeedback).toHaveBeenCalled();
    }
  });
  
  it('should handle ripple effect on Android', () => {
    Platform.OS = 'android';
    
    const { getByTestId } = render(
      <TouchableOpacity 
        testID="button"
        android_ripple={{ color: 'blue' }}
      >
        <Text>Press me</Text>
      </TouchableOpacity>
    );
    
    // Test that component renders without errors
    expect(getByTestId('button')).toBeTruthy();
  });
});
```

## Date and Time Testing Pitfalls

### Timezone and Locale Issues
```javascript
// Pitfall: Date formatting differs across platforms and locales
// Solution: Mock date and test different scenarios

describe('Date Formatting Tests', () => {
  beforeEach(() => {
    // Mock date to ensure consistent testing
    jest.useFakeTimers();
    jest.setSystemTime(new Date('2024-01-15T10:30:00Z'));
  });
  
  afterEach(() => {
    jest.useRealTimers();
  });
  
  it('should format dates consistently across platforms', () => {
    const testDate = new Date('2024-01-15T10:30:00Z');
    
    // Test with different locales
    const locales = ['en-US', 'en-GB', 'de-DE', 'ja-JP'];
    
    locales.forEach(locale => {
      const formatted = testDate.toLocaleDateString(locale);
      expect(formatted).toMatchSnapshot(`date-${locale}`);
    });
  });
  
  it('should handle timezone differences', () => {
    const testDate = new Date('2024-01-15T10:30:00Z');
    
    // Mock different timezones
    const timezones = [
      'America/New_York',
      'Europe/London', 
      'Asia/Tokyo',
      'Pacific/Auckland'
    ];
    
    timezones.forEach(timezone => {
      // Note: Full timezone testing requires additional setup
      // This is a simplified example
      const formatted = testDate.toLocaleDateString('en-US', {
        timeZone: timezone
      });
      expect(formatted).toMatchSnapshot(`timezone-${timezone}`);
    });
  });
});
```

### Time-Based Testing Issues
```javascript
// Pitfall: Tests that depend on current time can be flaky
// Solution: Mock time-dependent functionality

describe('Time-Dependent Component Tests', () => {
  it('should show correct relative time', () => {
    const mockNow = new Date('2024-01-15T10:30:00Z').getTime();
    const mockDate = new Date('2024-01-15T10:00:00Z'); // 30 minutes ago
    
    jest.spyOn(Date, 'now').mockReturnValue(mockNow);
    
    const { getByText } = render(
      <RelativeTimeComponent date={mockDate} />
    );
    
    expect(getByText('30 minutes ago')).toBeTruthy();
    
    Date.now.mockRestore();
  });
  
  it('should handle different time formats', () => {
    const testCases = [
      { input: '2024-01-15T10:30:00Z', expected: 'Jan 15, 2024' },
      { input: '2024-12-31T23:59:59Z', expected: 'Dec 31, 2024' },
      { input: '2024-02-29T12:00:00Z', expected: 'Feb 29, 2024' }, // Leap year
    ];
    
    testCases.forEach(({ input, expected }) => {
      const { getByText } = render(
        <DateDisplay date={new Date(input)} />
      );
      
      expect(getByText(expected)).toBeTruthy();
    });
  });
});
```

## Network and API Testing Pitfalls

### Different Network Behaviors
```javascript
// Pitfall: Network behavior varies between platforms and environments
// Solution: Mock network conditions and test error scenarios

describe('Network Testing', () => {
  beforeEach(() => {
    fetch.resetMocks();
  });
  
  it('should handle different network conditions', async () => {
    // Test slow network
    fetch.mockResponseOnce(
      JSON.stringify({ data: 'test' }),
      { 
        status: 200,
        headers: { 'Content-Type': 'application/json' }
      }
    );
    
    // Add artificial delay
    const mockDelayedFetch = jest.fn(() =>
      new Promise(resolve => 
        setTimeout(() => resolve(fetch()), 5000)
      )
    );
    
    global.fetch = mockDelayedFetch;
    
    const { getByTestId } = render(<ApiComponent />);
    
    // Should show loading state
    expect(getByTestId('loading-spinner')).toBeTruthy();
    
    // Wait for response
    await waitFor(() => {
      expect(getByTestId('data-display')).toBeTruthy();
    }, { timeout: 6000 });
  });
  
  it('should handle network errors gracefully', async () => {
    // Test different error scenarios
    const errorScenarios = [
      { error: new Error('Network request failed'), expectedMessage: 'Network error' },
      { error: new Error('Timeout'), expectedMessage: 'Request timeout' },
      { status: 404, expectedMessage: 'Not found' },
      { status: 500, expectedMessage: 'Server error' },
    ];
    
    for (const scenario of errorScenarios) {
      fetch.resetMocks();
      
      if (scenario.error) {
        fetch.mockRejectOnce(scenario.error);
      } else {
        fetch.mockResponseOnce('', { status: scenario.status });
      }
      
      const { getByText } = render(<ApiComponent />);
      
      await waitFor(() => {
        expect(getByText(scenario.expectedMessage)).toBeTruthy();
      });
    }
  });
});
```

### SSL and Certificate Testing
```javascript
// Pitfall: Certificate validation differs between development and production
// Solution: Test certificate handling scenarios

describe('SSL Certificate Tests', () => {
  it('should handle certificate validation errors', async () => {
    const certificateError = new Error('Certificate validation failed');
    certificateError.name = 'CertificateError';
    
    fetch.mockRejectOnce(certificateError);
    
    const { getByText } = render(<SecureApiComponent />);
    
    await waitFor(() => {
      expect(getByText('Security certificate error')).toBeTruthy();
    });
  });
  
  it('should enforce HTTPS in production', () => {
    const originalEnv = process.env.NODE_ENV;
    process.env.NODE_ENV = 'production';
    
    const httpUrl = 'http://api.example.com/data';
    const httpsUrl = 'https://api.example.com/data';
    
    // Test that HTTP URLs are upgraded to HTTPS in production
    const secureUrl = upgradeToHttps(httpUrl);
    expect(secureUrl).toBe(httpsUrl);
    
    process.env.NODE_ENV = originalEnv;
  });
});
```

## Storage Testing Pitfalls

### AsyncStorage Platform Differences
```javascript
// Pitfall: AsyncStorage behavior can differ between platforms
// Solution: Mock AsyncStorage consistently

import AsyncStorage from '@react-native-async-storage/async-storage';

describe('AsyncStorage Tests', () => {
  beforeEach(() => {
    AsyncStorage.clear();
  });
  
  it('should handle storage quota limits', async () => {
    // Test storage limits (varies by platform)
    const largeData = 'x'.repeat(10 * 1024 * 1024); // 10MB string
    
    try {
      await AsyncStorage.setItem('large-data', largeData);
      
      // If it succeeds, verify we can retrieve it
      const retrieved = await AsyncStorage.getItem('large-data');
      expect(retrieved).toBe(largeData);
    } catch (error) {
      // Handle quota exceeded error
      expect(error.message).toMatch(/quota/i);
    }
  });
  
  it('should handle concurrent access', async () => {
    // Test concurrent read/write operations
    const promises = [];
    
    for (let i = 0; i < 10; i++) {
      promises.push(
        AsyncStorage.setItem(`key-${i}`, `value-${i}`)
      );
    }
    
    await Promise.all(promises);
    
    // Verify all values were stored correctly
    for (let i = 0; i < 10; i++) {
      const value = await AsyncStorage.getItem(`key-${i}`);
      expect(value).toBe(`value-${i}`);
    }
  });
  
  it('should handle storage corruption gracefully', async () => {
    // Mock storage corruption
    AsyncStorage.getItem.mockImplementationOnce(() => {
      throw new Error('Storage corrupted');
    });
    
    const { getByText } = render(<StorageComponent />);
    
    await waitFor(() => {
      expect(getByText('Storage error - data has been reset')).toBeTruthy();
    });
  });
});
```

## Permission Testing Pitfalls

### Platform-Specific Permissions
```javascript
// Pitfall: Permission systems differ significantly between iOS and Android
// Solution: Test permission flows for both platforms

import { request, PERMISSIONS, RESULTS } from 'react-native-permissions';

describe('Permission Tests', () => {
  beforeEach(() => {
    jest.clearAllMocks();
  });
  
  it('should handle camera permission on iOS', async () => {
    Platform.OS = 'ios';
    
    const permissionScenarios = [
      { result: RESULTS.GRANTED, expectedAction: 'open_camera' },
      { result: RESULTS.DENIED, expectedAction: 'show_permission_dialog' },
      { result: RESULTS.BLOCKED, expectedAction: 'show_settings_prompt' },
    ];
    
    for (const scenario of permissionScenarios) {
      request.mockResolvedValueOnce(scenario.result);
      
      const { getByTestId } = render(<CameraComponent />);
      
      fireEvent.press(getByTestId('camera-button'));
      
      await waitFor(() => {
        expect(getByTestId(scenario.expectedAction)).toBeTruthy();
      });
    }
  });
  
  it('should handle camera permission on Android', async () => {
    Platform.OS = 'android';
    
    // Android has more granular permission states
    const androidScenarios = [
      { result: RESULTS.GRANTED, expectedAction: 'open_camera' },
      { result: RESULTS.DENIED, expectedAction: 'show_permission_rationale' },
      { result: RESULTS.NEVER_ASK_AGAIN, expectedAction: 'show_settings_prompt' },
    ];
    
    for (const scenario of androidScenarios) {
      request.mockResolvedValueOnce(scenario.result);
      
      const { getByTestId } = render(<CameraComponent />);
      
      fireEvent.press(getByTestId('camera-button'));
      
      await waitFor(() => {
        expect(getByTestId(scenario.expectedAction)).toBeTruthy();
      });
    }
  });
});
```

## Font and Typography Testing

### Font Rendering Differences
```javascript
// Pitfall: Fonts render differently across platforms
// Solution: Test with platform-specific font fallbacks

describe('Typography Tests', () => {
  it('should use correct fonts per platform', () => {
    const { getByTestId } = render(<TextComponent />);
    const textElement = getByTestId('styled-text');
    
    const computedStyle = getComputedStyle(textElement);
    
    if (Platform.OS === 'ios') {
      expect(computedStyle.fontFamily).toMatch(/San Francisco|SF Pro/);
    } else {
      expect(computedStyle.fontFamily).toMatch(/Roboto|sans-serif/);
    }
  });
  
  it('should handle missing custom fonts gracefully', () => {
    // Test fallback when custom font is not available
    const { getByTestId } = render(
      <Text style={{ fontFamily: 'NonExistentFont' }} testID="text">
        Test Text
      </Text>
    );
    
    const textElement = getByTestId('text');
    
    // Should fall back to system font
    expect(textElement).toBeTruthy();
    // Font should not be 'NonExistentFont'
    const computedStyle = getComputedStyle(textElement);
    expect(computedStyle.fontFamily).not.toMatch(/NonExistentFont/);
  });
  
  it('should maintain text scaling accessibility', () => {
    // Test with different text scale settings
    const textScales = [0.85, 1.0, 1.15, 1.3, 2.0];
    
    textScales.forEach(scale => {
      // Mock text scale setting
      jest.doMock('react-native', () => ({
        ...jest.requireActual('react-native'),
        PixelRatio: {
          getFontScale: () => scale,
        },
      }));
      
      const { getByTestId } = render(<ScalableTextComponent />);
      const textElement = getByTestId('scalable-text');
      
      expect(textElement).toBeTruthy();
      // Text should be readable at all scale levels
    });
  });
});
```

## Animation Testing Pitfalls

### Platform Animation Differences
```javascript
// Pitfall: Animations behave differently across platforms
// Solution: Test animation states and completion

describe('Animation Tests', () => {
  beforeEach(() => {
    jest.useFakeTimers();
  });
  
  afterEach(() => {
    jest.useRealTimers();
  });
  
  it('should complete animations on both platforms', () => {
    const onAnimationComplete = jest.fn();
    
    const { getByTestId } = render(
      <AnimatedComponent onComplete={onAnimationComplete} />
    );
    
    // Start animation
    fireEvent.press(getByTestId('animate-button'));
    
    // Fast-forward time to complete animation
    jest.advanceTimersByTime(1000);
    
    expect(onAnimationComplete).toHaveBeenCalled();
  });
  
  it('should handle animation interruption', () => {
    const { getByTestId, unmount } = render(<AnimatedComponent />);
    
    // Start animation
    fireEvent.press(getByTestId('animate-button'));
    
    // Unmount component during animation
    unmount();
    
    // Should not crash or cause memory leaks
    jest.advanceTimersByTime(1000);
  });
  
  it('should respect reduced motion settings', () => {
    // Mock reduced motion preference
    jest.doMock('react-native', () => ({
      ...jest.requireActual('react-native'),
      AccessibilityInfo: {
        isReduceMotionEnabled: () => Promise.resolve(true),
      },
    }));
    
    const { getByTestId } = render(<AnimatedComponent />);
    
    // Animation should be instant or very short with reduced motion
    fireEvent.press(getByTestId('animate-button'));
    
    // Animation should complete immediately
    expect(getByTestId('animation-complete')).toBeTruthy();
  });
});
```

## Device Orientation Testing

### Orientation Change Handling
```javascript
// Pitfall: Orientation changes affect layout and functionality differently
// Solution: Test orientation change scenarios

describe('Orientation Tests', () => {
  it('should handle orientation changes gracefully', () => {
    const { getByTestId, rerender } = render(<ResponsiveComponent />);
    
    // Test portrait orientation
    mockDeviceOrientation('portrait');
    rerender(<ResponsiveComponent />);
    
    expect(getByTestId('portrait-layout')).toBeTruthy();
    
    // Test landscape orientation
    mockDeviceOrientation('landscape');
    rerender(<ResponsiveComponent />);
    
    expect(getByTestId('landscape-layout')).toBeTruthy();
  });
  
  it('should maintain state during orientation changes', () => {
    const { getByTestId } = render(<StatefulComponent />);
    
    // Set some state
    fireEvent.changeText(getByTestId('input'), 'test value');
    
    // Change orientation
    mockDeviceOrientation('landscape');
    
    // State should be preserved
    expect(getByTestId('input').props.value).toBe('test value');
  });
});

const mockDeviceOrientation = (orientation) => {
  const mockDimensions = {
    portrait: { width: 375, height: 812 },
    landscape: { width: 812, height: 375 },
  };
  
  jest.doMock('react-native', () => ({
    ...jest.requireActual('react-native'),
    Dimensions: {
      get: () => mockDimensions[orientation],
      addEventListener: jest.fn(),
      removeEventListener: jest.fn(),
    },
  }));
};
```

## Testing Best Practices for Cross-Platform

### Comprehensive Test Setup
```javascript
// jest.setup.js - Platform-agnostic test setup
import 'react-native-gesture-handler/jestSetup';
import mockAsyncStorage from '@react-native-async-storage/async-storage/jest/async-storage-mock';

// Mock AsyncStorage
jest.mock('@react-native-async-storage/async-storage', () => mockAsyncStorage);

// Mock react-native modules
jest.mock('react-native', () => {
  const RN = jest.requireActual('react-native');
  
  // Mock platform-specific modules
  RN.Platform.OS = 'ios'; // Default to iOS, override in specific tests
  
  return RN;
});

// Mock navigation
jest.mock('@react-navigation/native', () => ({
  ...jest.requireActual('@react-navigation/native'),
  useNavigation: () => ({
    navigate: jest.fn(),
    goBack: jest.fn(),
    reset: jest.fn(),
  }),
  useRoute: () => ({
    params: {},
  }),
}));

// Mock permissions
jest.mock('react-native-permissions', () => ({
  request: jest.fn(() => Promise.resolve('granted')),
  check: jest.fn(() => Promise.resolve('granted')),
  PERMISSIONS: {
    IOS: { CAMERA: 'ios.permission.CAMERA' },
    ANDROID: { CAMERA: 'android.permission.CAMERA' },
  },
  RESULTS: {
    GRANTED: 'granted',
    DENIED: 'denied',
    BLOCKED: 'blocked',
    NEVER_ASK_AGAIN: 'never_ask_again',
  },
}));

// Global test utilities
global.Platform = {
  OS: 'ios',
  select: (obj) => obj.ios || obj.default,
};

// Mock timers by default
jest.useFakeTimers();
```

This comprehensive guide helps identify and avoid common cross-platform testing pitfalls, ensuring robust applications that work consistently across iOS and Android platforms.