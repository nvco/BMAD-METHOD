# Mobile Development Workflow Examples

This document provides practical examples of how to use the BMad React Native expansion pack for common mobile development scenarios using Claude Code slash commands.

## Common Mobile Development Patterns

**Choose your development scenario to get started:**

### 1. Greenfield Development Pattern
```
Research → Plan → Design → Implement → Test → Submit
```
**Agent Flow:**
- **Research**: `/ReactNative:tasks:mobile-user-research` + `/ReactNative:tasks:mobile-competitive-analysis`
- **Plan**: `/ReactNative:agents:pm`
- **Design**: `/ReactNative:agents:architect` + `/ReactNative:tasks:cross-platform-analysis`
- **Implement**: `/ReactNative:agents:dev`
- **Test**: `/ReactNative:agents:qa`
- **Submit**: `/ReactNative:workflows:app-store-submission`

**Use when:** Building a new mobile app from scratch
**Start with:** [Greenfield Mobile App Development](#greenfield-mobile-app-development)

### 2. Existing Project Enhancement Pattern  
```
Analyze Current State → Plan Enhancement → Design Integration → Implement → Test → Deploy
```
**Agent Flow:**
- **Analyze Current State**: `/ReactNative:agents:architect` + `/ReactNative:tasks:mobile-user-research`
- **Plan Enhancement**: `/ReactNative:agents:pm` + `/ReactNative:tasks:mobile-competitive-analysis`
- **Design Integration**: `/ReactNative:agents:architect` + `/ReactNative:tasks:cross-platform-analysis`
- **Implement**: `/ReactNative:agents:dev`
- **Test**: `/ReactNative:agents:qa` + `/ReactNative:tasks:mobile-performance-optimization`
- **Deploy**: `/ReactNative:workflows:app-store-submission`

**Use when:** Adding features to existing mobile app or migrating existing app to React Native
**Start with:** [Existing Project Enhancement](#existing-project-enhancement)

### 3. Cross-Platform Implementation Pattern
```
Analyze Platform Differences → Design Shared Architecture → Implement Platform-Specific UI → Test Both Platforms
```
**Agent Flow:**
- **Analyze Platform Differences**: `/ReactNative:tasks:cross-platform-analysis`
- **Design Shared Architecture**: `/ReactNative:agents:architect`
- **Implement Platform-Specific UI**: `/ReactNative:agents:dev`
- **Test Both Platforms**: `/ReactNative:agents:qa`

**Use when:** Implementing features that need to work differently on iOS vs Android
**Start with:** [Cross-Platform Implementation](#cross-platform-implementation)

### 4. Performance Optimization Pattern
```
Measure → Identify Bottlenecks → Optimize → Monitor → Iterate
```
**Agent Flow:**
- **Measure**: `/ReactNative:tasks:mobile-performance-optimization`
- **Identify Bottlenecks**: `/ReactNative:tasks:mobile-performance-optimization`
- **Optimize**: `/ReactNative:agents:dev`
- **Monitor**: `/ReactNative:agents:architect` (setup monitoring)
- **Iterate**: Repeat `/ReactNative:agents:dev` + `/ReactNative:tasks:mobile-performance-optimization`

**Use when:** App performance issues need to be resolved
**Start with:** [Mobile Performance Optimization](#mobile-performance-optimization)

### 5. Store Submission Pattern
```
Prepare Assets → Validate Compliance → Submit → Monitor → Update
```
**Agent Flow:**
- **Prepare Assets**: `/ReactNative:agents:pm` (store listings) + `/ReactNative:agents:dev` (build preparation)
- **Validate Compliance**: `/ReactNative:agents:qa`
- **Submit**: `/ReactNative:workflows:app-store-submission`
- **Monitor**: `/ReactNative:workflows:app-store-submission` (includes monitoring)
- **Update**: `/ReactNative:agents:dev` (for required changes)

**Use when:** Ready to submit app to App Store and Google Play
**Start with:** [App Store Submission](#app-store-submission)

---

## Detailed Workflow Examples

**The sections below provide step-by-step expansions of the patterns above with complete examples, expected outputs, and specific scenarios:**

1. [Greenfield Mobile App Development](#greenfield-mobile-app-development) - *Detailed version of Pattern #1*
2. [Existing Project Enhancement](#existing-project-enhancement) - *Detailed version of Pattern #2*
3. [Mobile Feature Enhancement](#mobile-feature-enhancement) - *Feature-specific workflow example*
4. [Cross-Platform Implementation](#cross-platform-implementation) - *Detailed version of Pattern #3*
5. [App Store Submission](#app-store-submission) - *Detailed version of Pattern #5*
6. [Mobile Performance Optimization](#mobile-performance-optimization) - *Detailed version of Pattern #4*
7. [Mobile User Research & Competitive Analysis](#mobile-user-research--competitive-analysis) - *Standalone research workflows*

---

## Greenfield Mobile App Development

### Scenario: Building a new fitness tracking mobile app from scratch

#### Phase 1: Product Planning

```
# Start with mobile user research
/ReactNative:tasks:mobile-user-research

# Conduct mobile competitive analysis
/ReactNative:tasks:mobile-competitive-analysis

# Create mobile PRD with PM agent
/ReactNative:agents:pm
```

**Expected Outputs:**
- Mobile user research findings with mobile-specific insights
- Competitive analysis covering app store positioning and mobile features
- PRD optimized for mobile platforms with React Native considerations

#### Phase 2: Architecture Design

```
# Design mobile architecture
/ReactNative:agents:architect

# Analyze cross-platform considerations
/ReactNative:tasks:cross-platform-analysis
```

**Expected Outputs:**
- Mobile architecture using `mobile-architecture-tmpl.yaml`
- iOS and Android specific considerations
- React Native patterns and component structure
- Performance and security recommendations

#### Phase 3: Complete Development Workflow

```
# Execute full mobile development workflow
/ReactNative:workflows:mobile-greenfield-app
```

**Workflow Steps:**
1. Mobile user research and competitive analysis
2. Mobile PRD creation with MVP scoping
3. Mobile architecture design
4. Iterative development with mobile best practices
5. Cross-platform testing and validation
6. App store preparation

---

## Existing Project Enhancement

### Scenario: Adding React Native to existing native app or enhancing existing React Native app

#### Phase 1: Current State Analysis

```
# Analyze existing project architecture and constraints
/ReactNative:agents:architect

# Assess current mobile user experience and identify improvement opportunities  
/ReactNative:tasks:mobile-user-research

# Analyze competitive position and feature gaps
/ReactNative:tasks:mobile-competitive-analysis
```

**Expected Outputs:**
- Analysis of existing architecture and technical debt
- Current user experience assessment and improvement opportunities
- Competitive analysis showing feature gaps and market positioning

#### Phase 2: Enhancement Planning

```
# Create enhancement plan and roadmap
/ReactNative:agents:pm

# Design integration approach for new features with existing system
/ReactNative:agents:architect

# Plan cross-platform considerations for existing native components
/ReactNative:tasks:cross-platform-analysis
```

**Expected Outputs:**
- Enhancement PRD with clear scope and priorities
- Integration architecture preserving existing functionality
- Cross-platform migration strategy for selected features

#### Phase 3: Implementation Strategy

```
# Implement enhancements incrementally
/ReactNative:agents:dev

# Validate integration with existing systems
/ReactNative:agents:qa

# Monitor performance impact of new features
/ReactNative:tasks:mobile-performance-optimization
```

**Key Considerations for Existing Projects:**
- **Incremental Migration**: Add React Native features alongside existing native code
- **Data Integration**: Ensure new React Native components work with existing data layers
- **User Experience Continuity**: Maintain consistent UX across old and new features
- **Performance Monitoring**: Track impact of new features on app performance
- **Rollback Strategy**: Plan for reverting changes if issues arise

#### Phase 4: Production Deployment

```
# Prepare updated app for store submission
/ReactNative:agents:qa

# Execute app store update process
/ReactNative:workflows:app-store-submission
```

**Brownfield-Specific Outputs:**
- Migration plan for gradual feature rollout
- Integration testing strategy for new and existing features
- Performance impact assessment and optimization plan
- User communication strategy for feature updates

---

## Mobile Feature Enhancement

### Scenario: Adding biometric authentication to existing mobile app

#### Feature Planning

```
# Research mobile authentication best practices
/ReactNative:agents:dev

# Create feature architecture
/ReactNative:agents:architect
```

#### Implementation

```
# Implement biometric authentication
/ReactNative:agents:dev

# Validate implementation
/ReactNative:agents:qa
```

**Key Mobile Considerations:**
- iOS Face ID vs Android fingerprint differences
- Platform-specific permission handling
- Secure storage using mobile patterns
- Error handling and fallback mechanisms

---

## Cross-Platform Implementation

### Scenario: Implementing a camera feature that works optimally on both platforms

#### Cross-Platform Analysis

```
# Analyze platform differences
/ReactNative:tasks:cross-platform-analysis
```

**Analysis Output:**
- iOS camera API capabilities and limitations
- Android camera permissions and behavior
- React Native library recommendations
- Platform-specific UI considerations

#### Implementation Strategy

```
# Design cross-platform camera architecture
/ReactNative:agents:architect

# Implement with platform awareness
/ReactNative:agents:dev
```

**Key Outputs:**
- Platform-appropriate UI designs
- Shared business logic with platform-specific presentation
- Performance optimizations for each platform
- Testing strategy for both iOS and Android

---

## App Store Submission

### Scenario: Preparing and submitting app to both App Store and Google Play

#### Pre-Submission Preparation

```
# Create app store listings
/ReactNative:agents:pm

# Validate submission readiness
/ReactNative:agents:qa
```

#### Complete Submission Workflow

```
# Execute app store submission workflow
/ReactNative:workflows:app-store-submission
```

**Workflow Includes:**
1. App store asset preparation (icons, screenshots, descriptions)
2. iOS App Store submission process
3. Google Play Store submission process
4. Compliance verification for both platforms
5. Post-submission monitoring setup

**Expected Deliverables:**
- App Store Connect configured app
- Google Play Console configured app
- All required assets and metadata
- Compliance documentation
- Submission tracking and monitoring

---

## Mobile Performance Optimization

### Scenario: Optimizing app performance for better user experience

#### Performance Analysis

```
# Analyze current performance issues
/ReactNative:tasks:mobile-performance-optimization

# Get performance monitoring recommendations
/ReactNative:agents:architect
```

#### Implementation

```
# Implement performance optimizations
/ReactNative:agents:dev

# Set up performance monitoring
/ReactNative:agents:dev
```

**Performance Areas Covered:**
- App launch time optimization
- List scrolling performance
- Memory management
- Network request optimization
- Bundle size reduction
- Battery usage optimization

---

## Mobile User Research & Competitive Analysis

### Scenario: Understanding mobile market and user needs for a new feature

#### Mobile User Research

```
# Conduct mobile-specific user research
/ReactNative:tasks:mobile-user-research
```

**Research Output:**
- Mobile-specific user behaviors and preferences
- Platform usage patterns (iOS vs Android)
- Mobile app expectations and pain points
- Touch interaction patterns and accessibility needs

#### Competitive Analysis

```
# Analyze mobile app competition
/ReactNative:tasks:mobile-competitive-analysis
```

**Analysis Output:**
- App store positioning and ratings analysis
- Mobile feature comparison across platforms
- UI/UX pattern analysis for iOS and Android
- App store optimization opportunities
- Platform-specific competitive advantages

#### Strategic Planning

```
# Create strategic recommendations
/ReactNative:agents:pm
```

---

## Advanced Workflow Examples

### Multi-Platform Feature Rollout

```
# Plan phased rollout strategy
/ReactNative:agents:pm

# Design A/B testing for mobile
/ReactNative:agents:architect
```

### Mobile Accessibility Implementation

```
# Implement accessibility features
/ReactNative:agents:dev

# Validate accessibility compliance
/ReactNative:agents:qa
```

### Offline-First Mobile Architecture

```
# Design offline-first architecture
/ReactNative:agents:architect

# Implement offline functionality
/ReactNative:agents:dev
```

## Best Practices for Mobile Workflows

### 1. Always Start with Mobile Context
- Use `/ReactNative:` prefix for all mobile development commands
- Reference mobile-specific guidelines and patterns
- Consider both iOS and Android from the beginning

### 2. Leverage Mobile-Specific Tasks
- Use `/ReactNative:tasks:mobile-user-research` for user insights
- Use `/ReactNative:tasks:mobile-competitive-analysis` for market understanding
- Use `/ReactNative:tasks:cross-platform-analysis` for implementation planning

### 3. Apply Mobile Quality Gates
- Use `mobile-development-checklist` throughout development
- Use `app-store-submission-checklist` before submission
- Validate against platform-specific guidelines

### 4. Follow Mobile Performance Standards
- Target < 3 second app launch time
- Maintain 60fps during animations
- Optimize for mobile network conditions
- Test on real devices, not just simulators

### 5. Plan for Both Platforms
- Design platform-appropriate experiences
- Share business logic, adapt presentation
- Test thoroughly on both iOS and Android
- Consider platform-specific store requirements

---

These workflow examples demonstrate how the BMad React Native expansion pack provides comprehensive mobile development capabilities through the core agents + mobile data pattern, enabling professional mobile app development from concept to store submission.