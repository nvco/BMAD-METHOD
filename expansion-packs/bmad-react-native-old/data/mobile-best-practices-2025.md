# React Native Mobile Development Best Practices 2025

## Platform Version Support Strategy

### iOS Version Support (Current Recommendations)
- **Minimum iOS**: 13.0 (covers 95%+ of active devices)
- **Target iOS**: 17.0+ (latest stable)
- **Recommended Strategy**: Support current version + 3 previous major versions
- **Update Frequency**: Drop oldest version annually after new iOS release

**Decision Framework for iOS Support**:
- Consumer apps: iOS 14.0+ (broader reach)
- Enterprise apps: iOS 15.0+ (better security)
- New projects: iOS 13.0+ (React Native minimum)

### Android Version Support (Current Recommendations)
- **Minimum API Level**: 21 (Android 5.0 - covers 99%+ of active devices)
- **Target API Level**: 34 (Android 14)
- **Compile SDK**: 34 (latest stable)
- **Recommended Strategy**: Min API 21, Target latest stable

**Decision Framework for Android Support**:
- Global apps: API 21+ (maximum reach)
- Modern feature apps: API 23+ (runtime permissions)
- Enterprise apps: API 26+ (better security)

## React Native Version Strategy

### Current Stable Versions (2025)
- **Latest Stable**: 0.75.x
- **Recommended for New Projects**: 0.74.x (proven stable)
- **Minimum Supported**: 0.70.0 (for this expansion pack)
- **LTS Strategy**: Use stable version that's 1-2 releases behind latest

### Version Selection Criteria
- **New Projects**: Use latest stable (0.74.x)
- **Existing Projects**: Upgrade every 2-3 minor versions
- **Enterprise**: Use version with 6+ months stability track record
- **Bleeding Edge**: Only for research/experimentation

## Technology Stack Recommendations

### State Management Selection Guide
**Project Complexity-Based Recommendations**:

**Simple Apps (< 10 screens)**:
- **Recommended**: React Context + useReducer
- **Why**: Built-in, no external dependencies
- **When**: Local state, simple data flow

**Medium Apps (10-30 screens)**:
- **Recommended**: Zustand
- **Alternative**: Redux Toolkit
- **Why**: Minimal boilerplate, TypeScript-friendly
- **When**: Complex state, multiple data sources

**Large Apps (30+ screens)**:
- **Recommended**: Redux Toolkit + RTK Query
- **Alternative**: Zustand + React Query
- **Why**: Mature ecosystem, predictable patterns
- **When**: Team > 5 developers, complex business logic

### UI Library Recommendations
**By App Type**:

**Material Design Focus**:
- **Primary**: React Native Paper 5.x
- **Secondary**: NativeBase 3.x
- **When**: Android-first or cross-platform consistency

**Custom Design Systems**:
- **Primary**: Styled Components + React Native
- **Secondary**: Emotion + React Native
- **When**: Unique branding, design system exists

**Rapid Prototyping**:
- **Primary**: React Native Elements
- **Secondary**: UI Kitten
- **When**: Quick MVP, standard patterns

### Navigation Strategy
**Recommended**: React Navigation 6.x
- **Stack Navigator**: Hierarchical navigation
- **Tab Navigator**: 2-5 top-level sections
- **Drawer Navigator**: 5+ sections or secondary nav
- **Modal**: Contextual tasks, forms

**Alternative**: React Native Navigation (Wix)
- **When**: Performance critical, complex animations
- **Trade-off**: More complex setup, native performance

## Performance Targets & Benchmarks

### App Performance Targets
**Startup Time**:
- **Excellent**: < 1.5 seconds to interactive
- **Good**: < 2.5 seconds to interactive
- **Acceptable**: < 4 seconds to interactive

**Frame Rate**:
- **Target**: 60fps consistently
- **Minimum**: 45fps during animations
- **Method**: Monitor with Flipper/React DevTools

**Memory Usage**:
- **Target**: < 150MB RAM for typical usage
- **Maximum**: < 300MB RAM peak usage
- **Method**: Profile with Xcode Instruments/Android Studio

**Bundle Size**:
- **Target**: < 25MB total app size
- **Android**: Use App Bundle for dynamic delivery
- **iOS**: Use App Thinning for device-specific bundles

### Performance Optimization Priorities
1. **JavaScript Bundle Size**: Code splitting, tree shaking
2. **Image Optimization**: WebP, proper sizing, caching
3. **List Performance**: FlatList optimization, lazy loading
4. **Navigation**: Lazy screen loading, proper transitions
5. **Memory Management**: Proper cleanup, avoid leaks

## Device Support Matrix

### iOS Device Support
**Recommended Support Levels**:
- **iPhone**: 8 and newer (iOS 13+ compatible)
- **iPad**: 6th generation and newer
- **Screen Sizes**: 4.7" to 6.9" (iPhone), 10.2" to 12.9" (iPad)
- **Safe Area**: Handle all notch/Dynamic Island configurations

**Testing Priority Devices**:
1. iPhone 13/14/15 (current mainstream)
2. iPhone SE 3rd gen (smallest screen)
3. iPhone 15 Pro Max (largest screen)
4. iPad Air/Pro (tablet experience)

### Android Device Support
**Recommended Support Levels**:
- **Screen Densities**: mdpi, hdpi, xhdpi, xxhdpi, xxxhdpi
- **Screen Sizes**: 4.0" to 7.0" (phones), 7.0"+ (tablets)
- **RAM**: 2GB minimum, optimize for 4GB+
- **Manufacturers**: Samsung, Google, OnePlus, Xiaomi

**Testing Priority Devices**:
1. Google Pixel (latest 2 generations)
2. Samsung Galaxy S series (latest 2 generations)
3. Low-end device (2-3GB RAM)
4. Tablet (Samsung Tab or similar)

## Testing Strategy Recommendations

### Testing Pyramid for Mobile
**Unit Tests (70%)**:
- Business logic functions
- Custom hooks
- Utility functions
- **Framework**: Jest

**Integration Tests (20%)**:
- Component behavior
- API integration
- Navigation flows
- **Framework**: React Native Testing Library

**E2E Tests (10%)**:
- Critical user journeys
- Platform-specific flows
- **Framework**: Detox (recommended) or Maestro

### Device Testing Strategy
**Simulator/Emulator Testing (Development)**:
- Rapid iteration
- Multiple OS versions
- Different screen sizes
- **Limitations**: Performance, hardware features

**Real Device Testing (Pre-release)**:
- Performance validation
- Hardware feature testing
- Network condition testing
- **Required**: Before every release

## CI/CD Best Practices

### Build Pipeline Recommendations
**For Small Teams**:
- **Platform**: GitHub Actions or GitLab CI
- **Strategy**: Build on PR + main branch
- **Testing**: Unit tests + key E2E tests

**For Large Teams**:
- **Platform**: Bitrise, Appcenter, or custom
- **Strategy**: Multi-stage pipeline with gates
- **Testing**: Full test suite + device farm

### Release Strategy
**iOS Release Process**:
1. TestFlight beta (internal team)
2. TestFlight beta (external testers)
3. App Store review (3-7 days)
4. Phased rollout (25% → 50% → 100%)

**Android Release Process**:
1. Internal testing track
2. Closed testing track (beta users)
3. Open testing track (public beta)
4. Production release with staged rollout

## Security Best Practices

### Data Protection
- **API Keys**: Use environment variables, never commit
- **Sensitive Data**: Store in Keychain (iOS) / Keystore (Android)
- **Network**: Use HTTPS only, implement certificate pinning
- **Authentication**: Implement proper token management

### App Store Security
- **iOS**: Enable App Transport Security (ATS)
- **Android**: Use App Bundle signing, enable ProGuard
- **Both**: Regular security dependency updates

## Popular Library Ecosystem (2025)

### Essential Libraries
**Navigation**: React Navigation 6.x
**HTTP Client**: Axios or React Query
**Forms**: React Hook Form + Yup/Zod
**Date Handling**: date-fns or Day.js
**Icons**: React Native Vector Icons
**Animations**: React Native Reanimated 3.x

### Platform-Specific Libraries
**iOS Specific**:
- react-native-keychain (secure storage)
- @react-native-community/push-notification-ios
- react-native-permissions

**Android Specific**:
- react-native-android-keyboard-adjust
- @react-native-async-storage/async-storage
- react-native-splash-screen

### Quality & Monitoring
**Crash Reporting**: Flipper (dev) + Crashlytics (prod)
**Analytics**: Firebase Analytics or Mixpanel
**Performance**: Flipper + Xcode Instruments/Android Profiler
**Error Monitoring**: Sentry or Bugsnag

## Project Structure Best Practices

### Recommended Folder Structure
```
src/
├── components/          # Reusable UI components
│   ├── common/         # Cross-platform components
│   ├── ios/           # iOS-specific components
│   └── android/       # Android-specific components
├── screens/            # Screen components
├── navigation/         # Navigation configuration
├── services/          # API and external services
├── store/             # State management
├── utils/             # Utility functions
├── hooks/             # Custom hooks
├── types/             # TypeScript definitions
└── constants/         # App constants
```

### File Naming Conventions
- **Components**: PascalCase (e.g., `UserProfile.tsx`)
- **Screens**: PascalCase with "Screen" suffix (e.g., `LoginScreen.tsx`)
- **Hooks**: camelCase with "use" prefix (e.g., `useAuth.ts`)
- **Utilities**: camelCase (e.g., `formatDate.ts`)
- **Platform-specific**: `.ios.tsx` / `.android.tsx` extensions

## Accessibility Requirements

### iOS Accessibility (VoiceOver)
- **Minimum**: All interactive elements have accessibility labels
- **Target**: Full VoiceOver navigation support
- **Testing**: Use VoiceOver on real devices

### Android Accessibility (TalkBack)
- **Minimum**: All interactive elements have content descriptions
- **Target**: Full TalkBack navigation support
- **Testing**: Use TalkBack on real devices

### Cross-Platform Requirements
- **Text Scaling**: Support Dynamic Type (iOS) and font scaling (Android)
- **Color Contrast**: WCAG 2.1 AA compliance (4.5:1 normal, 3:1 large text)
- **Touch Targets**: 44x44 points minimum (iOS), 48x48dp minimum (Android)

## Market Considerations

### App Store Optimization (ASO)
**iOS App Store**:
- App name (30 chars) + subtitle (30 chars)
- Keywords field (100 chars)
- Screenshots (up to 10 per device type)
- App preview videos (30 seconds max)

**Google Play Store**:
- Title (30 chars)
- Short description (80 chars)
- Full description (4000 chars)
- Screenshots (up to 8 per device type)

### Regional Considerations
**Localization Strategy**:
- **Tier 1**: English (required)
- **Tier 2**: Spanish, French, German, Japanese, Chinese (Simplified)
- **Tier 3**: Based on target markets

**Legal/Privacy Requirements**:
- **GDPR**: European users
- **CCPA**: California users
- **COPPA**: Users under 13
- **App Store Privacy Labels**: Required

## Decision Trees for Common Questions

### "What iOS version should we support?"
```
New consumer app → iOS 13.0+ (max reach)
Enterprise app → iOS 15.0+ (security focus)
Feature-rich app → iOS 14.0+ (balance)
Quick MVP → iOS 13.0+ (React Native minimum)
```

### "What state management should we use?"
```
< 10 screens → Context + useReducer
10-30 screens + simple data → Zustand
10-30 screens + complex data → Redux Toolkit
30+ screens → Redux Toolkit + RTK Query
Team < 3 people → Zustand
Team 5+ people → Redux Toolkit
```

### "What testing strategy should we implement?"
```
MVP/Prototype → Manual testing + key unit tests
Small team → Unit tests + smoke E2E tests
Medium team → Full testing pyramid
Large team → Full automation + device farm
```

This guide should be referenced by all mobile agents when asking users technical questions, providing smart defaults and current best practices for 2025.