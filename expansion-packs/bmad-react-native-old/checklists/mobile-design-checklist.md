# Mobile Design Compliance Checklist

## Cross-Platform Design Guidelines Compliance

### Platform Selection
- [ ] Target platforms defined (iOS, Android, or both)
- [ ] Platform-specific design requirements understood
- [ ] Shared vs platform-specific components identified

## iOS Human Interface Guidelines Compliance

*(Complete this section if targeting iOS)*

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
- [ ] 44x44 point minimum touch target size for iOS (48x48dp for Android)
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
- [ ] Platform-appropriate fonts used (SF Pro for iOS, Roboto for Android)
- [ ] Text styles follow iOS size and weight guidelines
- [ ] Line height and character spacing optimized for readability
- [ ] Dynamic Type supported for accessibility
- [ ] Text truncation handled gracefully with proper ellipsis
- [ ] Proper text color for light/dark modes

### Color and Visual Style
- [ ] Platform system colors used where appropriate (iOS system colors, Material Design colors)
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

## Material Design Guidelines Compliance

*(Complete this section if targeting Android)*

### Material Design Fundamentals
- [ ] Material metaphor: surfaces, edges, and shadows provide visual cues
- [ ] Bold, graphic, intentional design with typography, grids, space, scale, color
- [ ] Motion provides meaning: animations are purposeful and focused
- [ ] Consistent use of Roboto font family
- [ ] Proper color contrast ratios for accessibility
- [ ] Support for both light and dark themes

### Android Layout and Spacing
- [ ] Edge-to-edge design with proper system bar handling
- [ ] Consistent margins and padding following Material Design guidelines
- [ ] 48x48dp minimum touch target size for all interactive elements
- [ ] Proper spacing between elements (8dp grid system)
- [ ] Layout adapts to different Android screen sizes and densities
- [ ] Font scaling accessibility support

### Material Navigation Patterns
- [ ] Navigation follows Material Design patterns (drawer, bottom nav, tabs)
- [ ] Back button behavior follows Android conventions
- [ ] App bar (toolbar) styling matches Material guidelines
- [ ] Bottom navigation bar follows Material guidelines (3-5 destinations)
- [ ] Navigation drawer used appropriately for 5+ destinations
- [ ] Floating Action Button (FAB) placement and usage

### Material Components
- [ ] Cards used appropriately for grouped content
- [ ] Chips for compact representations of input, attribute, or action
- [ ] Snackbars for brief messages about app processes
- [ ] Bottom sheets for additional options
- [ ] Material buttons with appropriate elevation and ripple effects
- [ ] Text fields follow Material Design patterns

## Platform Integration

### iOS-Specific Features
- [ ] Shortcuts app integration considered
- [ ] Spotlight search integration if appropriate
- [ ] Share sheet implementation follows conventions
- [ ] Context menus use iOS 13+ patterns
- [ ] Widget design follows WidgetKit guidelines (if applicable)
- [ ] App Clips considerations (if applicable)

### Android-Specific Features
- [ ] App shortcuts for launcher integration
- [ ] Android widgets considered (if applicable)
- [ ] Share sheet implementation follows Android patterns
- [ ] Context menus use Android patterns
- [ ] Notification channels properly configured
- [ ] Android Auto or Android TV support (if applicable)

### System Integration
- [ ] Status bar style appropriate for content (both platforms)
- [ ] Notification design follows platform patterns
- [ ] Background behavior appropriate for each platform
- [ ] Platform-specific integrations considered
- [ ] Keyboard shortcuts for external keyboards

## App Store and Google Play Marketing

### App Icon Design
- [ ] App icon follows platform design guidelines (iOS and/or Android)
- [ ] Icon works at all required sizes for target platforms
- [ ] No platform-specific interface elements in icon
- [ ] Icon distinctive and memorable
- [ ] Icon appropriate for target audience
- [ ] Alternative app icons considered (iOS feature)
- [ ] Adaptive icon support for Android (if targeting Android)

### Launch and Onboarding
- [ ] Launch screen follows iOS guidelines
- [ ] Onboarding respects user time and attention
- [ ] Permission requests include clear rationale
- [ ] Progressive disclosure of features
- [ ] Skip options provided where appropriate
- [ ] Onboarding can be revisited if needed

### Screenshots and Preview
- [ ] Store screenshots show actual app content (App Store and/or Google Play)
- [ ] Screenshots highlight key features effectively
- [ ] Preview video follows store guidelines
- [ ] Localized screenshots for international markets
- [ ] Screenshots updated with app changes
- [ ] Feature graphic created for Google Play (if targeting Android)

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

**Completion Criteria**: All applicable checklist items must be verified before design handoff to development. Items marked as not applicable should be documented with reasoning. For cross-platform apps, ensure both iOS and Android (Material Design) sections are completed as appropriate.