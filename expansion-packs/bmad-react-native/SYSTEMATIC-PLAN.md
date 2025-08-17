# BMad React Native Expansion Pack - Systematic Development Plan

## Overview

This document provides a complete, systematic plan for developing the BMad React Native expansion pack. It incorporates lessons learned from previous development attempts and follows proven patterns from existing expansion packs.

## Key Principles Learned

### 1. Follow Established Patterns
- **BMad Core**: 12 templates, lean and focused
- **Game Expansion**: 5 templates, adapts core patterns
- **Mobile Expansion**: Should be similar scale, 4-6 templates max

### 2. Don't Over-Engineer
- Use existing core templates where possible (PRD, architecture)
- Only create mobile-specific templates when truly needed
- Tasks are for processes, templates are for documents
- Agents reference templates, breaking references breaks the system

### 3. Build Up, Don't Tear Down
- Start with clean bmad-core foundation
- Add components systematically
- Verify dependencies before any deletions
- Test integration at each step

## Reference Materials

### Existing Work (bmad-react-native-old/)
Our previous work contains valuable components to adapt:

**Completed Agents (10 total):**
- mobile-analyst.md
- mobile-pm.md
- mobile-po.md
- mobile-architect.md
- mobile-dev.md
- mobile-ux.md
- mobile-sm.md
- mobile-qa.md
- mobile-master.md
- mobile-orchestrator.md

**Completed Tasks (13 total):**
- app-store-submission.md
- cross-platform-analysis.md
- mobile-analytics-setup.md
- mobile-architecture-design.md
- mobile-competitive-analysis.md
- mobile-feature-prioritization.md
- mobile-kb-mode-interaction.md
- mobile-performance-optimization.md
- mobile-story-refinement.md
- mobile-testing-strategy.md
- mobile-user-research.md
- mobile-workflow-coordination.md
- create-mobile-story.md

**Completed Workflows (6 total):**
- app-store-submission.yaml
- cross-platform-migration.yaml
- mobile-brownfield-enhancement.yaml
- mobile-greenfield-app.yaml
- mobile-performance-optimization.yaml
- mobile-testing-automation.yaml

**Valid Templates Created:**
- mobile-brief-tmpl.yaml (adapts core project-brief)
- mobile-architecture-tmpl.yaml (mobile-specific)
- mobile-story-tmpl.yaml (adapts core story)
- app-store-listing-tmpl.yaml (mobile-specific)

**Data Files (9 total):**
- android-guidelines.md
- bmad-kb.md
- cross-platform-testing-pitfalls.md
- ios-guidelines.md
- mobile-best-practices-2025.md
- mobile-troubleshooting.md
- performance-monitoring-setup.md
- react-native-patterns.md
- react-native-vs-expo-decision-framework.md

**Checklists (6 total):**
- app-store-submission-checklist.md
- mobile-architect-checklist.md
- mobile-design-checklist.md
- mobile-dev-checklist.md
- mobile-qa-checklist.md
- mobile-story-checklist.md

### Pattern References
- **BMad Core**: `/bmad-core/` - Base patterns for agents, tasks, templates
- **Game Expansion**: `/expansion-packs/bmad-2d-phaser-game-dev/` - Proven expansion pattern

## Systematic Implementation Plan

**CRITICAL RULE**: Stop after each phase and wait for manual approval before proceeding to next phase.

### Phase 1: Foundation Setup
**Goal**: Establish basic expansion pack structure and configuration

#### Step 1.1: Create Basic Config
- [ ] Create `config.yaml` with expansion pack metadata
- [ ] Follow game expansion pattern for structure
- [ ] Set `slashPrefix: ReactNative` for clean agent naming
- [ ] Initially reference core agents only (test if they work with mobile data)

#### Step 1.2: Verify Structure
- [ ] Ensure all required folders exist: `tasks/`, `templates/`, `workflows/`, `data/`, `checklists/`
- [ ] Test that structure matches BMad expectations
- [ ] **Note**: May not need `agents/` folder if core agents work

**STOP**: Wait for approval before Phase 2

### Phase 2: Mobile-Specific Data Files (Priority: High)
**Goal**: Create mobile knowledge that core agents can use

#### Step 2.1: Platform Guidelines
- [ ] `ios-guidelines.md` - iOS Human Interface Guidelines summary
- [ ] `android-guidelines.md` - Material Design guidelines summary
- [ ] `mobile-best-practices-2025.md` - Current mobile development best practices

#### Step 2.2: Technical References
- [ ] `react-native-patterns.md` - React Native development patterns
- [ ] `performance-monitoring-setup.md` - Mobile performance monitoring
- [ ] `cross-platform-testing-pitfalls.md` - Common cross-platform issues

#### Step 2.3: Decision Support
- [ ] `react-native-vs-expo-decision-framework.md` - Technology selection guide
- [ ] `mobile-troubleshooting.md` - Common mobile development issues

#### Step 2.4: Knowledge Base
- [ ] `bmad-kb.md` - Mobile-specific knowledge base integration

**Validation**: Test that core `dev.md` agent can access and use these mobile data files

**STOP**: Wait for approval before Phase 3

### Phase 3: Essential Templates (Priority: Medium)
**Goal**: Test if core templates work, only create mobile-specific ones if needed

#### Step 3.1: Test Core Templates First
- [ ] Test if core `project-brief-tmpl.yaml` works for mobile projects
- [ ] Test if core `story-tmpl.yaml` works for mobile stories  
- [ ] Test if core `prd-tmpl.yaml` works for mobile PRDs
- [ ] Test if core `architecture-tmpl.yaml` works for mobile architecture

#### Step 3.2: Create Mobile Templates Only If Needed
- [ ] `mobile-architecture-tmpl.yaml` - Only if core architecture template lacks mobile-specific sections (iOS/Android, React Native, app stores)
- [ ] `app-store-listing-tmpl.yaml` - Truly mobile-unique (no core equivalent)

**Key Principle**: Only create if core template is insufficient for mobile needs

**Validation**: Test template loading and ensure agents can reference them

**STOP**: Wait for approval before Phase 4

### Phase 4: Mobile-Specific Tasks (Priority: High)
**Goal**: Create tasks for truly mobile-specific processes

#### Step 4.1: Mobile-Unique Tasks (No Core Equivalent)
- [ ] `app-store-submission.md` - iOS App Store and Google Play submission process
- [ ] `cross-platform-analysis.md` - React Native iOS/Android implementation analysis

#### Step 4.2: Mobile-Adapted Tasks (Core Tasks Don't Cover Mobile Specifics)
- [ ] `mobile-competitive-analysis.md` - Mobile app competitive analysis (vs generic competitor analysis)
- [ ] `mobile-user-research.md` - Mobile user research methodology (vs generic user research)
- [ ] `mobile-performance-optimization.md` - Mobile-specific performance optimization

#### Step 4.3: Test If These Are Actually Needed
- [ ] Test if core `create-story.md` works for mobile stories (vs `create-mobile-story.md`)
- [ ] Test if core architecture tasks work for mobile (vs `mobile-architecture-design.md`)

**Key Principle**: Only create tasks for processes that are fundamentally different in mobile context

**Validation**: Ensure core agents can execute these tasks with mobile data files

**STOP**: Wait for approval before Phase 5

### Phase 5: Custom Agents (Priority: Low - Only If Needed)
**Goal**: Create agents only if core agents + mobile data/tasks are insufficient

#### Step 5.1: Test Core Agent Sufficiency First
- [ ] Test core `dev.md` + mobile data files for mobile development
- [ ] Test core `pm.md` + mobile data files for mobile product management  
- [ ] Test core `architect.md` + mobile data files for mobile architecture

#### Step 5.2: Create Mobile Agents Only If Core Agents Are Insufficient
- [ ] `mobile-master.md` - Only if needed for mobile-specific orchestration
- [ ] Mobile specialist agents - Only if core agents can't handle mobile workflows

**Key Principle**: Core agents + mobile data/tasks should be sufficient. Only create new agents if absolutely necessary.

**STOP**: Wait for approval before Phase 6

### Phase 6: Workflows (Priority: Medium)
**Goal**: Create complete mobile development workflows

#### Step 6.1: Essential Mobile Workflows
- [ ] `mobile-greenfield-app.yaml` - New React Native app development
- [ ] `app-store-submission.yaml` - Complete app store deployment

#### Step 6.2: Advanced Mobile Workflows (Only If Needed)
- [ ] `mobile-brownfield-enhancement.yaml` - Existing app improvement
- [ ] `cross-platform-migration.yaml` - Platform migration workflow

**Validation**: Test workflow execution with core agents

**STOP**: Wait for approval before Phase 7

### Phase 7: Quality Checklists (Priority: Low)
**Goal**: Create mobile-specific checklists only if core checklists are insufficient

#### Step 7.1: Test Core Checklists First
- [ ] Test if core checklists work for mobile development
- [ ] Identify mobile-specific quality gates not covered by core

#### Step 7.2: Create Mobile Checklists Only If Needed
- [ ] `app-store-submission-checklist.md` - Truly mobile-unique checklist
- [ ] Mobile-specific quality gates - Only if core checklists don't cover mobile needs

**STOP**: Wait for approval before Phase 8

### Phase 8: Documentation (Priority: Low)
**Goal**: Complete expansion pack documentation

#### Step 8.1: Update Core Documentation
- [ ] Update `config.yaml` with final configuration
- [ ] Update `README.md` to document what's included and how to use

#### Step 8.2: Usage Documentation
- [ ] Document how core agents + mobile data files work together
- [ ] Create mobile development workflow examples
- [ ] Document any mobile-specific components created

**STOP**: Expansion pack complete!

## Implementation Rules

### DO:
1. **Test core components first** - Always try core agents/templates/tasks before creating new ones
2. **Stop after each phase** - Wait for manual approval before proceeding
3. **Create only when necessary** - If core works, use core
4. **Start with data files** - Mobile-specific knowledge that core agents can use
5. **Test incrementally** - Validate each component works with core system
6. **Think critically** - Ask "Do we really need this, or does core handle it?"

### DON'T:
1. **Create without testing core first** - Always validate core insufficiency before creating new
2. **Copy game expansion blindly** - Just because game expansion has it doesn't mean we need it
3. **Over-engineer** - Core + mobile data files should handle most needs
4. **Continue without approval** - Stop and wait after each phase
5. **Create mobile versions of everything** - Most core components should work fine
6. **Rush the process** - Test thoroughly at each step

## Validation Checklist

### After Each Phase:
- [ ] All file references resolve correctly
- [ ] No broken agent dependencies
- [ ] Config.yaml lists all agents correctly
- [ ] Templates load without errors
- [ ] Tasks can be executed
- [ ] Workflows can be instantiated

### Before Completion:
- [ ] All agents load successfully
- [ ] All templates render correctly
- [ ] All tasks execute without missing dependencies
- [ ] All workflows can be started
- [ ] Installation process works
- [ ] Example usage scenarios work
- [ ] Documentation is complete and accurate

## Recovery Instructions

If development gets off track:
1. **Stop immediately** - Don't continue making changes
2. **Backup current state** - Preserve any valuable work
3. **Return to this plan** - Use this document as the definitive guide
4. **Start from clean bmad-core** - Begin with fresh foundation
5. **Follow phases systematically** - Don't skip steps or rush
6. **Validate each step** - Test before proceeding

## Success Criteria

The expansion pack is complete when:
- [ ] All agents work without dependency errors
- [ ] Core mobile workflows function end-to-end
- [ ] Installation process is smooth and documented
- [ ] Expansion pack follows established BMad patterns
- [ ] Template count is reasonable (4-6, like game expansion)
- [ ] Dev agents are lean and performant
- [ ] Documentation is comprehensive and accurate

## Notes for Future Sessions

- This plan is the source of truth for development approach
- Reference bmad-react-native-old/ for completed components
- Always validate dependencies before making changes
- Follow the phases in order for best results
- Keep the expansion pack lean and focused like the game expansion

---

**Remember**: Systematic development beats fast and broken. Follow this plan, and the expansion pack will be robust and maintainable.