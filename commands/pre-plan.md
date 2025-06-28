---
description: Create investigation checklist before planning implementation
allowed-tools:
  - Read
  - Write
  - Glob
  - Grep
  - LS
  - Task
---

# Pre-Planning Investigation Command

Creates investigation checklist and gathers requirements before implementation planning.

## Usage

```
/pre-plan [feature-name]
# Creates investigation checklist and starts requirements gathering
```

## Command Flow

### 1. Create Investigation File
- Generate `plans/[feature-name]-pre-plan.md`
- Include comprehensive investigation checklist
- All items must be completed before `/plan` command

### 2. Requirements Gathering
Prompt user to provide:
- **Specifications**: Technical requirements, user stories
- **Screenshots**: UI mockups, design references
- **Context**: Background information, constraints
- **Examples**: Similar features, reference implementations

### 3. Interactive Investigation
Guide user through checklist completion:
- Codebase analysis
- Database investigation
- External dependencies validation
- Technical requirements clarification

## Investigation Checklist Template

```markdown
# Pre-Planning Investigation - [Feature Name]

## 📋 Requirements Gathering
- [ ] **Specifications provided**: Technical requirements documented
- [ ] **UI/UX materials**: Screenshots, mockups, design references shared
- [ ] **User stories**: Clear understanding of user needs
- [ ] **Constraints identified**: Technical, business, or timeline limitations
- [ ] **Success criteria defined**: Clear definition of completion

## 🔍 Codebase Analysis  
- [ ] **Similar features identified**: Existing patterns and implementations found
- [ ] **Reusable components**: Available components and utilities documented
- [ ] **Code conventions**: Naming patterns and architecture styles understood
- [ ] **Integration points**: How feature connects with existing system

## 🗄️ Database Investigation
- [ ] **Current schema mapped**: Existing tables, columns, relationships, and constraints documented
- [ ] **Data patterns sampled**: Actual data examined to understand structure and volume
- [ ] **Similar features analyzed**: How existing features handle data storage and relationships
- [ ] **Domain rules identified**: Business constraints and validation requirements documented
- [ ] **External data verified**: Third-party API responses logged and data structures confirmed
- [ ] **Migration approach planned**: Backward compatibility, rollback strategy, and deployment approach defined
- [ ] **Performance considerations**: Index requirements and query patterns evaluated
- [ ] **Anti-patterns avoided**: No assumptions without verification, no copy-paste patterns without analysis

## 🔗 External Dependencies
- [ ] **APIs validated**: Third-party service responses verified with real data
- [ ] **Package compatibility**: Library versions and capabilities confirmed
- [ ] **Integration testing**: External service behavior documented
- [ ] **Error handling**: Failure scenarios and fallbacks identified

## ⚡ Technical Validation
- [ ] **Performance requirements**: Load, speed, and scalability needs defined
- [ ] **Security considerations**: Authentication, authorization, data protection
- [ ] **Testing strategy**: Unit, integration, and end-to-end test approach
- [ ] **Deployment approach**: How feature will be released and monitored

## 📝 Investigation Notes

*Record key discoveries, decisions, and findings during investigation - BE DETAILED. Include specific technical details, version numbers, performance metrics, constraints discovered through testing or conversation. Document architectural decisions with rationale and alternatives considered. List any unresolved questions that need clarification. This preserves context that may be lost due to token limits.*

---

**Status**: ⚠️ Investigation in progress
**Next Step**: Complete all checklist items, then run `/plan [feature-name]`
```

## Final Verification Before Status Update

**CRITICAL**: Before marking investigation as completed, perform these verification steps:

1. **Checklist Audit**: Read through ALL checklist items line by line
2. **Unchecked Items Check**: Search for `- [ ]` patterns in the file using grep or manual scan
3. **Status Logic**: Only mark completed if ZERO unchecked items exist
4. **Double Confirmation**: Re-read investigation notes to ensure completeness
5. **Verification Command**: Run `grep '\- \[ \]' "[filename]"` to confirm no unchecked items

**If ANY unchecked items remain**: Keep status as "⚠️ Investigation in progress"

## Key Principles

- **Investigation First**: No planning without thorough investigation
- **Interactive Process**: Engage with user to gather all necessary information
- **Comprehensive Coverage**: All technical aspects must be explored
- **Documentation Focus**: Record findings for future reference
- **Blocking Mechanism**: `/plan` command checks for completed pre-plan
- **Strict Verification**: Never mark complete without 100% verification

## Integration with Planning

- `/plan [feature-name]` requires completed `[feature-name]-pre-plan.md`
- All checklist items must be marked `[x]` 
- Investigation findings inform detailed planning
- Pre-plan serves as foundation for implementation design