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
- Generate `todos/[feature-name]-pre-plan.md`
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

### Findings
*Record key discoveries during investigation - BE DETAILED. Include specific technical details, version numbers, performance metrics, constraints discovered through testing or conversation. This preserves context that may be lost due to token limits.*

### Decisions
*Document important architectural or design decisions made - BE SPECIFIC. Include rationale, alternatives considered, and technical justification. Record the "why" behind each decision to preserve reasoning for future reference.*

### Questions
*List unresolved questions that need clarification - PROVIDE CONTEXT. Include background information and why each question matters for implementation success.*

---

**Status**: ⚠️ Investigation in progress
**Next Step**: Complete all checklist items, then run `/plan [feature-name]`
```

## Key Principles

- **Investigation First**: No planning without thorough investigation
- **Interactive Process**: Engage with user to gather all necessary information
- **Comprehensive Coverage**: All technical aspects must be explored
- **Documentation Focus**: Record findings for future reference
- **Blocking Mechanism**: `/plan` command checks for completed pre-plan

## Integration with Planning

- `/plan [feature-name]` requires completed `[feature-name]-pre-plan.md`
- All checklist items must be marked `[x]` 
- Investigation findings inform detailed planning
- Pre-plan serves as foundation for implementation design