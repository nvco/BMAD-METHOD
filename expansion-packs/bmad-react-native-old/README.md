# BMad React Native Cross-Platform Expansion Pack

Transform your BMad-Method installation into a powerful React Native development team with specialized mobile agents for iOS and Android.

## Overview

This expansion pack extends BMad-Method with React Native cross-platform development expertise, providing specialized agents that understand mobile development patterns, iOS Human Interface Guidelines, Material Design, and React Native best practices.

## Features

- 🏗️ **Cross-Platform Architecture** - React Native system design optimized for iOS and Android
- ⚛️ **React Native Development** - Component implementation with TypeScript and performance focus
- 🎨 **Platform-Native UX Design** - iOS HIG and Material Design compliance with mobile-first approach
- 📋 **Mobile Sprint Management** - Story creation with complete cross-platform context
- 🧪 **Comprehensive QA & Testing** - Cross-platform testing with device coverage and performance validation
- 🗺️ **Platform Awareness** - Intelligent handling of iOS and Android differences
- 🎯 **Smart Recommendations** - 2025 best practices with intelligent defaults and decision frameworks
- 📊 **Performance Monitoring** - Complete setup guides for development and production monitoring
- 🚀 **App Store Ready** - Comprehensive submission checklists for iOS App Store and Google Play
- 🧪 **Test Templates** - Ready-to-use unit, integration, and E2E test templates

## Included Agents

### 1. Mobile Business Analyst (Alex)
- Mobile market research and app store intelligence
- Competitive mobile app analysis and positioning
- Mobile user acquisition and retention strategy
- Cross-platform market opportunity assessment
- Mobile business model and monetization analysis

### 2. Mobile Product Manager (Jordan)
- Mobile PRD creation with iOS and Android considerations
- Cross-platform mobile product strategy and roadmap planning
- App Store and Google Play submission strategy
- Mobile user acquisition and retention planning
- Mobile analytics and KPI definition

### 3. Mobile Product Owner (Taylor)
- Mobile backlog management with platform considerations
- Mobile story refinement and acceptance criteria
- Cross-platform development coordination
- App store submission readiness validation
- Mobile quality gates and validation

### 4. Mobile Architect (Maxwell)
- React Native architecture patterns for cross-platform development
- State management selection (Redux, Zustand, Context)
- Performance optimization strategies for both platforms
- Native module integration planning (iOS and Android)
- Platform-specific architectural considerations

### 5. Mobile Developer (Morgan)
- React Native component implementation
- Cross-platform feature development (iOS and Android)
- Debugging with Flipper, React DevTools, Xcode, and Android Studio
- Performance profiling and optimization
- Testing with Jest and React Native Testing Library

### 6. Mobile UX Designer (Riley)
- iOS Human Interface Guidelines and Material Design expertise
- Mobile-first responsive design for both platforms
- Touch interactions and platform-specific gestures
- Cross-platform accessibility implementation
- Design to code specifications with platform awareness

### 7. Mobile Scrum Master (Casey)
- React Native story creation with platform considerations
- Mobile sprint planning for cross-platform development
- iOS and Android release cycle management
- App Store and Google Play submission coordination
- Complete cross-platform context in every story

### 8. Mobile QA Specialist (Quinn)
- Cross-platform mobile testing strategy and implementation
- React Native Testing Library and Jest expertise
- iOS Simulator and Android Emulator testing coordination
- Real device testing and platform-specific validation
- Performance testing and accessibility compliance (VoiceOver/TalkBack)

### 9. Mobile Master Task Executor
- Universal mobile development task execution
- Comprehensive React Native and cross-platform expertise
- Mobile workflow coordination and resource management
- Mobile knowledge base access and guidance
- Complex mobile development task orchestration

### 10. Mobile Orchestrator
- Mobile workflow coordination and agent management
- Cross-platform mobile development orchestration
- Mobile team coordination and task assignment
- Mobile project workflow guidance and planning
- Comprehensive mobile development process coordination

## Installation

### Local Development Installation ONLY

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

## Recommended Setup: MCP Documentation Server

For the best development experience, the mobile agents can access real-time documentation through the Context7 MCP server. This provides:
- Latest React Native API documentation
- Current iOS SDK references
- TypeScript and library documentation
- Up-to-date best practices and patterns

### Setting up MCP Server

#### Option 1: Cursor IDE
If using Cursor IDE, create `.cursor/mcp.json`:
```json
{
  "mcpServers": {
    "context7": {
      "url": "https://mcp.context7.com/mcp"
    }
  }
}
```

#### Option 2: Claude Code
For Claude Code users:

1. **Create configuration directory**:
   ```bash
   mkdir -p .claude
   ```

2. **Add MCP configuration**:
   Create `.claude/mcp.json` with:
   ```json
   {
     "mcpServers": {
       "context7": {
         "transport": "http",
         "url": "https://mcp.context7.com/mcp"
       }
     }
   }
   ```

3. **Or use Claude Code CLI**:
   ```bash
   claude mcp add --transport http context7 https://mcp.context7.com/mcp
   ```

Once configured, the mobile agents will automatically use the MCP server to:
- Verify API availability and usage
- Check for deprecated patterns
- Access latest documentation
- Ensure compatibility with current versions

**Note**: The expansion pack works without MCP, but having it configured ensures agents provide the most current and accurate guidance.

## Enhanced Capabilities

### 🎯 Intelligent Decision Support
- **React Native CLI vs Expo**: Smart decision framework based on project requirements
- **Technology Stack**: Complexity-based recommendations (Context API vs Zustand vs Redux)
- **Platform Support**: Informed iOS/Android version recommendations with device coverage data
- **Performance Targets**: Specific benchmarks for startup time, frame rate, and memory usage

### 📊 Production-Ready Monitoring
- **Development Tools**: React DevTools, Flipper, Metro bundle analysis
- **Performance Tracking**: Custom trackers, screen load monitoring, memory management
- **Production Monitoring**: Crashlytics integration, analytics setup, performance dashboards
- **Platform-Specific**: Xcode Instruments and Android Studio Profiler guidance

### 🚀 App Store Success
- **iOS App Store**: Complete submission checklist with metadata, privacy, and technical requirements
- **Google Play**: Comprehensive Play Console requirements and content policy compliance
- **Cross-Platform**: Legal, accessibility, and quality assurance requirements
- **Rejection Prevention**: Common rejection reasons and how to avoid them

### 🧪 Complete Testing Strategy
- **Unit Tests**: Component testing templates with React Native Testing Library
- **Integration Tests**: Workflow testing with navigation, state management, and API integration
- **E2E Tests**: Complete user journey testing with Detox for both iOS and Android
- **Performance Tests**: Load time validation and memory usage testing

## Usage

### Starting a New React Native Project

1. **Planning Phase (Web UI or IDE)**
   ```
   *analyst → Create project brief
   *pm → Create PRD with mobile requirements
   *mobile-ux → Design platform-appropriate interfaces
   *mobile-architect → Design cross-platform React Native architecture
   ```

2. **Development Phase (IDE)**
   ```
   *mobile-sm → Create implementation stories
   *mobile-dev → Implement features
   *mobile-qa → Test and validate across platforms
   ```

### Working with Designs

The mobile-ux agent can work with:
- Existing mockups and screenshots (provide in `/docs/design/`)
- Figma/Sketch specifications (describe in detail)
- Or create specifications from requirements

### Technology Stack

**Core:**
- React Native (latest stable)
- TypeScript
- React Navigation

**Platform Support:**
- iOS (iPhone and iPad)
- Android (phones and tablets)
- Cross-platform code sharing with platform-specific optimizations

**Flexible (agents will ask):**
- State Management: Context API, Redux, Zustand, or MobX
- UI Libraries: React Native Paper (Material), Elements, or custom
- Testing: Jest, React Native Testing Library, Detox

## Project Structure

The agents will guide you to create:

```
your-app/
├── src/
│   ├── components/     # Reusable components
│   ├── screens/        # Screen components
│   ├── navigation/     # Navigation configuration
│   ├── services/       # API and external services
│   ├── store/          # State management
│   ├── utils/          # Utility functions
│   └── types/          # TypeScript definitions
├── ios/                # iOS native project (Xcode workspace)
├── android/            # Android native project (Gradle)
├── __tests__/          # Test files
├── metro.config.js     # Metro bundler configuration
├── babel.config.js     # Babel configuration
├── package.json        # Dependencies and scripts
├── tsconfig.json       # TypeScript configuration
├── index.js            # App entry point
└── docs/
    ├── prd.md          # Product requirements
    ├── architecture.md # Technical architecture
    └── design/         # Design assets
```

## Common Workflows

### Creating a New Screen
```
*mobile-sm create-story "User Authentication Screen"
*mobile-dev implement
```

### Optimizing Performance
```
*mobile-dev optimize FlatList
*mobile-architect review performance
```

### Preparing for Store Release
```
*mobile-sm release-plan
*mobile-dev prepare-release
```

## Best Practices

1. **Always start with planning** - Create PRD and Architecture first
2. **Test on real devices** - Simulators/emulators are good, real devices are better
3. **Profile performance early** - Don't wait until the end
4. **Follow platform guidelines** - Respect iOS HIG and Material Design conventions
5. **Design for offline** - Apps should work without connectivity
6. **Consider both platforms early** - Design for shared components with platform-specific touches

## Requirements

**For iOS Development:**
- Node.js 20+
- Xcode 15+
- macOS
- iOS Simulator

**For Android Development:**
- Node.js 20+
- Android Studio
- Android SDK
- Android Emulator or device

**For Both:**
- React Native development environment setup

## Support

This expansion pack is part of BMad-Method. For issues or questions:
- [BMad Discord](https://discord.gg/gk8jAdXWmj)
- [GitHub Issues](https://github.com/bmadcode/bmad-method/issues)

## Future Enhancements

Active development continues on this expansion pack. For planned features and development roadmap, see [PLANNING.md](PLANNING.md#next-steps).

---

*Built with ❤️ in Superior, CO*