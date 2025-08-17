# Mobile-Specific Components Reference

This document provides detailed documentation for all mobile-specific components created in the BMad React Native expansion pack.

## Component Categories Overview

- **Templates (2)**: Mobile architecture and app store listings
- **Tasks (5)**: Mobile-specific development processes  
- **Workflows (2)**: Complete mobile development and submission flows
- **Checklists (2)**: Mobile quality gates and store submission validation
- **Data Files (11)**: Mobile knowledge and guidelines

---

## 📋 Templates

### 1. `mobile-architecture-tmpl.yaml`

**Purpose**: Architecture template specifically designed for mobile applications with iOS and Android considerations.

**Key Sections:**
- **Mobile Platform Strategy**: iOS vs Android approach
- **Cross-Platform Architecture**: Shared vs platform-specific components
- **Mobile Performance Considerations**: App launch, memory, battery
- **App Store Requirements**: Platform-specific compliance needs
- **Mobile Security**: Device-specific security patterns
- **Navigation & UX Patterns**: Platform-appropriate navigation
- **State Management**: Mobile-optimized state handling
- **Offline Capabilities**: Mobile network considerations

**Usage:**
```
/ReactNative:agents:architect
```

**Differs from Core Architecture Template:**
- Includes mobile platform considerations
- Covers app store submission requirements
- Addresses mobile performance standards
- Includes mobile-specific security patterns

### 2. `app-store-listing-tmpl.yaml`

**Purpose**: Template for creating App Store and Google Play Store listings with platform-specific requirements.

**Key Sections:**
- **App Store Connect (iOS)**: App metadata, keywords, descriptions
- **Google Play Console (Android)**: Store listing details, content rating
- **Visual Assets**: Icons, screenshots, promotional materials
- **Privacy & Compliance**: Privacy policies, age ratings, content guidelines
- **Localization**: Multi-language store presence
- **App Store Optimization (ASO)**: Keyword strategy and positioning

**Usage:**
```
/ReactNative:agents:pm
```

**Mobile-Unique Features:**
- Platform-specific metadata requirements
- Mobile app store optimization strategies
- Visual asset specifications for mobile stores
- Mobile privacy and compliance considerations

---

## 🎯 Tasks

### 1. `app-store-submission.md`

**Purpose**: Complete process for submitting apps to both iOS App Store and Google Play Store.

**Process Steps:**
- **Pre-Submission Preparation**: Asset creation, compliance verification
- **iOS App Store Process**: App Store Connect configuration, review guidelines
- **Google Play Process**: Play Console setup, policy compliance
- **Cross-Platform Considerations**: Maintaining consistency across stores
- **Post-Submission**: Monitoring, user feedback, updates

**Key Deliverables:**
- Store-ready app builds
- Complete metadata and assets
- Privacy policy and compliance documentation
- Submission timeline and checklist

### 2. `cross-platform-analysis.md`

**Purpose**: Systematic analysis of iOS vs Android implementation considerations for mobile features.

**Analysis Framework:**
- **Platform Capabilities**: Native feature availability
- **UI/UX Differences**: iOS HIG vs Material Design
- **Performance Considerations**: Platform-specific optimizations
- **Implementation Strategy**: Shared vs platform-specific code
- **Testing Approach**: Platform-specific testing needs

**Output Format:**
- Comparison matrix of platform differences
- Implementation recommendations
- Risk assessment for each platform
- Development effort estimation

### 3. `mobile-competitive-analysis.md`

**Purpose**: Mobile app competitive analysis with app store and platform-specific considerations.

**Analysis Areas:**
- **App Store Presence**: Rankings, reviews, ASO strategies
- **Mobile Feature Comparison**: Platform-specific feature sets
- **UI/UX Patterns**: Mobile design trends and patterns
- **Performance Benchmarks**: App store ratings and user feedback
- **Platform Strategy**: iOS vs Android market positioning

**Mobile-Specific Elements:**
- App store optimization analysis
- Mobile user review sentiment analysis
- Platform-specific competitive advantages
- Mobile feature gap analysis

### 4. `mobile-user-research.md`

**Purpose**: Mobile-specific user research methodologies and considerations.

**Research Methods:**
- **Mobile User Interviews**: Touch interaction preferences, device usage patterns
- **App Store Research**: User review analysis, rating factors
- **Mobile Usability Testing**: Device-specific testing approaches
- **Cross-Platform User Behavior**: iOS vs Android user differences
- **Mobile Accessibility Research**: Assistive technology usage patterns

**Mobile Considerations:**
- Device form factor impact on usage
- Platform ecosystem preferences
- Mobile-specific pain points and opportunities
- Touch interaction and gesture preferences

### 5. `mobile-performance-optimization.md`

**Purpose**: Mobile-specific performance optimization strategies and implementation.

**Optimization Areas:**
- **App Launch Performance**: Cold start optimization, splash screens
- **Runtime Performance**: 60fps animations, smooth scrolling
- **Memory Management**: Mobile memory constraints, optimization techniques
- **Network Optimization**: Mobile network conditions, offline capabilities
- **Battery Usage**: Power-efficient implementation patterns
- **Bundle Size**: App store size limits, optimization strategies

**Implementation Approach:**
- Performance measurement and monitoring
- Platform-specific optimization techniques
- React Native performance best practices
- Mobile-specific profiling tools

---

## 🔄 Workflows

### 1. `mobile-greenfield-app.yaml`

**Purpose**: Complete React Native mobile app development workflow from concept to store-ready application.

**Workflow Phases:**

#### Planning Phase
- Mobile user research and analysis
- Mobile competitive analysis
- MVP scoping with mobile considerations
- Technology selection (React Native vs Expo)

#### Architecture Phase
- Mobile architecture design
- Cross-platform strategy definition
- Performance and security planning
- Component and navigation design

#### Development Phase
- Project setup and configuration
- Iterative feature development
- Cross-platform implementation
- Mobile best practices application

#### Testing Phase
- Cross-platform testing
- Mobile device testing
- Performance validation
- Accessibility testing

#### Deployment Phase
- App store preparation
- Submission process
- Post-launch monitoring

**Key Features:**
- Full mobile development lifecycle
- Platform-specific considerations throughout
- Quality gates at each phase
- Store submission preparation

### 2. `app-store-submission.yaml`

**Purpose**: Complete app store submission workflow for both iOS App Store and Google Play Store.

**Submission Process:**

#### Asset Preparation
- Icon generation and optimization
- Screenshot creation and localization
- Store listing content creation
- Privacy policy and legal document preparation

#### iOS Submission
- App Store Connect configuration
- Build upload and processing
- Metadata and asset submission
- Review process management

#### Android Submission
- Google Play Console setup
- App bundle upload and processing
- Store listing completion
- Release management

#### Post-Submission
- Review monitoring and response
- Launch analytics setup
- User feedback monitoring
- Update planning and scheduling

**Store-Specific Features:**
- Platform-specific requirements handling
- Compliance verification for both stores
- Release management strategies
- Post-launch support processes

---

## ✅ Checklists

### 1. `app-store-submission-checklist.md`

**Purpose**: Comprehensive checklist ensuring app store submission readiness for both platforms.

**iOS App Store Sections:**
- App Store Connect setup and configuration
- App binary requirements and optimization
- App icons and visual assets
- Screenshots and promotional media
- App metadata and descriptions
- Privacy and compliance requirements
- Technical requirements and guidelines
- Content guidelines compliance

**Google Play Store Sections:**
- Google Play Console setup
- App bundle requirements
- App icons and promotional assets
- Store listing optimization
- Technical requirements
- Content policy compliance
- Data safety section completion

**Cross-Platform Requirements:**
- Legal and business compliance
- Quality assurance validation
- User experience standards
- Analytics and monitoring setup

### 2. `mobile-development-checklist.md`

**Purpose**: Mobile-specific quality gates covering platform compliance, performance, and mobile best practices.

**Quality Gate Categories:**

#### Mobile Platform Compliance
- iOS Human Interface Guidelines adherence
- Android Material Design compliance
- Platform-specific navigation patterns
- Touch target size requirements
- Accessibility compliance

#### Mobile Performance Standards
- App launch time requirements (< 3 seconds)
- Runtime performance targets (60fps)
- Memory management validation
- Network and data optimization
- Battery usage optimization

#### Mobile-Specific Testing
- Cross-platform device testing
- Platform-specific feature validation
- Mobile accessibility testing
- Performance testing on various devices

#### Mobile Security & Privacy
- Secure data storage practices
- Network security implementation
- Privacy compliance validation
- Platform security requirements

#### App Store Readiness
- Build preparation and optimization
- Store asset preparation
- Compliance verification
- Submission readiness validation

---

## 📚 Data Files

### Platform Guidelines (2 files)

#### `ios-guidelines.md`
**Content**: iOS Human Interface Guidelines summary
- Design principles and patterns
- Navigation and interaction guidelines
- Visual design standards
- Accessibility requirements
- Platform-specific UI components

#### `android-guidelines.md`
**Content**: Material Design guidelines summary
- Material Design principles
- Component specifications
- Interaction patterns
- Accessibility guidelines
- Android-specific UI patterns

### React Native Technical Knowledge (4 files)

#### `react-native-patterns.md`
**Content**: React Native development patterns and best practices
- Component architecture patterns
- State management approaches
- Navigation implementation
- Performance optimization patterns
- Testing strategies

#### `mobile-project-setup-guide.md`
**Content**: Complete greenfield project setup walkthrough
- Development environment setup
- Project initialization steps
- Configuration and tooling setup
- Platform-specific setup requirements

#### `mobile-development-workflow.md`
**Content**: Daily development workflow and best practices
- Development process guidelines
- Code organization patterns
- Testing and debugging workflows
- Platform-specific development tips

#### `mobile-troubleshooting.md`
**Content**: Common mobile development issues and solutions
- Platform-specific troubleshooting
- Performance issue resolution
- Build and deployment problems
- Common React Native issues

### Performance & Quality (2 files)

#### `performance-monitoring-setup.md`
**Content**: Mobile performance monitoring strategies
- Performance metrics and targets
- Monitoring tool setup
- Performance optimization techniques
- Crash reporting and analytics

#### `cross-platform-testing-pitfalls.md`
**Content**: Common cross-platform testing issues
- Platform-specific testing considerations
- Common compatibility issues
- Testing strategy recommendations
- Automated testing approaches

### Decision Support (2 files)

#### `react-native-vs-expo-decision-framework.md`
**Content**: Technology selection guidance
- React Native vs Expo comparison
- Decision criteria and frameworks
- Use case recommendations
- Migration considerations

#### `mobile-best-practices-2025.md`
**Content**: Current mobile development best practices
- Industry standards and trends
- Platform-specific best practices
- Performance and security guidelines
- User experience standards

### Knowledge Base (1 file)

#### `bmad-kb.md`
**Content**: Mobile-specific knowledge base integration
- Mobile development terminology
- Platform-specific concepts
- Best practice summaries
- Quick reference guides

---

## Component Integration

### How Components Work Together

1. **Data Files** provide foundational mobile knowledge
2. **Templates** structure mobile-specific documents
3. **Tasks** handle specialized mobile processes
4. **Workflows** orchestrate complete mobile development cycles
5. **Checklists** ensure quality and compliance

### Usage Patterns

- **Core Agents** automatically access data files when using `/ReactNative:agents:` commands
- **Templates** are used by core agents for structured document creation
- **Tasks** provide specialized mobile processes via `/ReactNative:tasks:` commands
- **Workflows** combine multiple agents and tasks via `/ReactNative:workflows:` commands
- **Checklists** validate quality throughout development and submission

This comprehensive set of mobile-specific components ensures complete React Native mobile development coverage while maintaining the lean, focused approach of the BMad Method.