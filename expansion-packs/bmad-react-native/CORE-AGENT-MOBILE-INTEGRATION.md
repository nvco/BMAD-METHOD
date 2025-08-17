# Core Agent + Mobile Data Integration Guide

This document explains how BMad's core agents seamlessly work with mobile-specific data files to provide comprehensive React Native mobile development capabilities.

## Architecture Overview

The **core agents + mobile data** pattern provides mobile development capabilities without duplicating core functionality:

```
Core Agents (bmad-core) + Mobile Data Files (expansion) = Mobile Development Capability
```

### Why This Pattern Works

1. **No Duplication**: Core agents handle software development fundamentals
2. **Specialized Knowledge**: Mobile data files provide platform-specific expertise
3. **Seamless Integration**: Agents automatically access expansion data when active
4. **Maintained Consistency**: Core patterns ensure consistent development approach

## Core Agent Roles in Mobile Development

### 📊 PM Agent (`pm.md`)

**Mobile Capabilities:**
- Creates mobile PRDs using mobile user research methodologies
- Conducts mobile competitive analysis with app store considerations
- Defines mobile MVP scope with platform-specific requirements
- Plans mobile feature prioritization based on mobile best practices

**Mobile Data Access:**
- `mobile-best-practices-2025.md` - Current mobile development standards
- `react-native-vs-expo-decision-framework.md` - Technology selection guidance
- `mobile-user-research.md` via tasks - Mobile user research methodologies

**Example Usage:**
```
/ReactNative:agents:pm
# PM agent automatically references mobile user research, competitive analysis, and best practices
```

### 🏗️ Architect Agent (`architect.md`)

**Mobile Capabilities:**
- Designs mobile architecture with iOS and Android considerations
- Selects appropriate React Native patterns and libraries
- Plans cross-platform strategy with platform-specific adaptations
- Addresses mobile performance, security, and scalability

**Mobile Data Access:**
- `ios-guidelines.md` - iOS Human Interface Guidelines
- `android-guidelines.md` - Material Design principles
- `react-native-patterns.md` - React Native architectural patterns
- `performance-monitoring-setup.md` - Mobile performance considerations
- `mobile-architecture-tmpl.yaml` - Mobile-specific architecture template

**Example Usage:**
```
/ReactNative:agents:architect
# Architect agent references iOS/Android guidelines and React Native patterns
```

### 💻 Dev Agent (`dev.md`)

**Mobile Capabilities:**
- Implements React Native components following platform guidelines
- Writes cross-platform code with iOS and Android optimizations
- Handles mobile-specific features (navigation, permissions, storage)
- Applies mobile performance best practices and troubleshooting

**Mobile Data Access:**
- `mobile-development-workflow.md` - Daily development workflow
- `react-native-patterns.md` - Implementation patterns and examples
- `cross-platform-testing-pitfalls.md` - Common issues and solutions
- `mobile-troubleshooting.md` - Problem-solving guidance
- `mobile-project-setup-guide.md` - Project initialization steps

**Example Usage:**
```
/ReactNative:agents:dev
# Dev agent uses mobile patterns, iOS/Android guidelines, and troubleshooting guides
```

### 🧪 QA Agent (`qa.md`)

**Mobile Capabilities:**
- Validates mobile apps against platform compliance standards
- Performs cross-platform testing with mobile-specific scenarios
- Ensures app store submission readiness
- Verifies mobile performance and accessibility requirements

**Mobile Data Access:**
- `mobile-development-checklist.md` - Mobile quality gates
- `app-store-submission-checklist.md` - Store submission requirements
- `cross-platform-testing-pitfalls.md` - Testing considerations
- `ios-guidelines.md` / `android-guidelines.md` - Platform compliance

**Example Usage:**
```
/ReactNative:agents:qa
# QA agent applies mobile checklists and platform-specific validation
```

## Mobile Data File Categories

### 📱 Platform Guidelines
**Purpose**: Ensure platform compliance and native user experience

- **`ios-guidelines.md`**: iOS Human Interface Guidelines summary
  - Used by: Architect, Dev, UX Expert for iOS-specific design decisions
- **`android-guidelines.md`**: Material Design guidelines summary
  - Used by: Architect, Dev, UX Expert for Android-specific design decisions

### ⚛️ React Native Technical Knowledge
**Purpose**: Provide React Native-specific implementation guidance

- **`react-native-patterns.md`**: Development patterns and best practices
  - Used by: Architect, Dev for implementation decisions
- **`mobile-project-setup-guide.md`**: Complete project initialization
  - Used by: Dev for project setup and configuration
- **`mobile-development-workflow.md`**: Daily development best practices
  - Used by: Dev for efficient development practices

### 🚀 Performance & Quality
**Purpose**: Ensure mobile app performance and quality standards

- **`performance-monitoring-setup.md`**: Performance monitoring strategies
  - Used by: Architect, Dev, QA for performance validation
- **`cross-platform-testing-pitfalls.md`**: Common testing issues
  - Used by: Dev, QA for thorough testing approaches
- **`mobile-troubleshooting.md`**: Problem-solving guidance
  - Used by: Dev for debugging and issue resolution

### 🎯 Decision Support
**Purpose**: Guide technology and strategy decisions

- **`react-native-vs-expo-decision-framework.md`**: Technology selection
  - Used by: PM, Architect for platform decisions
- **`mobile-best-practices-2025.md`**: Current industry standards
  - Used by: All agents for up-to-date mobile guidance

## Integration Examples

### Example 1: Mobile Feature Development

**Scenario**: Implement push notifications

1. **PM Agent** references `mobile-best-practices-2025.md` for user engagement strategies
2. **Architect Agent** uses `ios-guidelines.md` and `android-guidelines.md` for platform notification patterns
3. **Dev Agent** follows `react-native-patterns.md` for implementation and `mobile-troubleshooting.md` for common issues
4. **QA Agent** validates against `mobile-development-checklist.md` for platform compliance

### Example 2: Cross-Platform Analysis

**Scenario**: Evaluate iOS vs Android implementation differences

1. **Architect Agent** analyzes using:
   - `ios-guidelines.md` for iOS-specific requirements
   - `android-guidelines.md` for Android-specific requirements
   - `cross-platform-testing-pitfalls.md` for implementation considerations
2. **Cross-Platform Analysis Task** provides structured evaluation framework
3. **Dev Agent** implements platform-specific optimizations using mobile patterns

### Example 3: App Store Preparation

**Scenario**: Prepare app for store submission

1. **QA Agent** validates using `app-store-submission-checklist.md`
2. **PM Agent** creates store listings using `app-store-listing-tmpl.yaml`
3. **App Store Submission Workflow** orchestrates the complete process
4. **Multiple agents** ensure compliance with iOS and Android requirements

## Best Practices for Integration

### For Agents
1. **Always Reference Mobile Data**: Check mobile-specific guidelines before generic approaches
2. **Platform-Specific Considerations**: Use iOS and Android guidelines for platform decisions
3. **Performance First**: Apply mobile performance standards from the start
4. **Cross-Platform Validation**: Test implementation against both platform requirements

### for Users
1. **Use ReactNative Prefix**: Always use `/ReactNative:` prefix to activate mobile capabilities
2. **Leverage Mobile Tasks**: Use `/ReactNative:tasks:` for specialized mobile processes
3. **Follow Mobile Workflows**: Use `/ReactNative:workflows:` for structured mobile development
4. **Validate with Mobile Checklists**: Apply mobile quality gates throughout development

## Data File Usage Patterns

### High-Frequency Usage
**Used in most mobile development scenarios:**
- `mobile-best-practices-2025.md` - Referenced by all agents
- `react-native-patterns.md` - Core development guidance
- `ios-guidelines.md` / `android-guidelines.md` - Platform compliance

### Task-Specific Usage
**Used for specific development phases:**
- `mobile-project-setup-guide.md` - Project initialization only
- `app-store-submission-checklist.md` - Store submission phase
- `performance-monitoring-setup.md` - Performance optimization phase

### Troubleshooting Usage
**Used when problems arise:**
- `mobile-troubleshooting.md` - General problem-solving
- `cross-platform-testing-pitfalls.md` - Testing issues
- `react-native-vs-expo-decision-framework.md` - Technology decisions

## Validation and Quality Assurance

### Automatic Integration Validation
Core agents automatically validate mobile requirements:

1. **Architect Agent** ensures mobile architecture follows platform guidelines
2. **Dev Agent** implements features using mobile best practices
3. **QA Agent** validates against mobile-specific quality gates
4. **PM Agent** creates mobile-appropriate requirements and scope

### Mobile-Specific Quality Gates
Additional mobile validation through:
- `mobile-development-checklist.md` - Platform compliance and performance
- `app-store-submission-checklist.md` - Store readiness validation
- Mobile workflows - Structured development and submission processes

## Troubleshooting Integration Issues

### Common Issues
1. **Missing Mobile Context**: Ensure `--ReactNative` flag is used
2. **Generic Solutions**: Core agents may provide generic answers without mobile data access
3. **Platform Conflicts**: iOS and Android requirements may conflict - use cross-platform analysis

### Solutions
1. **Explicit Mobile References**: Mention specific mobile requirements in prompts
2. **Use Mobile Tasks**: Leverage mobile-specific tasks for complex scenarios
3. **Validate Against Checklists**: Use mobile checklists to ensure complete coverage

## Summary

The core agent + mobile data integration provides:

✅ **Complete Mobile Coverage**: iOS, Android, and React Native expertise
✅ **No Duplication**: Leverages existing core agent capabilities
✅ **Seamless Experience**: Mobile knowledge automatically available to core agents
✅ **Quality Assurance**: Mobile-specific validation and quality gates
✅ **Store Readiness**: Complete app store submission guidance
✅ **Performance Focus**: Mobile performance standards and monitoring

This integration pattern ensures that BMad's proven core agents can provide expert mobile development guidance while maintaining the method's consistency and quality standards.