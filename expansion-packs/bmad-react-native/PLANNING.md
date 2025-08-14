# React Native Cross-Platform Expansion Pack - Planning Document

## Overview
This expansion pack extends BMad-Method for React Native cross-platform mobile app development, supporting both iOS and Android platforms.

## Agent Architecture

### Core Specialized Agents

#### 1. `mobile-architect`
**Purpose**: Extends base architect with cross-platform mobile architecture patterns
**Key Responsibilities**:
- React Native architecture patterns (Redux/Context/Zustand)
- iOS and Android-specific considerations (navigation, native modules)
- Performance optimization strategies for both platforms
- Data persistence strategies (AsyncStorage, Realm, SQLite)
- API integration patterns
- State management design
- Platform-specific code organization

#### 2. `mobile-dev`
**Purpose**: Implements React Native components and features for cross-platform deployment
**Key Responsibilities**:
- React Native component development
- iOS Simulator and Android Emulator management
- Native module integration (both platforms)
- Debugging with Flipper/React DevTools/Xcode/Android Studio
- Performance optimization implementation
- Testing implementation (unit, integration, E2E)

#### 3. `mobile-ux`
**Purpose**: Ensures cross-platform design compliance and mobile UX best practices
**Key Responsibilities**:
- iOS Human Interface Guidelines and Material Design compliance
- Mobile-first responsive design for both platforms
- Touch interactions and platform-specific gestures
- Platform-native UI patterns while maintaining consistency
- Cross-platform accessibility implementation
- App icon and splash screen design guidance
- **Design Input Handling**:
  - Work with provided mockups/screenshots
  - Reference design files in `/docs/design/` folder
  - Convert visual designs to platform-appropriate implementation specs
  - Ask for existing designs and target platforms during planning phase

#### 4. `mobile-sm`
**Purpose**: Creates cross-platform mobile user stories
**Key Responsibilities**:
- Cross-platform mobile story templates
- iOS and Android deployment considerations in stories
- App Store and Google Play submission requirements
- Breaking down mobile features into implementable tasks with platform awareness

### Future Agents (Not in Initial Release)

#### 5. `mobile-deployment` (Future Addition)
**Purpose**: Handles iOS deployment and release automation
**Key Responsibilities**:
- TestFlight setup and management
- App Store Connect configuration
- Provisioning profiles and certificates
- Release management
- App Store listing optimization
**Note**: For initial release, deployment guidance will be included in mobile-dev and mobile-sm agents

## Technology Stack

### Core Technologies
- **React Native**: Latest stable version
- **TypeScript**: For type safety
- **React Navigation**: Navigation library (recommended for all apps)

### Optional Technologies (Project-Specific)
- **State Management**: 
  - Simple apps: React Context API
  - Complex apps: Redux, Zustand, or MobX
- **UI Libraries**: 
  - React Native Paper (Material Design)
  - React Native Elements
  - NativeBase
  - Or custom styled components
- **Decision Point**: Agents will ask during PRD/Architecture phase

### Development Tools
- **IDE**: Cursor, VS Code, or any AI-assisted IDE for React Native development
- **Xcode**: iOS development, building, and simulator management
- **Metro**: JavaScript bundler
- **Flipper**: Debugging tool
- **React DevTools**: Component debugging
- **iOS Simulator**: Testing on various iPhone/iPad models

### Testing
- **Jest**: Unit and integration testing
- **React Native Testing Library**: Component testing
- **Detox** (optional): E2E testing

### Build & Deployment
- **Development**: Xcode + Metro bundler
- **Production**: Xcode Archive → App Store Connect
- **Future CI/CD**: Fastlane or EAS Build (optional)

## Workflow Integration

### Planning Phase
1. Analyst/PM create PRD with cross-platform mobile requirements
2. Mobile-UX creates platform-appropriate design specifications (iOS HIG/Material Design)
3. Mobile-Architect creates React Native cross-platform architecture
4. PO validates mobile requirements alignment for target platforms

### Development Phase
1. Mobile-SM creates React Native cross-platform stories with platform considerations
2. Mobile-Dev implements with iOS and Android considerations
3. QA reviews mobile-specific concerns for both platforms
4. Mobile-Deployment handles release (when needed for both App Store and Google Play)

## Key Considerations

### iOS Specific
- App Store Review Guidelines compliance
- iOS version support strategy
- Device compatibility (iPhone/iPad)
- Push notifications setup (APNs)
- Universal links configuration

### Android Specific
- Google Play Store policies compliance
- Android API level support strategy
- Device compatibility (phones/tablets)
- Push notifications setup (FCM)
- App links configuration
- Back button behavior handling

### React Native Cross-Platform
- Native module requirements for both platforms
- Platform-specific code organization (.ios.js/.android.js)
- Performance optimization priorities for both platforms
- Bundle size optimization
- Over-the-air updates strategy
- Shared component architecture vs platform-specific components

## Project Discovery Process

Each agent includes comprehensive discovery questions to ensure all project requirements are captured:

- **Mobile Architect**: Platform support, technical stack, and integration requirements
- **Mobile UX Designer**: Design approach, user experience, and accessibility needs  
- **Mobile Scrum Master**: Sprint planning, release strategy, and story requirements
- **Mobile Developer**: Implementation approach, testing strategy, and environment setup

*See individual agent files for complete discovery question sets.*

## Next Steps

### Completed ✅
1. Finalize agent roster (4 core agents: architect, dev, ux, sm)
2. Create agent markdown files with prompts (cross-platform aware)
3. Develop mobile-specific checklists (iOS and Android support)
4. Create story templates for common mobile features
5. Add React Native knowledge base (including Android guidelines)
6. Add MCP context7 integration for real-time documentation
7. Add structured discovery questions to all agents for comprehensive project planning

### Planned Development 🚧
8. **Add Mobile QA/Testing Agent** - Critical missing piece for comprehensive mobile development
   - Create `mobile-qa.md` agent file with cross-platform testing expertise
   - Include discovery questions for testing strategy, device coverage, platform-specific testing
   - Add to `config.yaml` agent roster
   - Create corresponding checklist in `checklists/mobile-qa-checklist.md`

9. **Implement docs/mobile/ Documentation Strategy**
   - Update `mobile-dev` agent to create `cross-platform-development-patterns.md` in user's `docs/mobile/` folder
   - Update `mobile-qa` agent to create `cross-platform-testing-pitfalls.md` in user's `docs/mobile/` folder
   - Configure both agents to use this folder for mobile-specific documentation
   - Document the pattern: standard BMad categories use existing docs folders, mobile-specific knowledge uses docs/mobile/

10. Test with sample project (create a simple cross-platform app)
11. Create CI/CD pipeline templates for both App Store and Google Play

### Future Enhancements 🔮
- Mobile deployment agent for automated releases
- React Native Web support
- Advanced native module development guidance
- Enhanced testing frameworks integration
- Performance monitoring and optimization tools

---

*This is a living document - update as decisions are made*