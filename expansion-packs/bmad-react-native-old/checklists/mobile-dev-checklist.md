# Mobile Development Checklist

## Pre-Development Setup

### Environment Verification
- [ ] Node.js 20+ installed and verified
- [ ] React Native CLI or Expo CLI installed
- [ ] Xcode latest version installed (if targeting iOS)
- [ ] Android Studio installed (if targeting Android)
- [ ] iOS Simulator functional (if targeting iOS)
- [ ] Android Emulator functional (if targeting Android)
- [ ] Flipper debugger installed and configured
- [ ] VS Code/Cursor with React Native extensions
- [ ] Git repository initialized with .gitignore

### Project Initialization
- [ ] React Native project created with TypeScript
- [ ] Required dependencies installed (navigation, state management, etc.)
- [ ] Metro bundler configuration reviewed
- [ ] ESLint and Prettier configured
- [ ] Pre-commit hooks setup (husky, lint-staged)
- [ ] iOS project opening successfully in Xcode (if targeting iOS)
- [ ] Android project building successfully (if targeting Android)

### Story Context Review
- [ ] User story requirements fully understood
- [ ] Acceptance criteria reviewed and clarified
- [ ] Technical specifications from mobile-architect available
- [ ] UX specifications from mobile-ux available
- [ ] Dependencies and blockers identified
- [ ] Performance requirements noted

## Implementation Phase

### Component Development
- [ ] TypeScript interfaces/types defined
- [ ] Functional component structure created
- [ ] Props interface properly typed
- [ ] Default props defined where appropriate
- [ ] Component memoization applied if beneficial (React.memo, useMemo, useCallback)
- [ ] Error boundaries implemented for complex components

### UI Implementation
- [ ] Layout implemented with Flexbox
- [ ] SafeAreaView properly utilized for iOS (if targeting iOS)
- [ ] Status bar handling implemented for Android (if targeting Android)
- [ ] Platform-specific styles applied (.ios.tsx/.android.tsx if needed)
- [ ] Responsive design for different screen sizes
- [ ] Dark mode support implemented (if required)
- [ ] Accessibility props added (accessibilityLabel, accessibilityRole, etc.)

### State Management
- [ ] Local state with useState/useReducer implemented correctly
- [ ] Global state integration (Context/Redux/Zustand) if needed
- [ ] State updates optimized to prevent unnecessary re-renders
- [ ] Async state handling with proper loading/error states
- [ ] State persistence implemented if required

### Navigation Implementation
- [ ] Screen navigation configured
- [ ] Navigation parameters properly typed
- [ ] Navigation options set (header, tabs, etc.)
- [ ] Deep linking integration if required
- [ ] Navigation state persistence if needed
- [ ] Back button behavior verified

### API Integration
- [ ] API service functions created with proper typing
- [ ] Error handling implemented with user-friendly messages
- [ ] Loading states managed appropriately
- [ ] Retry logic implemented where appropriate
- [ ] Offline handling with cached data
- [ ] Network request optimization (avoid redundant calls)

### Performance Optimization
- [ ] FlatList/VirtualizedList used for large datasets
- [ ] Image optimization and caching implemented
- [ ] Lazy loading for heavy components
- [ ] Bundle analyzer run to check size
- [ ] Memory leaks checked with profiler
- [ ] Render cycles optimized (avoid inline functions/objects)

## Platform-Specific Implementation

### iOS Implementation (if targeting iOS)

#### iOS Platform Integration
- [ ] iOS-specific components used where appropriate
- [ ] Native module integration if required
- [ ] iOS permissions requested properly
- [ ] Push notifications setup with APNs
- [ ] Deep linking/universal links configured
- [ ] iOS app lifecycle events handled

#### iOS Visual Compliance
- [ ] iOS Human Interface Guidelines followed
- [ ] Status bar style configured appropriately
- [ ] Navigation bar style matches iOS conventions
- [ ] Touch targets meet minimum size requirements (44x44 points)
- [ ] Haptic feedback implemented where appropriate
- [ ] iOS-specific animations and transitions

#### iOS Device Compatibility
- [ ] iPhone compatibility verified (multiple sizes)
- [ ] iPad compatibility if required
- [ ] Notch/Dynamic Island handling verified
- [ ] Safe area insets properly handled
- [ ] Landscape orientation support if needed
- [ ] iOS version compatibility tested

### Android Implementation (if targeting Android)

#### Android Platform Integration
- [ ] Android-specific components used where appropriate
- [ ] Native module integration if required (Kotlin/Java)
- [ ] Android permissions requested properly (runtime permissions)
- [ ] Push notifications setup with FCM
- [ ] Deep linking/app links configured
- [ ] Android app lifecycle events handled
- [ ] Back button behavior implemented properly

#### Android Visual Compliance
- [ ] Material Design guidelines followed
- [ ] Status bar and navigation bar handling (edge-to-edge)
- [ ] Touch targets meet minimum size requirements (48x48dp)
- [ ] Material Design animations and transitions
- [ ] Proper elevation and shadows for depth
- [ ] Android-specific UI patterns (FAB, Snackbar, etc.)

#### Android Device Compatibility
- [ ] Multiple Android device sizes tested
- [ ] Different Android versions compatibility verified
- [ ] Tablet layout considerations if applicable
- [ ] Different screen densities handled properly
- [ ] Landscape orientation support if needed
- [ ] Hardware back button behavior verified

## Testing Implementation

### Unit Testing
- [ ] Jest test files created for components
- [ ] React Native Testing Library used for component testing
- [ ] Custom hooks tested independently
- [ ] Utility functions have unit tests
- [ ] Mock implementations for native modules
- [ ] Test coverage meets project standards (>80%)

### Integration Testing
- [ ] Screen-level integration tests written
- [ ] Navigation flow testing implemented
- [ ] API integration tests with mocked responses
- [ ] State management integration tested
- [ ] User workflow testing completed

### Manual Testing
- [ ] Feature tested on iOS Simulator (if targeting iOS)
- [ ] Feature tested on Android Emulator (if targeting Android)
- [ ] Multiple device sizes tested on target platforms
- [ ] Both light and dark mode tested (if supported)
- [ ] Platform-specific features verified
- [ ] Cross-platform consistency checked (if targeting both platforms)
- [ ] Accessibility testing with VoiceOver (iOS) and TalkBack (Android)
- [ ] Performance tested with slow animations
- [ ] Edge cases and error scenarios verified

## Code Quality

### Code Standards
- [ ] TypeScript strict mode compliance
- [ ] ESLint rules passing without warnings
- [ ] Prettier formatting applied
- [ ] No console.log statements in production code
- [ ] Proper error handling and logging implemented
- [ ] Code comments added for complex logic

### Documentation
- [ ] Component props documented with JSDoc
- [ ] Complex algorithms/logic commented
- [ ] Setup instructions updated if new dependencies added
- [ ] Known issues or limitations documented
- [ ] Performance considerations noted

### Security
- [ ] No sensitive data in code or logs
- [ ] Input validation implemented
- [ ] Secure storage used for sensitive data (Keychain)
- [ ] API keys and secrets properly managed
- [ ] Deep link validation implemented

## Performance Validation

### Metrics Verification
- [ ] App startup time under target (< 3 seconds)
- [ ] 60fps maintained during animations and scrolling
- [ ] Memory usage within acceptable limits
- [ ] Bundle size meets targets
- [ ] Network requests optimized and minimal
- [ ] CPU usage reasonable during peak operations

### iOS Performance
- [ ] Main thread not blocked by heavy operations
- [ ] Background tasks properly managed
- [ ] Image loading doesn't cause memory spikes
- [ ] Smooth scrolling in lists and scroll views
- [ ] Quick app resume from background
- [ ] Battery usage reasonable

## Debugging and Troubleshooting

### Development Tools
- [ ] Flipper debugging sessions clean (no errors)
- [ ] React DevTools profiling shows no performance issues
- [ ] Metro bundler logs clean
- [ ] Xcode console shows no warnings/errors
- [ ] iOS Simulator performance acceptable
- [ ] Hot reloading working properly

### Error Handling
- [ ] Graceful error handling for all user interactions
- [ ] Appropriate error messages shown to users
- [ ] Error boundary catches and displays fallback UI
- [ ] Network errors handled with retry options
- [ ] Crash reporting integrated (if required)

## Pre-Submission Checklist

### Code Review Preparation
- [ ] Self-review completed - code reads cleanly
- [ ] All TODO comments resolved or tracked
- [ ] Dead code removed
- [ ] Commented-out code removed
- [ ] Proper git commit messages
- [ ] Feature branch up to date with main

### Story Completion
- [ ] All acceptance criteria met and tested
- [ ] Definition of done checklist completed
- [ ] Performance requirements verified
- [ ] No known bugs or issues
- [ ] Documentation updated as needed
- [ ] Ready for QA review

### Handoff Documentation
- [ ] Implementation notes documented for complex features
- [ ] Any deviations from original design explained
- [ ] Setup steps for testing documented
- [ ] Known limitations or future improvements noted
- [ ] Dependencies or configuration changes documented

---

**Completion Criteria**: All checklist items must be completed before marking story as "Ready for Review". Any exceptions must be documented and approved by the team.