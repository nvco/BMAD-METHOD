# BMad React Native Mobile Development Expansion Pack

A comprehensive React Native cross-platform mobile development expansion for the BMad Method, covering iOS and Android development with app store submission guidance.

## Overview

This expansion pack follows the proven **"core agents + specialized data"** pattern. Rather than creating duplicate mobile-specific agents, it provides mobile-specific knowledge, templates, and workflows that work seamlessly with BMad's core agents.

### Architecture Philosophy

- **Lean & Focused**: Uses core BMad agents enhanced with mobile-specific data files
- **Platform Coverage**: Full iOS and Android development support
- **Store-Ready**: Complete app store submission guidance for both platforms
- **Quality-First**: Mobile-specific quality gates and testing approaches

## What's Included

### 🤖 Agents
- **Uses Core Agents**: `dev.md`, `pm.md`, `architect.md`, `qa.md`, etc.
- **No Custom Agents**: Core agents work excellently with mobile data files
- **Enhanced Capabilities**: Core agents access mobile-specific knowledge seamlessly

### 📚 Mobile Data Files (11 total)
- `ios-guidelines.md` - iOS Human Interface Guidelines summary
- `android-guidelines.md` - Material Design guidelines summary  
- `mobile-best-practices-2025.md` - Current mobile development best practices
- `react-native-patterns.md` - React Native development patterns
- `performance-monitoring-setup.md` - Mobile performance monitoring
- `cross-platform-testing-pitfalls.md` - Common cross-platform issues
- `react-native-vs-expo-decision-framework.md` - Technology selection guide
- `mobile-troubleshooting.md` - Common mobile development issues
- `mobile-project-setup-guide.md` - Complete greenfield project setup
- `mobile-development-workflow.md` - Daily development workflow and best practices
- `bmad-kb.md` - Mobile-specific knowledge base integration

### 📋 Templates (2 mobile-specific)
- `mobile-architecture-tmpl.yaml` - Mobile architecture with app store considerations
- `app-store-listing-tmpl.yaml` - App Store and Play Store listing template

### 🎯 Tasks (5 mobile-specific)
- `app-store-submission.md` - iOS App Store and Google Play submission process
- `cross-platform-analysis.md` - React Native iOS/Android implementation analysis
- `mobile-competitive-analysis.md` - Mobile app competitive analysis
- `mobile-user-research.md` - Mobile user research methodology
- `mobile-performance-optimization.md` - Mobile-specific performance optimization

### 🔄 Workflows (2 mobile-specific)
- `mobile-greenfield-app.yaml` - Complete React Native app development workflow
- `app-store-submission.yaml` - iOS App Store and Google Play Store deployment

### ✅ Quality Checklists (2 mobile-specific)
- `app-store-submission-checklist.md` - Complete store submission requirements
- `mobile-development-checklist.md` - Mobile platform compliance and quality gates

## How It Works

### Core Agents + Mobile Data Pattern

1. **PM Agent** creates mobile PRDs using mobile competitive analysis and user research
2. **Architect Agent** designs mobile architecture using mobile patterns and guidelines  
3. **Dev Agent** implements React Native features using mobile best practices and troubleshooting guides
4. **QA Agent** validates using mobile development checklist and cross-platform testing guidance

### Example Usage (Claude Code)

```
# Start mobile greenfield project
/ReactNative:workflows:mobile-greenfield-app

# Create mobile architecture  
/ReactNative:agents:architect

# Implement mobile feature
/ReactNative:agents:dev

# Analyze cross-platform considerations
/ReactNative:tasks:cross-platform-analysis

# Prepare for app store submission
/ReactNative:workflows:app-store-submission
```

## Installation - For Local Dev ONLY

If you're working with this expansion pack from your own feature branch (e.g., contributing or using unreleased features):

Clone or navigate to the BMad-Method repository:
```bash
git clone https://github.com/bmadcode/bmad-method.git
cd bmad-method
```

Install dependencies:
```bash
npm install
```

Run the interactive installer
```bash
npm run install:bmad
```

**Important: Target Directory Paths**

When the installer prompts for your target project directory, you can use:

**Absolute path from BMad-Method repository (recommended):**
```
/Users/your-username/your-projects/your-new-project
```

**Relative path from BMad-Method repository:**
```
../your-new-project    # Goes up one level, then into your project folder
```

The installer will prompt you to select which expansion packs to include, where you can choose extra expansion packs along with the BMad-Method core.

## Mobile Development Workflows

The expansion pack provides comprehensive workflow guidance for mobile development:

### 📋 **Development Patterns & Examples**
**5 proven mobile development patterns** with specific agent commands and step-by-step guides.
→ **See: [`MOBILE-WORKFLOW-EXAMPLES.md`](MOBILE-WORKFLOW-EXAMPLES.md)**

### 🔗 **Core Agent Integration Guide** 
How core BMad agents work seamlessly with mobile-specific data files and knowledge.
→ **See: [`CORE-AGENT-MOBILE-INTEGRATION.md`](CORE-AGENT-MOBILE-INTEGRATION.md)**

### 📖 **Mobile Components Reference**
Complete documentation of all mobile-specific templates, tasks, workflows, and checklists.
→ **See: [`MOBILE-COMPONENTS-REFERENCE.md`](MOBILE-COMPONENTS-REFERENCE.md)**

## Quality Assurance

### Comprehensive Quality Gates

This expansion provides mobile-specific quality gates that complement core BMad checklists:

- **Mobile Platform Compliance**: iOS HIG and Material Design adherence
- **Performance Standards**: 60fps animations, < 3 second app launch
- **Cross-Platform Testing**: Multiple devices, OS versions, orientations  
- **App Store Readiness**: Complete submission requirements for both platforms
- **Security & Privacy**: Mobile-specific security practices and privacy compliance

### Testing Strategy

- **Unit Testing**: React Native Testing Library patterns
- **Integration Testing**: Cross-platform API and navigation testing
- **Device Testing**: Real device testing across iOS and Android
- **Performance Testing**: Mobile-specific performance benchmarks
- **Accessibility Testing**: VoiceOver and TalkBack compatibility

## Key Features

### 🎯 Platform-Specific Excellence
- **iOS**: Human Interface Guidelines, safe area handling, App Store submission
- **Android**: Material Design, back button behavior, Google Play submission
- **Cross-Platform**: Consistent functionality with platform-appropriate UI

### ⚡ Performance Focus
- **App Launch**: < 3 second cold start optimization
- **Runtime Performance**: 60fps animations and smooth scrolling
- **Memory Management**: Efficient memory usage and leak prevention
- **Network Optimization**: Offline capability and efficient API usage

### 🏪 Store-Ready
- **Complete Submission Guidance**: Step-by-step App Store and Play Store processes
- **Asset Management**: Icon requirements, screenshots, store listings
- **Compliance**: Privacy policies, age ratings, content guidelines
- **Post-Launch**: Update processes, user feedback handling

## Best Practices

### Development Approach
1. **Start with Core Agents**: Use `pm.md` and `architect.md` for planning
2. **Reference Mobile Data**: Access iOS/Android guidelines and React Native patterns
3. **Follow Mobile Workflows**: Use structured mobile development processes
4. **Validate Quality**: Apply mobile-specific checklists and testing approaches

### Cross-Platform Strategy
1. **Platform Parity**: Maintain feature consistency across iOS and Android
2. **Platform Adaptation**: Respect platform-specific UI conventions
3. **Performance Optimization**: Target mobile performance standards
4. **Testing Coverage**: Verify functionality on both platforms

## Troubleshooting

Common mobile development issues and solutions are documented in:
- `mobile-troubleshooting.md` - General mobile development issues
- `cross-platform-testing-pitfalls.md` - Platform-specific gotchas
- `performance-monitoring-setup.md` - Performance optimization guidance

## Contributing

This expansion pack follows BMad Method principles:
- **Minimal Complexity**: Only essential mobile-specific components
- **Core Integration**: Leverages core agents rather than duplicating functionality  
- **Practical Focus**: Real-world mobile development needs
- **Quality First**: Comprehensive testing and validation approaches

## Version History

- **v1.0.0**: Initial release with core agents + mobile data pattern
  - 11 mobile data files covering iOS, Android, and React Native
  - 2 mobile templates for architecture and app store listings
  - 5 mobile tasks for specialized mobile development processes
  - 2 mobile workflows for greenfield development and app store submission
  - 2 mobile checklists for quality assurance and store readiness

## Support

For issues, questions, or contributions:
- Check mobile troubleshooting guides in the `data/` directory
- Review mobile development checklist for quality validation
- Reference systematic plan for development methodology
- Follow established BMad Method patterns for consistency