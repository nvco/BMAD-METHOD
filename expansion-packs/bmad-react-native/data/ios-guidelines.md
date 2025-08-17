# iOS Human Interface Guidelines Summary

## Core Design Principles

### Clarity
- **Clear Visual Communication**: Use clear, legible text, well-defined icons, and purposeful decorations
- **Minimize Cognitive Load**: Reduce the number of elements users need to process
- **Progressive Disclosure**: Show only essential options first, reveal details as needed
- **Consistent Visual Hierarchy**: Use size, color, and position to show importance

### Deference
- **Content First**: UI should support content, not compete with it
- **Minimal Decoration**: Use ornamentation sparingly and purposefully
- **Respect User Content**: Let user-generated content shine
- **Subtle Backgrounds**: Use neutral colors that don't interfere with content

### Depth
- **Layered Interface**: Use visual layers to show relationships and hierarchy
- **Realistic Motion**: Animations should feel natural and physics-based
- **Z-axis Thinking**: Consider how elements relate in 3D space
- **Purposeful Transitions**: Motion should guide users and provide feedback

## Visual Design

### Typography
- **System Fonts**: Use SF Pro Display for headlines, SF Pro Text for body text
- **Dynamic Type**: Support iOS Dynamic Type for accessibility
- **Text Hierarchy**: Use font weights and sizes to create clear information hierarchy
- **Line Height**: Maintain appropriate line spacing for readability

**Type Scale Guidelines**:
- Large Title: 34pt (SF Pro Display)
- Title 1: 28pt (SF Pro Display)
- Title 2: 22pt (SF Pro Display)
- Title 3: 20pt (SF Pro Display)
- Headline: 17pt (SF Pro Text Semibold)
- Body: 17pt (SF Pro Text Regular)
- Callout: 16pt (SF Pro Text Regular)
- Subhead: 15pt (SF Pro Text Regular)
- Footnote: 13pt (SF Pro Text Regular)
- Caption 1: 12pt (SF Pro Text Regular)
- Caption 2: 11pt (SF Pro Text Regular)

### Color
- **System Colors**: Use iOS system colors for consistency and dark mode support
- **Semantic Colors**: Colors should convey meaning (red for destructive, blue for primary)
- **Accessibility**: Maintain 4.5:1 contrast ratio for normal text, 3:1 for large text
- **Dark Mode**: Design for both light and dark appearances

**iOS System Colors**:
- Blue: #007AFF (Primary actions, links)
- Green: #34C759 (Success, positive actions)
- Indigo: #5856D6 (Alternative primary)
- Orange: #FF9500 (Warnings, secondary actions)
- Pink: #FF2D92 (Accent, highlights)
- Purple: #AF52DE (Creative, premium)
- Red: #FF3B30 (Destructive actions, errors)
- Teal: #5AC8FA (Calm, professional)
- Yellow: #FFCC00 (Attention, caution)

### Spacing and Layout
- **Safe Area**: Respect device safe areas (notch, home indicator)
- **Layout Margins**: Use standard 16pt margins on iPhone, 20pt on iPad
- **Touch Targets**: Minimum 44x44pt touch targets
- **Spacing**: Use 8pt grid system for consistent spacing

## Navigation

### Navigation Patterns
- **Tab Bar**: 3-5 top-level sections, bottom placement
- **Navigation Bar**: Hierarchical navigation with back button
- **Page Control**: For horizontal paging through content
- **Segmented Control**: For switching between related views

### Navigation Guidelines
- **Clear Hierarchy**: Users should always know where they are
- **Consistent Back Button**: Always provide a way to go back
- **Contextual Actions**: Place actions where users expect them
- **Search**: Make search prominent when content is searchable

## Input and Controls

### Common Controls
- **Buttons**: Clear, actionable labels with appropriate styles
- **Text Fields**: Single-line text input with clear placeholder text
- **Switches**: For binary on/off states
- **Sliders**: For selecting values from a range
- **Steppers**: For incrementing/decrementing values

### Touch Interactions
- **Tap**: Primary interaction method
- **Swipe**: For navigation or actions (delete, archive)
- **Long Press**: For contextual menus or additional options
- **Pinch**: For zooming content
- **Drag**: For reordering or moving content

## Platform-Specific Features

### iOS-Specific Patterns
- **Pull to Refresh**: Standard gesture for refreshing content
- **Swipe Actions**: Left/right swipe for quick actions
- **3D Touch/Haptic Touch**: Peek and pop interactions
- **Action Sheets**: Modal dialogs for choosing from options
- **Activity View**: For sharing content

### Accessibility
- **VoiceOver**: Screen reader support with proper labels
- **Dynamic Type**: Support for user font size preferences
- **Voice Control**: Navigation using voice commands
- **Switch Control**: Navigation using external switches
- **Reduce Motion**: Respect user preference for reduced animations

## React Native Implementation Notes

### iOS-Specific Components
```javascript
// Use platform-specific components when needed
import { ActionSheetIOS, Alert } from 'react-native';

// iOS-style alerts
Alert.alert('Title', 'Message', [
  { text: 'Cancel', style: 'cancel' },
  { text: 'OK', style: 'default' }
]);

// iOS Action Sheet
ActionSheetIOS.showActionSheetWithOptions(
  {
    options: ['Cancel', 'Option 1', 'Option 2'],
    cancelButtonIndex: 0,
  },
  (buttonIndex) => {
    // Handle selection
  }
);
```

### iOS Styling Considerations
```javascript
// Use iOS-appropriate styling
const styles = StyleSheet.create({
  iosButton: {
    backgroundColor: '#007AFF', // iOS blue
    borderRadius: 8,
    paddingVertical: 12,
    paddingHorizontal: 16,
  },
  iosText: {
    fontFamily: Platform.OS === 'ios' ? 'SF Pro Text' : 'System',
    fontSize: 17,
    lineHeight: 22,
  },
});
```

### Safe Area Handling
```javascript
import { SafeAreaView, SafeAreaProvider } from 'react-native-safe-area-context';

// Always wrap content in SafeAreaView for iOS
<SafeAreaView style={{ flex: 1 }}>
  <YourContent />
</SafeAreaView>
```

## Common iOS Pitfalls in React Native

1. **Ignoring Safe Areas**: Always account for notch and home indicator
2. **Wrong Font Rendering**: Test fonts on actual iOS devices
3. **Inconsistent Navigation**: Follow iOS navigation patterns
4. **Poor Touch Targets**: Ensure minimum 44pt touch areas
5. **Missing Haptic Feedback**: Use appropriate haptic feedback for actions
6. **Accessibility Oversights**: Test with VoiceOver enabled
7. **Color Issues**: Test in both light and dark mode
8. **Animation Performance**: Use native driver for smooth animations

## App Store Guidelines Compliance

### Design Requirements
- Follow Human Interface Guidelines consistently
- Support both light and dark mode
- Implement proper accessibility features
- Use appropriate app icon and launch screen

### Content Requirements
- Family-friendly content if targeting all ages
- Proper content warnings and age ratings
- Respect user privacy and data
- Follow App Store Review Guidelines

### Technical Requirements
- Support latest iOS versions (typically last 2-3 versions)
- Optimize for different screen sizes
- Handle network connectivity issues gracefully
- Implement proper error handling and user feedback