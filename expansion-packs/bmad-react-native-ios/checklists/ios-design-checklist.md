# iOS Design Compliance Checklist

## iOS Human Interface Guidelines Compliance

### Visual Design Fundamentals
- [ ] Clarity: Interface elements are clear and easy to understand
- [ ] Deference: UI defers to content, avoiding unnecessary ornamentation
- [ ] Depth: Visual layers and realistic motion provide hierarchy and vitality
- [ ] Consistent use of iOS system fonts (SF Pro, SF Compact, SF Mono)
- [ ] Proper color contrast ratios for accessibility (4.5:1 for normal text, 3:1 for large text)
- [ ] Support for both light and dark appearance modes

### Layout and Spacing
- [ ] Safe area respected on all screens (especially iPhone X+ devices)
- [ ] Consistent margins and padding following iOS spacing guidelines
- [ ] 44x44 point minimum touch target size for all interactive elements
- [ ] Proper spacing between interactive elements to prevent accidental taps
- [ ] Layout adapts gracefully to different screen sizes (iPhone, iPhone Plus, iPhone Pro Max)
- [ ] Dynamic Type support for text scaling accessibility

### Navigation Patterns
- [ ] Navigation follows iOS conventions (navigation controller, tab bar, modal presentation)
- [ ] Back button behavior matches iOS standards
- [ ] Navigation bar title placement and styling correct
- [ ] Tab bar follows iOS guidelines (2-5 tabs, appropriate icons)
- [ ] Modal presentation used appropriately (full screen, page sheet, form sheet)
- [ ] Search interface follows iOS search patterns

### Typography
- [ ] SF Pro Display/Text used appropriately for text hierarchy
- [ ] Text styles follow iOS size and weight guidelines
- [ ] Line height and character spacing optimized for readability
- [ ] Dynamic Type supported for accessibility
- [ ] Text truncation handled gracefully with proper ellipsis
- [ ] Proper text color for light/dark modes

### Color and Visual Style
- [ ] iOS system colors used where appropriate
- [ ] Custom colors work well in both light and dark modes
- [ ] Color semantics follow iOS conventions (red for destructive, blue for primary actions)
- [ ] Sufficient contrast for text readability
- [ ] Color is not the only way to convey information (accessibility)
- [ ] Consistent color palette throughout the app

## Component-Specific Guidelines

### Buttons and Controls
- [ ] Button styles follow iOS conventions (filled, plain, tinted)
- [ ] Destructive actions use appropriate red styling
- [ ] Button text uses title case
- [ ] Loading states show iOS-style activity indicators
- [ ] Switch controls follow iOS toggle patterns
- [ ] Slider and stepper controls use iOS styling

### Lists and Tables
- [ ] Table view cells follow iOS height and padding guidelines
- [ ] Section headers styled appropriately
- [ ] Disclosure indicators used correctly
- [ ] Swipe actions follow iOS patterns
- [ ] Selection states provide proper visual feedback
- [ ] Empty states designed with helpful messaging

### Forms and Input
- [ ] Text fields use iOS styling and behavior
- [ ] Keyboard types appropriate for input content
- [ ] Form validation follows iOS patterns
- [ ] Picker views use iOS wheel style
- [ ] Action sheets for multiple choice options
- [ ] Alerts follow iOS message and button conventions

### Navigation and Modals
- [ ] Navigation bar height and styling correct
- [ ] Large title behavior appropriate for content
- [ ] Modal presentation style fits content and purpose
- [ ] Sheet presentation uses proper corner radius and shadows
- [ ] Action sheets presented from correct anchor points
- [ ] Page control used for horizontal paging

## Interaction Design

### Touch and Gestures
- [ ] Tap targets meet minimum 44x44 point requirement
- [ ] Gesture conflicts avoided or properly prioritized
- [ ] Pull-to-refresh implemented where appropriate
- [ ] Swipe gestures follow iOS conventions
- [ ] Long press actions provide immediate feedback
- [ ] Pinch and zoom gestures work smoothly

### Animations and Transitions
- [ ] Screen transitions follow iOS timing and easing
- [ ] Loading animations use iOS system indicators
- [ ] Micro-interactions provide appropriate feedback
- [ ] Reduced motion accessibility respected
- [ ] Animation performance maintains 60fps
- [ ] Spring animations use iOS-appropriate parameters

### Feedback and States
- [ ] Haptic feedback used appropriately (selection, impact, notification)
- [ ] Visual feedback immediate for user interactions
- [ ] Loading states prevent user confusion
- [ ] Error states provide clear, actionable messages
- [ ] Success feedback appropriate and non-intrusive
- [ ] Empty states include helpful guidance

## Accessibility Compliance

### VoiceOver Support
- [ ] All interactive elements have accessibility labels
- [ ] Accessibility hints provided where helpful
- [ ] Accessibility traits correctly assigned
- [ ] Reading order logical and intuitive
- [ ] Custom controls properly implement accessibility protocols
- [ ] Images have descriptive alternative text

### Visual Accessibility
- [ ] Dynamic Type support implemented
- [ ] Sufficient color contrast in all states
- [ ] Color not sole indicator of information
- [ ] Reduce Motion preferences respected
- [ ] High Contrast mode considerations
- [ ] Button Shapes preference supported

### Motor Accessibility
- [ ] AssistiveTouch compatibility verified
- [ ] Voice Control labels appropriate
- [ ] Switch Control navigation possible
- [ ] Minimum touch target sizes maintained
- [ ] Timeout considerations for users with disabilities

## Platform Integration

### iOS-Specific Features
- [ ] Shortcuts app integration considered
- [ ] Spotlight search integration if appropriate
- [ ] Share sheet implementation follows conventions
- [ ] Context menus use iOS 13+ patterns
- [ ] Widget design follows WidgetKit guidelines (if applicable)
- [ ] App Clips considerations (if applicable)

### System Integration
- [ ] Status bar style appropriate for content
- [ ] Control Center integration if relevant
- [ ] Notification design follows iOS patterns
- [ ] Background app refresh behavior appropriate
- [ ] Handoff and Continuity support considered
- [ ] Keyboard shortcuts for external keyboards

## App Store and Marketing

### App Icon Design
- [ ] App icon follows iOS design guidelines
- [ ] Icon works at all required sizes
- [ ] No iOS interface elements in icon
- [ ] Icon distinctive and memorable
- [ ] Icon appropriate for target audience
- [ ] Alternative app icons considered (if feature is used)

### Launch and Onboarding
- [ ] Launch screen follows iOS guidelines
- [ ] Onboarding respects user time and attention
- [ ] Permission requests include clear rationale
- [ ] Progressive disclosure of features
- [ ] Skip options provided where appropriate
- [ ] Onboarding can be revisited if needed

### Screenshots and Preview
- [ ] App Store screenshots show actual app content
- [ ] Screenshots highlight key features effectively
- [ ] Preview video follows App Store guidelines
- [ ] Localized screenshots for international markets
- [ ] Screenshots updated with app changes

## Technical Design Considerations

### Performance Design
- [ ] 60fps maintained during all animations
- [ ] Images optimized for different screen densities
- [ ] Launch time minimized through design decisions
- [ ] Memory usage considered in visual complexity
- [ ] Network-dependent content has loading states
- [ ] Offline states designed appropriately

### Responsive Design
- [ ] Layout adapts to all iPhone screen sizes
- [ ] iPad layout consideration (if universal app)
- [ ] Landscape orientation handled gracefully
- [ ] Multitasking scenarios considered
- [ ] Split view and slide over compatibility (iPad)
- [ ] External display support if relevant

### Dark Mode Design
- [ ] All screens work in both light and dark modes
- [ ] Colors have appropriate dark mode variants
- [ ] Images have dark mode alternatives if needed
- [ ] Text remains readable in both modes
- [ ] Interface elements maintain proper contrast
- [ ] Semantic colors used appropriately

---

**Completion Criteria**: All applicable checklist items must be verified before design handoff to development. Items marked as not applicable should be documented with reasoning.