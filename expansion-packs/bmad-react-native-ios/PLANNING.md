# React Native iOS Expansion Pack - Planning Document

## Overview
This expansion pack extends BMad-Method for React Native iOS mobile app development.

## Agent Architecture

### Core Specialized Agents

#### 1. `mobile-architect`
**Purpose**: Extends base architect with mobile-specific architecture patterns
**Key Responsibilities**:
- React Native architecture patterns (Redux/Context/Zustand)
- iOS-specific considerations (navigation, native modules)
- Performance optimization strategies
- Data persistence strategies (AsyncStorage, Realm, SQLite)
- API integration patterns
- State management design

#### 2. `mobile-dev`
**Purpose**: Implements React Native components and features
**Key Responsibilities**:
- React Native component development
- iOS simulator management
- Native module integration
- Debugging with Flipper/React DevTools
- Performance optimization implementation
- Testing implementation

#### 3. `mobile-ux`
**Purpose**: Ensures iOS design compliance and mobile UX best practices
**Key Responsibilities**:
- iOS Human Interface Guidelines compliance
- Mobile-first responsive design
- Touch interactions and gestures
- Platform-specific UI patterns
- Accessibility implementation
- App icon and splash screen design guidance
- **Design Input Handling**:
  - Work with provided mockups/screenshots
  - Reference design files in `/docs/design/` folder
  - Convert visual designs to implementation specs
  - Ask for existing designs during planning phase

#### 4. `mobile-sm`
**Purpose**: Creates mobile-specific user stories
**Key Responsibilities**:
- Mobile-specific story templates
- iOS deployment considerations in stories
- App Store submission requirements
- Breaking down mobile features into implementable tasks

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
1. Analyst/PM create PRD with mobile-specific requirements
2. Mobile-UX creates iOS design specifications
3. Mobile-Architect creates React Native architecture
4. PO validates mobile requirements alignment

### Development Phase
1. Mobile-SM creates React Native specific stories
2. Mobile-Dev implements with iOS considerations
3. QA reviews mobile-specific concerns
4. Mobile-Deployment handles release (when needed)

## Key Considerations

### iOS Specific
- App Store Review Guidelines compliance
- iOS version support strategy
- Device compatibility (iPhone/iPad)
- Push notifications setup
- Deep linking configuration

### React Native Specific
- Native module requirements
- Platform-specific code organization
- Performance optimization priorities
- Bundle size optimization
- Over-the-air updates strategy

## Questions/Decisions Needed

- [ ] Minimum iOS version to support?
- [ ] iPad support required?
- [ ] Push notifications needed?
- [ ] Analytics requirements?
- [ ] Crash reporting service?
- [ ] State management preference?
- [ ] UI component library preference?
- [ ] Offline support requirements?

## Next Steps

1. Finalize agent roster
2. Create agent markdown files with prompts
3. Develop mobile-specific checklists
4. Create story templates for common mobile features
5. Add React Native knowledge base
6. Test with sample project

---

*This is a living document - update as decisions are made*