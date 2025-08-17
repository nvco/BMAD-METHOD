# cross-platform-analysis

## Task Overview
**Purpose**: Analyze the iOS and Android implementation requirements for a React Native feature or component to identify platform-specific considerations, code differences, and potential challenges.

**When to Use**: 
- Before implementing complex React Native features
- When planning features that may have platform-specific behaviors
- During architecture planning for cross-platform compatibility
- When troubleshooting platform-specific issues

**Prerequisites**: 
- Feature requirements defined
- Understanding of target iOS and Android versions
- Access to platform guidelines (`ios-guidelines.md`, `android-guidelines.md`)

## Task Instructions

### Step 1: Feature Analysis Preparation

**Review Feature Requirements**
1. Load and analyze feature specifications from PRD or story documents
2. Identify all user-facing functionality and technical requirements
3. Note any performance or behavior expectations
4. Review acceptance criteria for platform-specific mentions

**Platform Guidelines Review**
1. Reference `data/ios-guidelines.md` for iOS-specific considerations
2. Reference `data/android-guidelines.md` for Android-specific considerations  
3. Review `data/react-native-patterns.md` for cross-platform implementation approaches
4. Check `data/mobile-best-practices-2025.md` for current platform standards

### Step 2: Platform-Specific Analysis

**iOS Implementation Analysis**
1. **Native iOS Behavior**: How would this feature work in a native iOS app?
   - iOS Human Interface Guidelines compliance
   - Native iOS components and patterns used
   - iOS-specific user experience expectations
   - iOS system integration requirements

2. **React Native iOS Considerations**:
   - Available React Native components for iOS
   - Potential need for iOS-specific native modules
   - iOS-specific styling and layout considerations
   - Performance implications on iOS devices

3. **iOS-Specific Challenges**:
   - App Store review guidelines compliance
   - iOS version compatibility requirements
   - Device-specific considerations (iPhone vs iPad)
   - iOS permissions and privacy requirements

**Android Implementation Analysis**
1. **Native Android Behavior**: How would this feature work in a native Android app?
   - Material Design guidelines compliance
   - Native Android components and patterns used
   - Android-specific user experience expectations
   - Android system integration requirements

2. **React Native Android Considerations**:
   - Available React Native components for Android
   - Potential need for Android-specific native modules
   - Android-specific styling and layout considerations
   - Performance implications on Android devices

3. **Android-Specific Challenges**:
   - Google Play Store policy compliance
   - Android API level compatibility requirements
   - Device fragmentation considerations
   - Android permissions and security requirements

### Step 3: Cross-Platform Implementation Strategy

**Shared Implementation Assessment**
1. **Common Functionality**: What can be implemented once for both platforms?
   - Business logic that's platform-agnostic
   - Shared components and utilities
   - Common data structures and API interactions
   - Reusable styling and layout patterns

2. **Platform-Specific Code Requirements**:
   - Platform detection needs (`Platform.OS === 'ios'`)
   - Platform-specific component implementations
   - Different styling approaches (iOS shadows vs Android elevation)
   - Platform-specific native module integrations

**React Native Technology Assessment**
1. **React Native Core Components**: Which built-in components can be used?
2. **Third-Party Libraries**: What existing libraries handle cross-platform differences?
3. **Native Modules**: Are custom native modules required for either platform?
4. **Performance Considerations**: Platform-specific optimization strategies

### Step 4: Implementation Recommendations

**Recommended Approach**
1. **Code Organization Strategy**:
   ```
   components/
   ├── shared/           # Platform-agnostic components
   ├── ios/             # iOS-specific implementations  
   ├── android/         # Android-specific implementations
   └── common/          # Components with platform variations
   ```

2. **Platform-Specific Implementation Patterns**:
   - Use `Platform.select()` for simple differences
   - Create separate `.ios.js` and `.android.js` files for major differences
   - Implement platform-specific native modules when needed
   - Use third-party libraries that handle platform differences

**Development Strategy**
1. **Phase 1**: Implement shared functionality
2. **Phase 2**: Add iOS-specific adaptations
3. **Phase 3**: Add Android-specific adaptations  
4. **Phase 4**: Test and optimize for both platforms

### Step 5: Risk Assessment and Mitigation

**Identified Risks**
1. **Platform Parity Risks**: Features that work differently on each platform
2. **Performance Risks**: Platform-specific performance bottlenecks
3. **Maintenance Risks**: Code that's difficult to maintain across platforms
4. **User Experience Risks**: Inconsistent UX between platforms

**Mitigation Strategies**
1. **Testing Strategy**: How to test on both platforms effectively
2. **Code Review Process**: Ensuring platform-specific code quality
3. **Documentation Needs**: What platform differences need to be documented
4. **Future Considerations**: How platform differences might evolve

## Task Outputs

**Cross-Platform Analysis Document**
Create a comprehensive analysis document including:

### Platform Comparison Matrix
| Aspect | iOS Implementation | Android Implementation | Shared Implementation |
|--------|-------------------|----------------------|---------------------|
| UI Components | [iOS-specific components] | [Android-specific components] | [Shared components] |
| User Interactions | [iOS patterns] | [Android patterns] | [Common patterns] |
| Styling Approach | [iOS styling] | [Android styling] | [Shared styles] |
| Performance Considerations | [iOS optimizations] | [Android optimizations] | [Common optimizations] |
| Testing Requirements | [iOS testing needs] | [Android testing needs] | [Shared testing] |

### Implementation Recommendations
1. **Shared Code Percentage**: Estimated % of code that can be shared
2. **Platform-Specific Requirements**: Detailed list for each platform
3. **Third-Party Dependencies**: Required libraries and their platform support
4. **Native Module Needs**: Custom native code requirements
5. **Testing Strategy**: Platform-specific testing approaches

### Development Timeline Impact
- **Shared Development Time**: Time for common functionality
- **iOS-Specific Time**: Additional time for iOS adaptations
- **Android-Specific Time**: Additional time for Android adaptations
- **Testing Time**: Platform-specific testing requirements
- **Total Estimated Time**: Complete cross-platform implementation

## Quality Checklist

Before marking this task complete, verify:
- [ ] Both iOS and Android platform requirements analyzed
- [ ] Platform-specific implementation challenges identified
- [ ] Shared vs platform-specific code strategy defined
- [ ] Third-party library dependencies evaluated
- [ ] Performance considerations documented for both platforms
- [ ] Testing strategy addresses platform differences
- [ ] Implementation recommendations are actionable
- [ ] Risk mitigation strategies are practical

## Common Analysis Patterns

**UI/UX Features**
- Navigation patterns (iOS navigation vs Android material navigation)
- Form controls (iOS picker vs Android spinner)
- Gestures and interactions (iOS swipe vs Android touch patterns)
- Visual feedback (iOS haptics vs Android vibration)

**System Integration Features**
- Permissions handling (different permission models)
- Background processing (platform-specific limitations)
- Push notifications (different providers and configurations)
- Deep linking (different URL scheme handling)

**Performance-Critical Features**
- Image handling (platform-specific optimizations)
- List rendering (platform-specific virtualization)
- Animation performance (iOS vs Android animation systems)
- Memory management (different garbage collection behaviors)

## Success Criteria

This task is complete when:
1. Comprehensive platform analysis completed for both iOS and Android
2. Clear implementation strategy defined with specific recommendations
3. Platform-specific risks and mitigation strategies identified
4. Development team has actionable guidance for cross-platform implementation
5. Testing approach addresses platform differences appropriately

## Related Resources

- `data/ios-guidelines.md` - iOS Human Interface Guidelines
- `data/android-guidelines.md` - Material Design guidelines
- `data/react-native-patterns.md` - Cross-platform implementation patterns
- `data/cross-platform-testing-pitfalls.md` - Common testing issues
- `data/mobile-troubleshooting.md` - Platform-specific problem solving