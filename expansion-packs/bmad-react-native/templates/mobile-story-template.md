# Mobile Story Template

## Story: [Feature Title]
**ID**: [STORY-XXX]
**Epic**: [Parent Epic Name]

### User Story
As a [specific user type: app user, premium subscriber, first-time user, etc.]
I want [specific functionality with mobile context]
So that [specific business value and user benefit]

### Technical Context
**Architecture Pattern**: [Reference to mobile-architect decisions]
**State Management**: [Context API/Redux/Zustand approach for this feature]
**Navigation**: [How feature integrates with existing navigation]
**Dependencies**: [Required npm packages and versions]
**Native Modules**: [Any iOS native functionality required]
**Platform Code**: [Any .ios.tsx files needed]

### UX Specifications
**Screens**: [List of screens involved in this story]
**Components**: [UI components to create or modify]
**Interactions**: [Touch gestures, animations, haptic feedback]
**Designs**: [Reference to design files in /docs/design/ if available]
**iOS Compliance**: [Specific Human Interface Guidelines requirements]
**Accessibility**: [VoiceOver labels, Dynamic Type support, etc.]
**Dark Mode**: [Light/dark mode considerations]

### Acceptance Criteria
- [ ] [Specific, testable functional requirement]
- [ ] [Another specific, measurable criterion]
- [ ] Performance: App maintains 60fps during [specific interactions]
- [ ] Performance: Feature loads in under [X] seconds
- [ ] Performance: Memory usage increase less than [X]MB
- [ ] Accessibility: All interactive elements have VoiceOver labels
- [ ] Accessibility: Supports Dynamic Type scaling
- [ ] iOS Compatibility: Works on iOS [minimum version] and above
- [ ] Device Testing: Tested on iPhone [specific models/sizes]
- [ ] Error Handling: Graceful handling of [specific error scenarios]
- [ ] Offline Support: [Behavior when network unavailable]

### Implementation Notes
**Suggested Approach**:
1. [Step 1: Specific implementation step with file names]
2. [Step 2: Next logical implementation step]
3. [Step 3: Testing and validation step]

**Key Files to Create/Modify**:
- `src/screens/[ScreenName].tsx` - [Purpose]
- `src/components/[ComponentName].tsx` - [Purpose]
- `src/services/[ServiceName].ts` - [Purpose]
- `src/types/[TypeName].ts` - [TypeScript definitions]

**Code Patterns to Follow**:
- [Reference to established patterns in codebase]
- [Architectural decisions from previous stories]
- [Component composition patterns to use]

**Gotchas and iOS-Specific Considerations**:
- [Known iOS-specific issues to watch for]
- [Performance optimization hints]
- [Common React Native pitfalls to avoid]
- [SafeAreaView considerations for different devices]

### Testing Requirements
**Unit Tests**:
- Test [specific component behavior]
- Test [utility functions/custom hooks]
- Test [API service functions]
- Minimum 80% code coverage for new code

**Integration Tests**:
- Test [complete user workflow]
- Test [API integration end-to-end]
- Test [navigation flow]

**Manual Testing Checklist**:
- [ ] Test on iOS Simulator (iPhone 14, iPhone SE)
- [ ] Test in both light and dark mode
- [ ] Test with VoiceOver enabled
- [ ] Test with large text sizes (Dynamic Type)
- [ ] Test on slow network conditions
- [ ] Test offline behavior
- [ ] Test memory usage with Xcode Instruments
- [ ] Test performance with React DevTools Profiler

**Edge Cases to Verify**:
- [Specific error scenarios]
- [Boundary conditions]
- [Network failure scenarios]
- [Device rotation if applicable]

### Performance Targets
- [ ] 60fps maintained during all animations and scrolling
- [ ] Screen loads in under 3 seconds on iPhone 8
- [ ] Memory usage increase less than 50MB
- [ ] Bundle size increase less than 500KB
- [ ] No memory leaks detected after feature usage
- [ ] Smooth performance on iOS minimum supported version

### Definition of Done
**Development Complete**:
- [ ] All acceptance criteria implemented and verified
- [ ] Code follows TypeScript strict mode requirements
- [ ] ESLint passes with no errors or warnings
- [ ] No console.log statements in production code
- [ ] Error handling implemented with user-friendly messages
- [ ] Performance targets met and verified

**Testing Complete**:
- [ ] Unit tests written and passing (>80% coverage)
- [ ] Integration tests passing
- [ ] Manual testing completed on iOS simulator
- [ ] Accessibility testing with VoiceOver completed
- [ ] Performance tested and meets targets
- [ ] Edge cases and error scenarios tested

**Code Review Ready**:
- [ ] Self-review completed
- [ ] Code properly documented with JSDoc comments
- [ ] Complex logic explained with inline comments
- [ ] Implementation notes provided for reviewers
- [ ] Any deviations from design documented
- [ ] Future improvement suggestions noted

**Quality Assurance**:
- [ ] No TypeScript errors
- [ ] No React Native warnings in console
- [ ] App starts and runs without crashes
- [ ] Feature works correctly in both light and dark modes
- [ ] Responsive layout verified on different screen sizes
- [ ] Network error handling verified
- [ ] Loading states implemented and tested

### Dependencies and Blockers
**Blocked By**:
- [ ] [Other story IDs that must be completed first]
- [ ] [API endpoints that must be available]
- [ ] [Design assets that must be provided]

**Dependencies**:
- [ ] [Required third-party packages]
- [ ] [Native module installations]
- [ ] [Environment configurations]

### Notes for QA Review
**Focus Areas for Review**:
- [Specific areas that need extra attention]
- [Complex logic that should be thoroughly tested]
- [Performance-critical sections]

**Known Limitations**:
- [Any known issues or limitations]
- [Future improvements planned]
- [Technical debt created (if any)]

---

**Story Status**: [Draft/Ready/In Progress/In Review/Done]
**Assigned To**: [Developer name]
**Sprint**: [Sprint number/name]
**Priority**: [High/Medium/Low]

### Implementation History
**Completed**: [Date when marked as done]
**Lessons Learned**: [Key insights for future similar stories]
**Performance Results**: [Actual vs target performance metrics]
**Future Improvements**: [Identified enhancement opportunities]