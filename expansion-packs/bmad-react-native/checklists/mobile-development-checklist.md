# Mobile Development Quality Gates Checklist

This checklist covers **mobile-specific** quality gates not addressed by core BMad checklists. Use alongside core checklists (story-dod-checklist.md, architect-checklist.md, etc.) for comprehensive mobile development validation.

**Prerequisites**: Complete core BMad checklists first, then use this for mobile-specific validation.

---

## 📱 Mobile Platform Compliance

### iOS Platform Requirements
- [ ] **iOS Human Interface Guidelines**: UI follows iOS design patterns and conventions
- [ ] **Safe Area Handling**: Proper support for iPhone notch/Dynamic Island and safe areas
- [ ] **Status Bar Management**: Status bar style appropriate for content (light/dark)
- [ ] **Navigation Patterns**: Uses iOS-standard navigation (NavigationView, TabView patterns)
- [ ] **Touch Targets**: All interactive elements meet 44x44 point minimum size requirement
- [ ] **Haptic Feedback**: Appropriate haptic feedback for user interactions
- [ ] **iOS Permissions**: Permission requests include clear usage descriptions in Info.plist

### Android Platform Requirements
- [ ] **Material Design Guidelines**: UI follows Material Design principles and patterns
- [ ] **Edge-to-Edge Display**: Proper handling of status bar and navigation bar areas
- [ ] **Back Button Behavior**: Hardware back button handled correctly throughout app
- [ ] **Touch Targets**: All interactive elements meet 48x48dp minimum size requirement
- [ ] **Material Animations**: Smooth transitions following Material Motion principles
- [ ] **Android Permissions**: Runtime permissions requested properly with rationale
- [ ] **Target API Level**: App targets recent Android API level (API 33+ for 2024)

### Cross-Platform Consistency
- [ ] **Platform-Appropriate UI**: UI adapts to platform conventions while maintaining brand
- [ ] **Consistent Functionality**: Core features work identically across platforms
- [ ] **Platform-Specific Features**: Platform-unique features appropriately implemented
- [ ] **Shared Components**: Common components maintain platform-appropriate styling

---

## 🚀 Mobile Performance Standards

### App Launch Performance
- [ ] **Cold Start Time**: App launches to usable state in under 3 seconds
- [ ] **Warm Start Time**: App resumes from background in under 1 second
- [ ] **Splash Screen**: Launch screen displays immediately, no blank screens
- [ ] **Progressive Loading**: Critical content loads first, secondary content loads progressively

### Runtime Performance
- [ ] **60fps Target**: Maintains 60fps during animations and scrolling
- [ ] **Smooth Scrolling**: Lists and scroll views perform smoothly with large datasets
- [ ] **Memory Management**: No memory leaks, memory usage stays within reasonable bounds
- [ ] **Background Processing**: Heavy operations moved off main thread
- [ ] **Battery Usage**: App doesn't cause excessive battery drain

### Network & Data Performance
- [ ] **Offline Functionality**: Core features available with limited/no connectivity
- [ ] **Data Caching**: Appropriate caching strategy for images and API responses
- [ ] **Network Optimization**: Minimal and optimized API calls
- [ ] **Large Data Sets**: Efficient handling of large lists (virtualization, pagination)
- [ ] **Image Optimization**: Images compressed and cached appropriately

---

## 📱 Mobile-Specific Testing Requirements

### Device Testing
- [ ] **Multiple iOS Devices**: Tested on at least iPhone SE, standard iPhone, and iPhone Pro Max
- [ ] **Multiple Android Devices**: Tested on devices with different screen sizes and Android versions
- [ ] **Tablet Support**: If applicable, tested on iPad and Android tablets
- [ ] **Different OS Versions**: Verified compatibility with supported OS versions
- [ ] **Physical Device Testing**: Critical paths tested on real devices, not just simulators

### Platform-Specific Features
- [ ] **iOS-Specific Testing**: Deep links, universal links, push notifications, app lifecycle
- [ ] **Android-Specific Testing**: App links, notifications, background behavior, permissions
- [ ] **Orientation Changes**: App handles portrait/landscape transitions gracefully
- [ ] **Multi-Window Support**: App works correctly in split-screen mode (Android/iPad)

### Mobile Accessibility
- [ ] **Screen Reader Testing**: VoiceOver (iOS) and TalkBack (Android) navigation works correctly
- [ ] **Accessibility Labels**: All interactive elements have meaningful accessibility labels
- [ ] **Focus Management**: Logical focus order for keyboard and screen reader navigation
- [ ] **Contrast Compliance**: Text contrast meets WCAG guidelines
- [ ] **Dynamic Type Support**: Text scales appropriately with user's font size preferences

### Performance Testing
- [ ] **Low-End Device Testing**: Tested on older/slower devices within supported range
- [ ] **Network Condition Testing**: Tested with slow/intermittent network connections
- [ ] **Memory Pressure Testing**: App handles low memory conditions gracefully
- [ ] **Background/Foreground Testing**: App state preserved during app switching

---

## 🔒 Mobile Security & Privacy

### Data Protection
- [ ] **Secure Storage**: Sensitive data stored securely (Keychain/Android Keystore)
- [ ] **Network Security**: All network calls use HTTPS/TLS encryption
- [ ] **Certificate Pinning**: Implemented for critical API communications if required
- [ ] **Input Validation**: All user inputs validated and sanitized
- [ ] **Deep Link Validation**: Deep links validated to prevent malicious URLs

### Privacy Compliance
- [ ] **Permission Requests**: Clear explanations before requesting device permissions
- [ ] **Data Collection Transparency**: Users informed about what data is collected
- [ ] **Data Retention**: Clear policy on how long user data is stored
- [ ] **User Consent**: Proper consent mechanisms for data collection
- [ ] **Children's Privacy**: COPPA compliance if app may be used by children under 13

### Platform Security
- [ ] **iOS App Transport Security**: ATS properly configured, no arbitrary loads
- [ ] **Android Network Security**: Network security config properly implemented
- [ ] **Code Obfuscation**: Production builds use code obfuscation (ProGuard/R8)
- [ ] **Debug Information**: No debug information or logs in production builds

---

## 📊 Mobile Analytics & Monitoring

### Crash and Error Monitoring
- [ ] **Crash Reporting**: Comprehensive crash reporting implemented and tested
- [ ] **Error Tracking**: Non-fatal errors tracked and categorized
- [ ] **Performance Monitoring**: Key performance metrics tracked (app start, network, rendering)
- [ ] **User Session Tracking**: User flows and session data collected (privacy-compliant)

### Mobile-Specific Metrics
- [ ] **App Launch Analytics**: Cold/warm start times monitored
- [ ] **Screen Performance**: Frame rates and jank tracked on key screens
- [ ] **Network Performance**: API response times and failure rates monitored
- [ ] **User Engagement**: Screen views, feature usage, and retention tracked
- [ ] **Platform-Specific Metrics**: iOS/Android specific performance metrics

---

## 🏪 App Store Readiness

### Build Preparation
- [ ] **Release Build Configuration**: Optimized builds with production settings
- [ ] **Code Signing**: Proper certificates and provisioning profiles configured
- [ ] **Version Management**: Version numbers properly incremented
- [ ] **Bundle Analysis**: App bundle size analyzed and optimized

### Store Assets Preparation
- [ ] **App Icons**: All required icon sizes generated and optimized
- [ ] **Screenshots**: Platform-appropriate screenshots captured with real content
- [ ] **App Descriptions**: Store listings written following platform guidelines
- [ ] **Keywords/Tags**: Relevant keywords selected for app discovery

### Compliance Verification
- [ ] **Content Guidelines**: App content complies with App Store and Play Store policies
- [ ] **Age Rating**: Appropriate age rating selected based on app content
- [ ] **Privacy Policy**: Complete privacy policy accessible and accurate
- [ ] **Terms of Service**: Clear terms of service provided if required

---

## ✅ Mobile Development Completion Criteria

### Technical Readiness
- [ ] **Core Functionality**: All primary user flows work correctly on both platforms
- [ ] **Performance Targets**: App meets mobile performance standards defined above
- [ ] **Platform Compliance**: App follows both iOS and Android platform guidelines
- [ ] **Security Standards**: All mobile security requirements implemented

### Quality Assurance
- [ ] **Automated Testing**: Mobile-specific tests pass (unit, integration, UI tests)
- [ ] **Manual Testing**: Comprehensive manual testing completed on target devices
- [ ] **User Acceptance**: Key user scenarios validated with real users if possible
- [ ] **Regression Testing**: Existing functionality verified after new changes

### Documentation & Handoff
- [ ] **Mobile Implementation Notes**: Mobile-specific implementation details documented
- [ ] **Device Compatibility**: Supported devices and OS versions clearly documented
- [ ] **Known Limitations**: Any platform-specific limitations or workarounds noted
- [ ] **Deployment Instructions**: Mobile build and deployment process documented

---

**📱 Mobile Quality Gates Complete**: When all items are verified, the mobile application meets professional mobile development standards and is ready for store submission and user release.