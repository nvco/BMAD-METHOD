# BMad React Native iOS Knowledge Base

## Expansion Pack Overview

This knowledge base contains essential information for React Native iOS development using the BMad-Method framework.

## Core Concepts

### React Native Development
React Native enables building native iOS apps using JavaScript and React. Key concepts:
- **JavaScript Bridge**: Communication between JS and native iOS code
- **Metro Bundler**: Development server and JavaScript bundler
- **Native Modules**: Custom iOS functionality integration
- **Hot Reloading**: Live code updates during development

### iOS App Development
iOS-specific considerations for React Native apps:
- **Human Interface Guidelines**: Apple's design standards
- **App Store Review Guidelines**: Submission requirements
- **Xcode Integration**: iOS build and debugging tools
- **CocoaPods**: Dependency management for native iOS libraries

## Agent Roles and Responsibilities

### Mobile Architect (Maxwell)
- **Primary Focus**: System design and technology selection
- **Key Skills**: React Native architecture patterns, performance optimization
- **Deliverables**: Architecture documents, technology decision records
- **Collaboration**: Works with mobile-ux on design system architecture

### Mobile Developer (Morgan)
- **Primary Focus**: Feature implementation and optimization
- **Key Skills**: React Native components, iOS debugging, performance tuning
- **Deliverables**: Implemented features, tests, performance optimizations
- **Collaboration**: Implements designs from mobile-ux, follows architecture from mobile-architect

### Mobile UX Designer (Riley)
- **Primary Focus**: iOS-compliant user experience design
- **Key Skills**: iOS Human Interface Guidelines, accessibility, mobile interaction patterns
- **Deliverables**: UX specifications, design systems, accessibility guidelines
- **Collaboration**: Provides implementation specs to mobile-dev

### Mobile Scrum Master (Casey)
- **Primary Focus**: Story creation and development workflow
- **Key Skills**: Agile methodology, mobile development estimation, cross-team coordination
- **Deliverables**: User stories, sprint plans, progress tracking
- **Collaboration**: Coordinates all team members, tracks dependencies

## Development Workflow

### Planning Phase
1. **Requirements Gathering**: Understand user needs and business goals
2. **Architecture Design**: Select technology stack and design system architecture
3. **UX Design**: Create iOS-compliant interface specifications
4. **Story Creation**: Break down features into implementable stories

### Development Phase
1. **Story Implementation**: Develop features according to specifications
2. **Testing**: Unit, integration, and manual testing
3. **Code Review**: Quality assurance and knowledge sharing
4. **Performance Optimization**: Ensure 60fps and responsive user experience

### Release Phase
1. **Testing**: Comprehensive testing on iOS devices
2. **App Store Preparation**: Compliance check and asset preparation
3. **Deployment**: TestFlight beta and App Store submission
4. **Monitoring**: Performance monitoring and crash reporting

## Technology Stack

### Core Technologies
- **React Native**: Cross-platform mobile framework
- **TypeScript**: Type-safe JavaScript development
- **React Navigation**: Navigation library for React Native
- **Metro**: JavaScript bundler for React Native

### State Management Options
- **Context API**: Built-in React state management (simple apps)
- **Redux Toolkit**: Predictable state container (complex apps)
- **Zustand**: Lightweight state management (medium apps)
- **MobX**: Reactive state management (specific use cases)

### UI Libraries
- **React Native Paper**: Material Design components
- **React Native Elements**: Customizable component library
- **NativeBase**: Modular and accessible component library
- **Custom Components**: Fully customized brand-specific UI

### Development Tools
- **Flipper**: Desktop debugging platform
- **React DevTools**: Component hierarchy and performance debugging
- **Xcode**: iOS development environment
- **iOS Simulator**: iOS device simulation for testing

## Best Practices

### Code Organization
```
src/
├── components/     # Reusable UI components
├── screens/        # Screen-level components
├── navigation/     # Navigation configuration
├── services/       # API and external services
├── store/          # State management
├── utils/          # Utility functions
├── hooks/          # Custom React hooks
├── types/          # TypeScript definitions
└── constants/      # App constants
```

### Performance Guidelines
- **60fps Target**: Maintain smooth animations and interactions
- **Memory Management**: Prevent memory leaks and excessive usage
- **Bundle Optimization**: Minimize app size and startup time
- **Network Efficiency**: Optimize API calls and data loading

### iOS Compliance
- **Human Interface Guidelines**: Follow Apple's design standards
- **Accessibility**: Support VoiceOver and dynamic type
- **App Store Guidelines**: Ensure submission compliance
- **Platform Integration**: Use iOS-specific features appropriately

## Common Patterns

### Component Creation
```typescript
// Functional component with TypeScript
interface ButtonProps {
  title: string;
  onPress: () => void;
  disabled?: boolean;
}

const Button: React.FC<ButtonProps> = ({ title, onPress, disabled = false }) => {
  return (
    <TouchableOpacity onPress={onPress} disabled={disabled}>
      <Text>{title}</Text>
    </TouchableOpacity>
  );
};
```

### State Management
```typescript
// Context API for simple state
const AppContext = createContext<AppContextType | undefined>(undefined);

export const AppProvider: React.FC<{ children: React.ReactNode }> = ({ children }) => {
  const [state, setState] = useState(initialState);
  return (
    <AppContext.Provider value={{ state, setState }}>
      {children}
    </AppContext.Provider>
  );
};
```

### Navigation Setup
```typescript
// Stack navigator with TypeScript
type RootStackParamList = {
  Home: undefined;
  Profile: { userId: string };
};

const Stack = createNativeStackNavigator<RootStackParamList>();

export const AppNavigator = () => (
  <NavigationContainer>
    <Stack.Navigator>
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Profile" component={ProfileScreen} />
    </Stack.Navigator>
  </NavigationContainer>
);
```

## Troubleshooting

### Common Issues
- **Metro bundler cache**: Clear with `npx react-native start --reset-cache`
- **iOS simulator problems**: Reset simulator or restart Xcode
- **Native module issues**: Reinstall CocoaPods with `cd ios && pod install`
- **Performance issues**: Use React DevTools Profiler to identify bottlenecks

### Debugging Tools
- **Console.log**: Basic debugging (remove in production)
- **Flipper**: Network requests, state inspection, layout debugging
- **React DevTools**: Component performance profiling
- **Xcode Console**: Native iOS debugging and crash logs

## Resources

### Documentation
- [React Native Docs](https://reactnative.dev/)
- [iOS Human Interface Guidelines](https://developer.apple.com/design/human-interface-guidelines/)
- [App Store Review Guidelines](https://developer.apple.com/app-store/review/guidelines/)

### Tools and Libraries
- [React Navigation](https://reactnavigation.org/)
- [Redux Toolkit](https://redux-toolkit.js.org/)
- [React Native Testing Library](https://callstack.github.io/react-native-testing-library/)
- [Flipper](https://fbflipper.com/)

### Community
- [React Native Community](https://github.com/react-native-community)
- [iOS Developer Forums](https://developer.apple.com/forums/)
- [BMad Method Discord](https://discord.gg/gk8jAdXWmj)

This knowledge base serves as the foundation for effective React Native iOS development using BMad-Method principles and practices.