# Create Mobile Story Task

## Overview
This task creates comprehensive user stories for React Native iOS development with complete implementation context.

## Prerequisites
- PRD document available and sharded
- Architecture document available and sharded
- UX specifications available (if applicable)
- Previous story implementation notes reviewed

## Task Steps

### Step 1: Review Context Documents
1. **Read Sharded PRD Section**
   - Understand the feature requirements
   - Identify user goals and business value
   - Note any constraints or dependencies

2. **Review Architecture Decisions**
   - Extract relevant technical patterns
   - Identify state management approach
   - Note performance requirements
   - Check native module requirements

3. **Check UX Specifications**
   - Review screen designs if available
   - Note interaction patterns
   - Identify accessibility requirements
   - Check iOS compliance needs

### Step 2: Analyze Implementation Context
1. **Review Previous Stories**
   - Check implementation notes from completed stories
   - Identify established patterns in the codebase
   - Note any technical debt or improvement opportunities
   - Review performance lessons learned

2. **Identify Dependencies**
   - List required third-party packages
   - Check for native module dependencies
   - Identify API endpoints needed
   - Note any shared components required

3. **Assess Complexity**
   - Evaluate React Native complexity and implementation approach
   - Consider iOS-specific requirements
   - Factor in testing requirements
   - Account for performance optimization needs

### Step 3: Write User Story
Create story following this structure:

```markdown
## Story: [Descriptive Title]
**ID**: [STORY-XXX]
**Epic**: [Parent Epic Name]

### User Story
As a [specific user type]
I want [specific functionality]
So that [specific business value]

### Technical Context
**Architecture Pattern**: [Pattern from architecture doc]
**State Management**: [Context/Redux/Zustand approach]
**Navigation**: [How feature integrates with app navigation]
**Dependencies**: [Required npm packages]
**Native Modules**: [Any native functionality needed]

### UX Specifications
**Screens**: [List of screens involved]
**Components**: [UI components to create/modify]
**Interactions**: [Touch gestures, animations]
**Designs**: [Reference to mockups if available]
**iOS Compliance**: [Specific HIG requirements]

### Acceptance Criteria
- [ ] [Specific, testable criterion 1]
- [ ] [Specific, testable criterion 2]
- [ ] Performance: [60fps, startup time, memory usage]
- [ ] Accessibility: [VoiceOver support, Dynamic Type]
- [ ] iOS Compatibility: [iOS versions supported]
- [ ] Device Testing: [iPhone sizes to test]

### Implementation Notes
**Suggested Approach**:
1. [Step-by-step implementation plan]
2. [Key files to create/modify]
3. [Testing strategy]

**Gotchas**:
- [iOS-specific considerations]
- [Performance optimization needs]
- [Common pitfalls to avoid]

**Code Patterns**:
- [Reference to established patterns in codebase]
- [Architectural decisions from previous stories]

### Testing Requirements
- Unit tests for [specific components/logic]
- Integration tests for [workflows]
- Manual testing on [iOS simulator requirements]
- Edge cases: [specific scenarios to verify]

### Definition of Done
- [ ] Code complete with TypeScript
- [ ] Unit tests passing (>80% coverage)
- [ ] Tested on iOS simulator
- [ ] Code reviewed and approved
- [ ] Documentation updated
- [ ] No console errors/warnings
- [ ] Performance validated (60fps)
- [ ] Accessibility tested with VoiceOver
```

### Step 4: Add Mobile-Specific Context

1. **iOS Integration Details**
   - Specify iOS-specific components needed
   - Note any native iOS APIs required
   - Document permission requirements
   - Specify iOS version compatibility

2. **Performance Considerations**
   - Set specific performance targets
   - Note memory usage expectations
   - Specify animation requirements (60fps)
   - Document bundle size impact

3. **React Native Specifics**
   - Identify platform-specific code needs (.ios.tsx files)
   - Note Metro bundler considerations
   - Specify debugging approach
   - Document any bridge performance considerations

### Step 5: Validate Story Completeness

Use the mobile story checklist to ensure:
- [ ] All technical context is complete
- [ ] Acceptance criteria are testable
- [ ] Implementation guidance is sufficient
- [ ] Dependencies are identified
- [ ] Testing requirements are comprehensive
- [ ] iOS compliance is addressed

### Step 6: Story Estimation

Consider these factors for complexity assessment:

**1 Point (Simple)**:
- Basic UI component creation
- Simple state updates
- No native modules
- Minimal testing required

**Moderate Complexity**:
- Screen with multiple components
- API integration
- Navigation updates
- Standard testing requirements

**Complex Implementation**:
- Multiple screens with navigation
- Complex state management
- Third-party integrations
- Performance optimization required

**Very Complex Implementation**:
- Native module integration
- Complex animations
- Extensive testing requirements
- Multiple iOS-specific features

### Step 7: Implementation Readiness Check

Before marking story as ready:
1. **Technical Feasibility Confirmed**
   - All dependencies available
   - Architecture decisions documented
   - No blocking technical unknowns

2. **Design Clarity**
   - UX specifications complete
   - Interaction patterns defined
   - iOS compliance validated

3. **Development Context**
   - Implementation approach clear
   - Code patterns established
   - Testing strategy defined

## Deliverables

1. **Complete Story Document**
   - Formatted according to template
   - All sections completed
   - Technical context comprehensive

2. **Estimation and Priority**
   - Complexity assessment completed
   - Sprint priority noted
   - Dependencies mapped

3. **Implementation Plan**
   - Development approach documented
   - Testing strategy defined
   - Review requirements specified

## Quality Checks

- [ ] Story follows established template format
- [ ] All acceptance criteria are testable
- [ ] Technical context enables autonomous development
- [ ] iOS-specific requirements are documented
- [ ] Performance expectations are clear
- [ ] Testing requirements are comprehensive
- [ ] Dependencies and blockers are identified
- [ ] Estimation reflects true complexity

## Success Criteria

Story is considered complete when:
- Mobile developer can implement without additional requirements gathering
- All architectural context is embedded in the story
- Testing approach is clearly defined
- iOS compliance requirements are documented
- Performance targets are specific and measurable

## Common Patterns

### API Integration Story Pattern
```markdown
### Technical Context
**API Integration**: [Endpoint details]
**Error Handling**: [Retry logic, user feedback]
**Caching**: [AsyncStorage/cache strategy]
**Offline Support**: [Cached data fallback]
```

### Navigation Story Pattern
```markdown
### Technical Context
**Navigation Type**: [Stack/Tab/Modal]
**Parameters**: [TypeScript parameter types]
**Transitions**: [Animation specifications]
**Deep Linking**: [URL scheme if applicable]
```

### Performance Story Pattern
```markdown
### Acceptance Criteria
- [ ] 60fps during all animations
- [ ] < 3 second app startup impact
- [ ] < 50MB memory usage increase
- [ ] Smooth scrolling with 1000+ items
```

This task ensures that every story contains complete context for efficient React Native iOS development while maintaining BMad Method's quality standards.