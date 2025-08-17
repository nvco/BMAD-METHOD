# Mobile Performance Monitoring Setup

## Performance Monitoring Strategy

### Key Performance Indicators (KPIs)
- **App Launch Time**: Cold start < 3s, warm start < 1s
- **Screen Transition Time**: < 300ms for smooth UX
- **Memory Usage**: < 200MB for typical operations
- **CPU Usage**: < 30% during normal operation
- **Network Performance**: API response times < 2s
- **Crash Rate**: < 0.1% of sessions
- **ANR Rate**: < 0.01% (Android Application Not Responding)

## Firebase Performance Monitoring

### Setup and Configuration
```javascript
// Install Firebase Performance
npm install @react-native-firebase/perf

// iOS configuration (Podfile)
pod 'Firebase/Performance'

// Android configuration (build.gradle)
implementation 'com.google.firebase:firebase-perf'

// Initialize in index.js
import perf from '@react-native-firebase/perf';

// Auto-collection enabled by default
```

### Custom Performance Traces
```javascript
import perf from '@react-native-firebase/perf';

// Screen loading performance
const ScreenWithPerformanceTracking = () => {
  useEffect(() => {
    let trace;
    
    const startPerformanceTrace = async () => {
      trace = await perf().startTrace('user_profile_screen_load');
      trace.putAttribute('user_type', 'premium');
      trace.putMetric('initial_data_size', userData.length);
    };
    
    const stopPerformanceTrace = async () => {
      if (trace) {
        await trace.stop();
      }
    };
    
    startPerformanceTrace();
    
    // Stop trace when screen is fully loaded
    return () => {
      stopPerformanceTrace();
    };
  }, []);
};

// API call performance
const apiCallWithPerformance = async (endpoint) => {
  const trace = await perf().startTrace(`api_call_${endpoint}`);
  
  try {
    const response = await fetch(`/api/${endpoint}`);
    trace.putAttribute('status_code', response.status.toString());
    return await response.json();
  } catch (error) {
    trace.putAttribute('error', error.message);
    throw error;
  } finally {
    await trace.stop();
  }
};
```

### Network Request Monitoring
```javascript
// HTTP metrics are automatically collected
// Configure URL patterns to monitor
import perf from '@react-native-firebase/perf';

// Custom network monitoring
const NetworkMonitoredFetch = async (url, options) => {
  const httpMetric = perf().newHttpMetric(url, 'GET');
  
  try {
    await httpMetric.start();
    
    const response = await fetch(url, options);
    
    httpMetric.setHttpResponseCode(response.status);
    httpMetric.setResponseContentType(response.headers.get('Content-Type'));
    httpMetric.setResponsePayloadSize(
      parseInt(response.headers.get('Content-Length') || '0')
    );
    
    return response;
  } finally {
    await httpMetric.stop();
  }
};
```

## React Native Performance Monitor

### Built-in Performance Monitor
```javascript
// Enable in development
if (__DEV__) {
  require('react-native').unstable_enableLogBox();
  
  // Show performance overlay
  import { unstable_trace as trace } from 'scheduler/tracing';
  
  const performanceWrapper = (name, fn) => {
    return trace(name, performance.now(), fn);
  };
}

// Monitor component render performance
import { Profiler } from 'react';

const ProfiledComponent = ({ children }) => {
  const onRender = (id, phase, actualDuration, baseDuration) => {
    console.log('Performance Profile:', {
      id,
      phase,
      actualDuration,
      baseDuration,
    });
    
    // Send to analytics if duration is concerning
    if (actualDuration > 100) {
      analytics.track('slow_render', {
        component: id,
        duration: actualDuration,
      });
    }
  };
  
  return (
    <Profiler id="ExpensiveComponent" onRender={onRender}>
      {children}
    </Profiler>
  );
};
```

## Memory Monitoring

### Memory Leak Detection
```javascript
import { Platform } from 'react-native';

const MemoryMonitor = () => {
  useEffect(() => {
    let memoryCheckInterval;
    
    if (__DEV__) {
      memoryCheckInterval = setInterval(() => {
        if (Platform.OS === 'ios') {
          // iOS memory monitoring
          const memoryInfo = performance.memory;
          if (memoryInfo) {
            console.log('Memory Usage:', {
              used: memoryInfo.usedJSHeapSize,
              total: memoryInfo.totalJSHeapSize,
              limit: memoryInfo.jsHeapSizeLimit,
            });
          }
        } else {
          // Android memory monitoring
          console.log('Memory check - Android native monitoring required');
        }
      }, 10000); // Check every 10 seconds
    }
    
    return () => {
      if (memoryCheckInterval) {
        clearInterval(memoryCheckInterval);
      }
    };
  }, []);
};

// Component memory cleanup checker
const useMemoryCleanupChecker = (componentName) => {
  useEffect(() => {
    console.log(`${componentName} mounted`);
    
    return () => {
      console.log(`${componentName} unmounted - check for memory leaks`);
    };
  }, [componentName]);
};
```

### Image Memory Management
```javascript
import FastImage from 'react-native-fast-image';

// Preload important images
const preloadImages = (imageUrls) => {
  FastImage.preload(
    imageUrls.map(url => ({
      uri: url,
      priority: FastImage.priority.high,
    }))
  );
};

// Clear image cache periodically
const clearImageCache = () => {
  FastImage.clearMemoryCache();
  FastImage.clearDiskCache();
};

// Monitor image loading performance
const ImageWithPerformanceTracking = ({ uri, ...props }) => {
  const [loadTime, setLoadTime] = useState(null);
  const startTime = useRef(performance.now());
  
  const onLoad = () => {
    const endTime = performance.now();
    const duration = endTime - startTime.current;
    setLoadTime(duration);
    
    if (duration > 1000) {
      console.warn(`Slow image load: ${uri} took ${duration}ms`);
    }
  };
  
  return (
    <FastImage
      {...props}
      source={{ uri }}
      onLoad={onLoad}
    />
  );
};
```

## Battery and CPU Monitoring

### CPU Usage Monitoring
```javascript
// Monitor expensive operations
const useCPUMonitoring = (operationName) => {
  const monitorCPUIntensiveOperation = useCallback(async (operation) => {
    const startTime = performance.now();
    const startCPU = process.cpuUsage?.();
    
    try {
      const result = await operation();
      
      const endTime = performance.now();
      const endCPU = process.cpuUsage?.(startCPU);
      
      const metrics = {
        duration: endTime - startTime,
        cpuUser: endCPU?.user,
        cpuSystem: endCPU?.system,
      };
      
      // Log if operation is CPU intensive
      if (metrics.duration > 100) {
        console.warn(`CPU intensive operation: ${operationName}`, metrics);
        
        // Send to analytics
        analytics.track('cpu_intensive_operation', {
          operation: operationName,
          ...metrics,
        });
      }
      
      return result;
    } catch (error) {
      console.error(`Operation failed: ${operationName}`, error);
      throw error;
    }
  }, [operationName]);
  
  return monitorCPUIntensiveOperation;
};
```

### Battery Usage Awareness
```javascript
import { Platform } from 'react-native';

// Optimize for battery usage
const useBatteryOptimization = () => {
  const [isLowPowerMode, setIsLowPowerMode] = useState(false);
  
  useEffect(() => {
    if (Platform.OS === 'ios') {
      // Check low power mode on iOS
      // This would require native module implementation
      // or use react-native-device-info
    }
  }, []);
  
  // Reduce frequency of operations in low power mode
  const getOptimalUpdateInterval = useCallback(() => {
    return isLowPowerMode ? 30000 : 10000; // 30s vs 10s
  }, [isLowPowerMode]);
  
  // Reduce animation quality
  const getOptimalAnimationConfig = useCallback(() => {
    return isLowPowerMode 
      ? { duration: 150, useNativeDriver: true }
      : { duration: 300, useNativeDriver: true };
  }, [isLowPowerMode]);
  
  return {
    isLowPowerMode,
    getOptimalUpdateInterval,
    getOptimalAnimationConfig,
  };
};
```

## Third-Party Performance Tools

### New Relic Mobile
```javascript
// Install New Relic
npm install @newrelic/react-native-agent

// Initialize in index.js
import NewRelic from '@newrelic/react-native-agent';

NewRelic.startAgent('YOUR_APP_TOKEN');

// Custom events and attributes
NewRelic.recordCustomEvent('UserAction', {
  action: 'button_press',
  screen: 'home',
  user_type: 'premium',
});

// Track custom metrics
NewRelic.recordMetric('Custom/API/ResponseTime', responseTime);

// Set user attributes
NewRelic.setUserId('user123');
NewRelic.setAttribute('userType', 'premium');
```

### Datadog Real User Monitoring
```javascript
// Install Datadog
npm install @datadog/mobile-react-native

// Initialize
import { DdSdkReactNative } from '@datadog/mobile-react-native';

DdSdkReactNative.initialize({
  clientToken: 'YOUR_CLIENT_TOKEN',
  env: 'production',
  applicationId: 'YOUR_APP_ID',
  nativeCrashReportEnabled: true,
  nativeInteractionTracking: true,
});

// Track custom events
DdSdkReactNative.addAction('user_interaction', {
  type: 'tap',
  target: 'login_button',
});

// Track errors
DdSdkReactNative.addError('Custom error message', {
  source: 'custom',
  stack: error.stack,
});
```

## Performance Testing Automation

### Automated Performance Tests
```javascript
// Jest performance tests
describe('Performance Tests', () => {
  it('should render UserList within performance threshold', async () => {
    const startTime = performance.now();
    
    const { getByTestId } = render(
      <UserList users={generateMockUsers(1000)} />
    );
    
    await waitFor(() => {
      expect(getByTestId('user-list')).toBeTruthy();
    });
    
    const endTime = performance.now();
    const renderTime = endTime - startTime;
    
    expect(renderTime).toBeLessThan(1000); // Should render in under 1 second
  });
  
  it('should handle memory efficiently with large datasets', () => {
    const initialMemory = performance.memory?.usedJSHeapSize;
    
    // Render component with large dataset
    const { unmount } = render(
      <LargeDataComponent data={generateLargeDataset()} />
    );
    
    // Unmount component
    unmount();
    
    // Force garbage collection (in test environment)
    if (global.gc) {
      global.gc();
    }
    
    setTimeout(() => {
      const finalMemory = performance.memory?.usedJSHeapSize;
      const memoryDifference = finalMemory - initialMemory;
      
      // Memory should not increase significantly after unmount
      expect(memoryDifference).toBeLessThan(10 * 1024 * 1024); // 10MB threshold
    }, 1000);
  });
});
```

### Continuous Performance Monitoring
```yaml
# GitHub Actions performance monitoring
name: Performance Monitoring
on: [push, pull_request]

jobs:
  performance:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install dependencies
        run: npm ci
      
      - name: Run performance tests
        run: npm run test:performance
      
      - name: Bundle size analysis
        run: |
          npm run build:analyze
          npx bundlesize
      
      - name: Comment performance results
        uses: actions/github-script@v6
        with:
          script: |
            // Post performance metrics to PR
            const fs = require('fs');
            const results = JSON.parse(fs.readFileSync('performance-results.json'));
            
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: `📊 Performance Report:
              - Bundle size: ${results.bundleSize}
              - Render time: ${results.renderTime}ms
              - Memory usage: ${results.memoryUsage}MB`
            });
```

## Performance Alerting

### Performance Thresholds
```javascript
const PERFORMANCE_THRESHOLDS = {
  APP_LAUNCH_TIME: 3000, // 3 seconds
  SCREEN_TRANSITION: 300, // 300ms
  API_RESPONSE: 2000, // 2 seconds
  MEMORY_USAGE: 200 * 1024 * 1024, // 200MB
  CRASH_RATE: 0.001, // 0.1%
  ANR_RATE: 0.0001, // 0.01%
};

// Alert system
const sendPerformanceAlert = (metric, value, threshold) => {
  if (value > threshold) {
    // Send to monitoring service
    console.error(`Performance alert: ${metric} exceeded threshold`, {
      metric,
      value,
      threshold,
      timestamp: new Date().toISOString(),
    });
    
    // Send to crash reporting
    crashlytics().log(`Performance degradation: ${metric}`);
    crashlytics().recordError(
      new Error(`Performance threshold exceeded: ${metric}`)
    );
  }
};
```

## Device-Specific Optimization

### Adaptive Performance Based on Device
```javascript
import DeviceInfo from 'react-native-device-info';

const useDeviceOptimization = () => {
  const [deviceCapabilities, setDeviceCapabilities] = useState({
    isLowEndDevice: false,
    totalMemory: 0,
    cpuCount: 0,
  });
  
  useEffect(() => {
    const getDeviceCapabilities = async () => {
      const totalMemory = await DeviceInfo.getTotalMemory();
      const cpuCount = await DeviceInfo.getPhysicalCpuCount();
      
      // Consider devices with < 2GB RAM as low-end
      const isLowEndDevice = totalMemory < 2 * 1024 * 1024 * 1024;
      
      setDeviceCapabilities({
        isLowEndDevice,
        totalMemory,
        cpuCount,
      });
    };
    
    getDeviceCapabilities();
  }, []);
  
  // Adaptive configuration based on device
  const getOptimalConfiguration = useCallback(() => {
    return {
      maxCacheSize: deviceCapabilities.isLowEndDevice ? 50 * 1024 * 1024 : 200 * 1024 * 1024,
      imageQuality: deviceCapabilities.isLowEndDevice ? 0.7 : 0.9,
      animationDuration: deviceCapabilities.isLowEndDevice ? 150 : 300,
      maxConcurrentRequests: deviceCapabilities.cpuCount < 4 ? 2 : 4,
    };
  }, [deviceCapabilities]);
  
  return {
    deviceCapabilities,
    getOptimalConfiguration,
  };
};
```

This comprehensive performance monitoring setup provides real-time insights into app performance, automated testing, and adaptive optimization based on device capabilities.