# BMad React Native Cross-Platform Expansion Pack

Transform your BMad-Method installation into a powerful React Native development team with specialized mobile agents for iOS and Android.

## Overview

This expansion pack extends BMad-Method with React Native cross-platform development expertise, providing specialized agents that understand mobile development patterns, iOS Human Interface Guidelines, Material Design, and React Native best practices.

## Features

- 🏗️ **Cross-Platform Architecture** - React Native system design optimized for iOS and Android
- ⚛️ **React Native Development** - Component implementation with TypeScript and performance focus
- 🎨 **Platform-Native UX Design** - iOS HIG and Material Design compliance with mobile-first approach
- 📋 **Mobile Sprint Management** - Story creation with complete cross-platform context
- 🗺️ **Platform Awareness** - Intelligent handling of iOS and Android differences

## Included Agents

### 1. Mobile Architect (Maxwell)
- React Native architecture patterns for cross-platform development
- State management selection (Redux, Zustand, Context)
- Performance optimization strategies for both platforms
- Native module integration planning (iOS and Android)
- Platform-specific architectural considerations

### 2. Mobile Developer (Morgan)
- React Native component implementation
- Cross-platform feature development (iOS and Android)
- Debugging with Flipper, React DevTools, Xcode, and Android Studio
- Performance profiling and optimization
- Testing with Jest and React Native Testing Library

### 3. Mobile UX Designer (Riley)
- iOS Human Interface Guidelines and Material Design expertise
- Mobile-first responsive design for both platforms
- Touch interactions and platform-specific gestures
- Cross-platform accessibility implementation
- Design to code specifications with platform awareness

### 4. Mobile Scrum Master (Casey)
- React Native story creation with platform considerations
- Mobile sprint planning for cross-platform development
- iOS and Android release cycle management
- App Store and Google Play submission coordination
- Complete cross-platform context in every story

## Installation

### Method 1: Package.json Installation (Recommended)

Add to your project's `package.json`:

```json
{
  "bmadExpansionPacks": [
    "bmad-react-native"
  ]
}
```

Then run:
```bash
npx bmad-method install
```

### Method 2: Manual Installation

Copy the expansion pack to your project:
```bash
cp -r expansion-packs/bmad-react-native /path/to/your/project/bmad-react-native
```

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
   *qa → Review and refactor code
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
├── ios/                # iOS-specific code
├── android/            # Android-specific code
├── __tests__/          # Test files
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

Planned additions:
- Mobile deployment agent for automated releases
- React Native Web support
- Expo integration options
- Enhanced CI/CD pipeline templates

---

*Built with ❤️ for the React Native community*