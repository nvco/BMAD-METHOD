# Mobile Performance Optimization

## ⚠️ CRITICAL EXECUTION NOTICE ⚠️

**THIS IS AN EXECUTABLE WORKFLOW - NOT REFERENCE MATERIAL**

When this task is invoked:

1. **DISABLE ALL EFFICIENCY OPTIMIZATIONS** - This workflow requires full user interaction
2. **MANDATORY STEP-BY-STEP EXECUTION** - Each optimization area must be processed sequentially with user feedback
3. **ELICITATION IS REQUIRED** - When `elicit: true`, you MUST use the 1-9 format and wait for user response
4. **NO SHORTCUTS ALLOWED** - Mobile performance optimization cannot be completed without following this workflow

**VIOLATION INDICATOR:** If you create a complete optimization plan without user interaction, you have violated this workflow.

## Critical: Mobile Performance Context Requirements

Before beginning optimization, establish mobile-specific performance context:

- **Target platforms**: iOS, Android performance characteristics and constraints
- **Device categories**: Entry-level, mid-range, flagship device performance targets
- **React Native setup**: Bundle configuration, native modules, performance tooling
- **User experience goals**: Startup time, responsiveness, battery life expectations
- **Performance baselines**: Current metrics and optimization targets

## CRITICAL: Mandatory Mobile Performance Optimization Format

**When analyzing each performance area, this is a HARD STOP requiring user interaction:**

**YOU MUST:**

1. Present performance area analysis with mobile-specific measurements and bottlenecks
2. Provide detailed optimization recommendations (React Native techniques, platform optimizations)
3. **STOP and present numbered options 1-9:**
   - **Option 1:** Always "Proceed to next performance area"
   - **Options 2-9:** Select 8 methods from mobile performance optimization techniques:
     - React Native bundle size and code splitting analysis
     - JavaScript thread performance and bridge optimization
     - Native UI rendering and animation performance tuning
     - Memory management and garbage collection optimization
     - Network performance and caching strategy improvement
     - Battery usage and power consumption optimization
     - Cross-platform performance consistency validation
     - Performance monitoring and alerting setup
   - End with: "Select 1-9 or just type your question/feedback:"
4. **WAIT FOR USER RESPONSE** - Do not proceed until user selects option or provides feedback

**WORKFLOW VIOLATION:** Analyzing performance areas without user interaction violates this task.

**NEVER proceed to the next area without user selection.**

## Mobile Performance Optimization Framework

### Phase 1: Performance Baseline Assessment

1. **Establish current performance metrics**:
   - **Startup Performance**: Time to first render, time to interactive
   - **Runtime Performance**: Frame rate, animation smoothness, responsiveness
   - **Memory Usage**: RAM consumption, memory leaks, garbage collection
   - **Network Performance**: API response times, data usage, offline capability
   - **Battery Consumption**: Power usage patterns and optimization opportunities
   - **Bundle Size**: JavaScript bundle size and loading performance

### Phase 2: Performance Analysis and Optimization (Interactive)

For each performance optimization area:

1. **Present performance area analysis:**
   - Current performance metrics and bottlenecks
   - Platform-specific performance characteristics (iOS vs Android)
   - React Native optimization opportunities and constraints
   - User experience impact and business implications
   - Implementation complexity and resource requirements

2. **Assess optimization strategies:**
   - **Code-Level Optimizations**: Component rendering, state management efficiency
   - **Architecture Optimizations**: Bundle splitting, lazy loading, caching strategies
   - **Platform Optimizations**: Native module performance, bridge communication
   - **Resource Optimizations**: Image compression, asset management, network usage
   - **Monitoring Integration**: Performance tracking and alerting setup

3. **MANDATORY USER INTERACTION** (use 1-9 format above)

4. **Document optimization plan** with implementation priorities and expected impact

### Phase 3: Cross-Platform Performance Validation

Ensure optimization strategy addresses both platforms:

```
MOBILE PERFORMANCE OPTIMIZATION MATRIX

Performance Area          iOS    Android    React Native
Startup Time              ✅       ✅          ✅
JavaScript Execution      ✅       ✅          ✅
UI Rendering              ✅       ✅          ✅
Memory Management         ✅       ✅          ✅
Network Performance       ✅       ✅          ✅
Battery Optimization      ✅       ✅          ✅
Bundle Size               ✅       ✅          ✅
```

### Phase 4: Mobile Performance Implementation Strategy

1. **Optimization priority matrix:**
   - High impact, low effort optimizations (quick wins)
   - High impact, high effort optimizations (strategic investments)
   - Low impact optimizations (nice-to-have improvements)
   - Platform-specific optimizations vs cross-platform benefits

2. **Implementation approach:**
   - Incremental optimization with performance measurement
   - A/B testing for performance improvements
   - Rollback procedures for optimization regressions
   - Continuous monitoring and performance alerting

## Mobile Performance Optimization Areas

### 1. Startup Performance Optimization
**Targets**: < 2s time to first render, < 3s time to interactive
- **Bundle Optimization**: Code splitting, lazy loading, tree shaking
- **Asset Optimization**: Image compression, font optimization, splash screen efficiency
- **Initialization Optimization**: Reduce startup work, defer non-critical initialization
- **Platform-Specific**: iOS launch screens, Android cold start optimization

### 2. Runtime Performance Optimization
**Targets**: 60 FPS animations, < 16ms frame budget
- **React Optimization**: Component memoization, render optimization, hook efficiency
- **List Performance**: VirtualizedList optimization, FlatList configuration
- **Animation Performance**: Native driver usage, layout animation optimization
- **Bridge Optimization**: Reduce native bridge calls, batch updates

### 3. Memory Management Optimization
**Targets**: Stable memory usage, no memory leaks
- **Component Lifecycle**: Proper cleanup, listener removal, subscription management
- **Image Management**: Image caching, memory-efficient loading, cleanup
- **State Management**: Efficient state structure, memory-conscious data handling
- **Garbage Collection**: Minimize object creation, optimize memory allocation patterns

### 4. Network Performance Optimization
**Targets**: Fast API responses, efficient data usage
- **API Optimization**: Request batching, response caching, compression
- **Offline Strategy**: Data persistence, sync strategies, network error handling
- **Image Loading**: Progressive loading, caching strategies, optimization
- **Background Sync**: Efficient background data synchronization

### 5. Battery Optimization
**Targets**: Minimal battery drain, efficient power usage
- **Background Processing**: Minimize background work, efficient task scheduling
- **Network Efficiency**: Reduce unnecessary network calls, optimize data transfer
- **CPU Usage**: Optimize algorithms, reduce computational overhead
- **Screen and GPU**: Efficient rendering, minimize overdraw, optimize animations

### 6. Bundle Size Optimization
**Targets**: Fast download, efficient storage
- **Code Splitting**: Dynamic imports, lazy loading of components
- **Tree Shaking**: Remove unused code, optimize imports
- **Asset Optimization**: Compress images, optimize fonts, remove unused assets
- **Dependency Optimization**: Analyze and optimize third-party library usage

## Mobile Performance Tools and Techniques

### React Native Performance Tools
- **Flipper**: Real-time performance monitoring and profiling
- **React DevTools**: Component rendering and update analysis
- **Metro Bundle Analyzer**: Bundle size analysis and optimization
- **Native Performance Tools**: Xcode Instruments, Android Profiler

### Performance Monitoring Integration
```javascript
// Performance monitoring setup
import {Performance} from 'react-native-performance';

// Startup performance tracking
Performance.mark('app-start');
Performance.mark('first-render');
Performance.measure('startup-time', 'app-start', 'first-render');

// Component performance tracking
const OptimizedComponent = React.memo(({data}) => {
  Performance.mark('component-start');
  
  useEffect(() => {
    Performance.mark('component-rendered');
    Performance.measure('component-time', 'component-start', 'component-rendered');
  });
  
  return <ComponentUI data={data} />;
});
```

### Cross-Platform Optimization Strategies
- **Shared Optimizations**: React Native performance improvements benefiting both platforms
- **Platform-Specific**: iOS and Android targeted optimizations
- **Progressive Enhancement**: Optimize for lowest common denominator, enhance for capable devices
- **Performance Budgets**: Set and monitor platform-specific performance targets

## Performance Optimization Implementation

### Code-Level Optimizations
```javascript
// Component optimization examples
const OptimizedList = React.memo(({items}) => {
  const renderItem = useCallback(({item}) => (
    <MemoizedListItem key={item.id} item={item} />
  ), []);
  
  return (
    <FlatList
      data={items}
      renderItem={renderItem}
      getItemLayout={(data, index) => ({
        length: ITEM_HEIGHT,
        offset: ITEM_HEIGHT * index,
        index,
      })}
      removeClippedSubviews={true}
      maxToRenderPerBatch={10}
      windowSize={10}
    />
  );
});
```

### Bundle Optimization Configuration
```javascript
// Metro configuration for optimization
module.exports = {
  resolver: {
    alias: {
      'react-native-vector-icons': 'react-native-vector-icons/dist',
    },
  },
  transformer: {
    minifierConfig: {
      keep_fnames: true,
      mangle: {
        keep_fnames: true,
      },
    },
  },
};
```

## Output Requirements

**MANDATORY DELIVERABLES:**

1. **Performance Optimization Plan** with prioritized improvement areas
2. **Implementation Roadmap** with timeline and resource requirements
3. **Performance Monitoring Setup** with metrics and alerting configuration
4. **Cross-Platform Optimization Strategy** covering iOS and Android
5. **Performance Testing Framework** with automated performance validation
6. **Optimization Impact Assessment** with expected performance improvements

## Performance Optimization Success Criteria

✅ **Optimization Complete When:**
- All major performance bottlenecks identified and addressed
- Performance targets achieved for startup, runtime, and battery usage
- Cross-platform performance consistency validated
- Performance monitoring and alerting operational
- Team equipped with performance optimization knowledge and tools

## Integration Notes

- **Works with mobile-architect** for architectural performance optimization
- **Supports mobile-dev** with performance-optimized code implementation
- **Aligns with mobile-qa** for performance testing and validation
- **Guides mobile-po** for performance acceptance criteria and quality gates
- **Coordinates with mobile-orchestrator** for performance optimization workflow management