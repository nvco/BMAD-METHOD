# React Native Performance Monitoring Setup Guide

## Overview

Performance monitoring in React Native involves tracking key metrics during development and production to ensure optimal user experience. This guide covers essential tools and setup procedures for comprehensive performance monitoring.

## Development-Time Monitoring

### 1. React DevTools Profiler

**Purpose**: Monitor React component performance and rendering patterns

**Setup for React Native**:
```bash
# Install React DevTools globally
npm install -g react-devtools

# Start React DevTools (run this in separate terminal)
react-devtools
```

**In your app**:
```javascript
// Add to index.js (development only)
if (__DEV__) {
  import('react-devtools-core').then((devtools) => {
    devtools.connectToDevTools();
  });
}
```

**What to Monitor**:
- Component render frequency
- Props changes causing unnecessary renders
- Component mount/unmount cycles
- State update patterns

### 2. Flipper Integration

**Purpose**: Comprehensive debugging and performance monitoring

**Setup**:
```bash
# Install Flipper desktop app
# Download from: https://fbflipper.com/

# For React Native 0.62+, Flipper comes pre-configured
# For older versions, install manually:
npm install --save-dev react-native-flipper
```

**Available Plugins**:
- **React DevTools**: Component tree and state inspection
- **Network Inspector**: API calls, response times, payload analysis
- **Logs**: Console logs and crash reports
- **Layout Inspector**: View hierarchy and styling
- **Redux Debugger**: State management monitoring
- **Performance**: Frame rate monitoring
- **Crash Reporter**: Exception tracking

**Key Performance Features**:
```javascript
// Enable performance monitoring
import { logger } from 'react-native-flipper';

// Log performance markers
logger.logPerformance('screen_render_start', { screen: 'ProfileScreen' });
// ... render logic ...
logger.logPerformance('screen_render_end', { screen: 'ProfileScreen' });
```

### 3. React Native Performance Monitor

**Purpose**: Built-in FPS monitoring

**Setup**:
```javascript
// In your main App component (development only)
import { YellowBox } from 'react-native';

if (__DEV__) {
  // Show performance monitor
  // Shake device or press Cmd+D (iOS) / Cmd+M (Android)
  // Select "Show Perf Monitor"
}
```

**Metrics Displayed**:
- **RAM Usage**: Current memory consumption
- **FPS (JS)**: JavaScript thread frame rate
- **FPS (UI)**: UI thread frame rate
- **Bundle Size**: JavaScript bundle size

### 4. Metro Bundle Analyzer

**Purpose**: Analyze bundle size and identify large dependencies

**Setup**:
```bash
# Generate bundle analysis
npx react-native bundle \
  --platform ios \
  --dev false \
  --entry-file index.js \
  --bundle-output bundle.js \
  --sourcemap-output bundle.map

# Analyze with source-map-explorer
npm install -g source-map-explorer
source-map-explorer bundle.js bundle.map
```

## Runtime Performance Monitoring

### 1. Custom Performance Tracker

**Implementation**:
```javascript
// utils/PerformanceTracker.js
class PerformanceTracker {
  static startTimer(label) {
    if (__DEV__) {
      console.time(label);
    }
    return Date.now();
  }

  static endTimer(label, startTime) {
    const duration = Date.now() - startTime;
    
    if (__DEV__) {
      console.timeEnd(label);
      console.log(`${label} took ${duration}ms`);
    }

    // Log to analytics in production
    if (!__DEV__ && duration > 1000) {
      // Send to monitoring service
      this.logSlowOperation(label, duration);
    }
  }

  static logSlowOperation(operation, duration) {
    // Send to Firebase Analytics, Mixpanel, etc.
    analytics.track('slow_operation', {
      operation,
      duration,
      platform: Platform.OS,
      version: DeviceInfo.getVersion(),
    });
  }
}

// Usage
const timer = PerformanceTracker.startTimer('api_fetch');
await fetchData();
PerformanceTracker.endTimer('api_fetch', timer);
```

### 2. Screen Load Time Monitoring

**Implementation**:
```javascript
// hooks/useScreenLoadTime.js
import { useEffect, useRef } from 'react';
import { PerformanceTracker } from '../utils/PerformanceTracker';

export const useScreenLoadTime = (screenName) => {
  const startTime = useRef(Date.now());

  useEffect(() => {
    const loadTime = Date.now() - startTime.current;
    PerformanceTracker.logScreenLoad(screenName, loadTime);
  }, [screenName]);
};

// Usage in screen components
const ProfileScreen = () => {
  useScreenLoadTime('ProfileScreen');
  // ... screen content
};
```

### 3. List Performance Monitoring

**FlatList Optimization Tracking**:
```javascript
// components/OptimizedFlatList.js
import React, { useCallback, useMemo } from 'react';
import { FlatList } from 'react-native';

const OptimizedFlatList = ({ data, renderItem, ...props }) => {
  const keyExtractor = useCallback((item, index) => {
    return item.id?.toString() || index.toString();
  }, []);

  const memoizedRenderItem = useCallback(({ item, index }) => {
    const startTime = Date.now();
    const result = renderItem({ item, index });
    
    if (__DEV__) {
      const renderTime = Date.now() - startTime;
      if (renderTime > 16) { // 60fps = 16ms per frame
        console.warn(`Slow render for item ${index}: ${renderTime}ms`);
      }
    }
    
    return result;
  }, [renderItem]);

  const getItemLayout = useMemo(() => {
    // Return layout function if items have consistent height
    return props.itemHeight 
      ? (data, index) => ({
          length: props.itemHeight,
          offset: props.itemHeight * index,
          index,
        })
      : undefined;
  }, [props.itemHeight]);

  return (
    <FlatList
      data={data}
      renderItem={memoizedRenderItem}
      keyExtractor={keyExtractor}
      getItemLayout={getItemLayout}
      maxToRenderPerBatch={10}
      windowSize={10}
      removeClippedSubviews={true}
      {...props}
    />
  );
};
```

## Production Monitoring

### 1. Crash Reporting Setup

**Firebase Crashlytics**:
```bash
# Install
npm install @react-native-firebase/app @react-native-firebase/crashlytics

# iOS configuration
cd ios && pod install
```

```javascript
// App.js
import crashlytics from '@react-native-firebase/crashlytics';

// Enable crashlytics collection
crashlytics().setCrashlyticsCollectionEnabled(true);

// Log errors
const logError = (error, context) => {
  crashlytics().recordError(error);
  crashlytics().log(JSON.stringify(context));
};

// Custom crash reporting
const reportCrash = (error, isFatal = false) => {
  if (isFatal) {
    crashlytics().crash();
  } else {
    crashlytics().recordError(error);
  }
};
```

### 2. Analytics Integration

**Performance Events**:
```javascript
// utils/Analytics.js
import analytics from '@react-native-firebase/analytics';

class PerformanceAnalytics {
  static trackScreenLoad(screenName, duration) {
    analytics().logEvent('screen_load_time', {
      screen_name: screenName,
      duration_ms: duration,
      platform: Platform.OS,
    });
  }

  static trackSlowOperation(operation, duration) {
    if (duration > 2000) { // Track operations slower than 2 seconds
      analytics().logEvent('slow_operation', {
        operation_name: operation,
        duration_ms: duration,
        platform: Platform.OS,
      });
    }
  }

  static trackMemoryWarning() {
    analytics().logEvent('memory_warning', {
      platform: Platform.OS,
      timestamp: Date.now(),
    });
  }
}
```

### 3. Memory Monitoring

**Memory Usage Tracking**:
```javascript
// utils/MemoryMonitor.js
import { AppState, DeviceEventEmitter } from 'react-native';

class MemoryMonitor {
  static startMonitoring() {
    if (__DEV__) {
      this.memoryTimer = setInterval(() => {
        if (global.gc) {
          const before = (performance as any).memory?.usedJSHeapSize;
          global.gc();
          const after = (performance as any).memory?.usedJSHeapSize;
          
          console.log(`Memory: ${Math.round((after || 0) / 1024 / 1024)}MB`);
          console.log(`Freed: ${Math.round((before - after) / 1024)}KB`);
        }
      }, 10000); // Check every 10 seconds
    }

    // Listen for memory warnings
    DeviceEventEmitter.addListener('memoryWarning', () => {
      console.warn('Memory warning received');
      PerformanceAnalytics.trackMemoryWarning();
    });
  }

  static stopMonitoring() {
    if (this.memoryTimer) {
      clearInterval(this.memoryTimer);
    }
  }
}
```

## Key Performance Metrics to Track

### 1. App Launch Time
**Target**: < 2.5 seconds from tap to interactive
**Measurement**: Time from app launch to first meaningful paint

### 2. Screen Transition Time
**Target**: < 300ms for navigation
**Measurement**: Time from navigation trigger to new screen render

### 3. List Scroll Performance
**Target**: Consistent 60fps scrolling
**Measurement**: Frame drops during scroll events

### 4. Memory Usage
**Target**: < 150MB typical usage, < 300MB peak
**Measurement**: RSS memory footprint

### 5. Bundle Size
**Target**: < 25MB total app size
**Measurement**: Built app size for app stores

### 6. API Response Handling
**Target**: < 200ms UI response to user actions
**Measurement**: Time from user action to UI update

## Performance Testing Workflow

### 1. Development Testing
```bash
# 1. Start monitoring tools
npx react-devtools &
# 2. Open Flipper
# 3. Enable performance monitor in app
# 4. Run performance tests
npm run test:performance
```

### 2. Manual Testing Checklist

**Screen Performance**:
- [ ] Screen loads in < 2.5 seconds
- [ ] Navigation animations are smooth (60fps)
- [ ] Lists scroll without frame drops
- [ ] Pull-to-refresh is responsive

**Memory Performance**:
- [ ] Memory usage stays under 200MB
- [ ] No memory leaks after navigation
- [ ] Background cleanup works properly

**Network Performance**:
- [ ] API calls complete in reasonable time
- [ ] Offline behavior works correctly
- [ ] Loading states are shown appropriately

### 3. Automated Performance Testing

**Jest Performance Tests**:
```javascript
// __tests__/performance.test.js
import { measurePerformance } from '../utils/testUtils';

describe('Component Performance', () => {
  it('should render UserList quickly', async () => {
    const renderTime = await measurePerformance(() => {
      render(<UserList users={mockUsers} />);
    });

    expect(renderTime).toBeLessThan(100); // 100ms threshold
  });

  it('should handle large datasets efficiently', async () => {
    const largeDataset = generateMockUsers(1000);
    const renderTime = await measurePerformance(() => {
      render(<UserList users={largeDataset} />);
    });

    expect(renderTime).toBeLessThan(500); // 500ms for large datasets
  });
});
```

## Common Performance Issues & Solutions

### 1. Slow List Rendering
**Problem**: FlatList with complex items renders slowly
**Solution**:
- Use `getItemLayout` for fixed-height items
- Implement `maxToRenderPerBatch` and `windowSize`
- Memoize render functions
- Use `removeClippedSubviews`

### 2. Excessive Re-renders
**Problem**: Components re-render unnecessarily
**Solution**:
- Use React.memo for functional components
- Implement proper dependency arrays in hooks
- Avoid creating objects/functions in render

### 3. Large Bundle Size
**Problem**: App size too large for app stores
**Solution**:
- Use dynamic imports for large libraries
- Enable Hermes engine
- Implement code splitting
- Optimize images and assets

### 4. Memory Leaks
**Problem**: Memory usage increases over time
**Solution**:
- Clean up listeners in useEffect cleanup
- Avoid circular references
- Properly handle async operations
- Clear timers and intervals

## Platform-Specific Monitoring

### iOS Specific
**Xcode Instruments**:
- Time Profiler: CPU usage analysis
- Allocations: Memory usage tracking
- Leaks: Memory leak detection
- Energy Log: Battery usage analysis

### Android Specific
**Android Studio Profiler**:
- CPU Profiler: Performance bottlenecks
- Memory Profiler: Heap analysis
- Network Profiler: API call monitoring
- Energy Profiler: Battery usage

## Production Monitoring Dashboard

**Key Metrics to Display**:
1. App crash rate (< 1% target)
2. Average app startup time
3. Memory usage distribution
4. Slow operation frequency
5. Screen load time percentiles
6. User engagement after performance events

**Alerting Thresholds**:
- Crash rate > 2%
- Startup time > 5 seconds for 90th percentile
- Memory usage > 400MB consistently
- Screen load time > 5 seconds

This comprehensive monitoring setup ensures you can identify, track, and resolve performance issues throughout the development lifecycle.