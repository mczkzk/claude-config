---
description: Create implementation plan for structured development
allowed-tools:
  - Task
  - Read
  - Glob
  - Grep
  - Write
  - LS
---

# Implementation Planning Command

Creates detailed implementation plans from completed pre-plan investigations.

## Usage

```
/plan [feature-name]
# Creates implementation plan for specific feature (requires completed pre-plan)
```

## Command Execution Steps

1. **Find Specific Pre-Plan**: Look for `todos/[feature-name]-pre-plan.md` file
2. **STRICT Completion Verification**: 
   - Search file for `- [ ]` patterns using grep or manual scan
   - If ANY unchecked items found → STOP, return error message
   - Verify status shows "✅ Investigation completed" 
   - Only proceed if 100% verified complete
3. **Verification Command**: Run `grep '\- \[ \]' "todos/[feature-name]-pre-plan.md"` to confirm zero results
4. **Create Plan Document**: Generate `todos/[feature-name].md` using template below ONLY after verification passes
5. **Populate Content**: Use pre-plan investigation findings to fill plan sections

## Plan Creation Workflow

1. **Database Design Review**: Apply @docs/database-design.md principles for schema changes
2. **Methodology Integration**: Follow @docs/methodology.md TDD and refactoring standards
3. **Task Breakdown**: Structure implementation in Test → Code → Refactor cycles
4. **Plan Document Generation**: Create structured plan following template below

## Plan Document Template

```markdown
# [Feature Name] - Implementation Plan

## Requirements Summary
- [ ] Feature requirement 1
- [ ] Feature requirement 2
- [ ] Feature requirement 3

## Architecture Impact
- **Affected Components**: List of components that will be modified
- **Integration Points**: How this feature connects with existing systems
- **Dependencies**: External libraries, APIs, or services required

## File Changes

### Modified Files
- `src/component1.js` - Add new functionality
- `src/component2.js` - Update existing method
- `tests/component1.test.js` - Add test cases

### New Files
- `src/features/new-feature.js` - Core implementation
- `src/features/new-feature.test.js` - Test suite

## Testing Strategy
### Test Cases (TDD)
1. **Basic functionality test**
   - Input: [specific input]
   - Expected: [expected output]
   
2. **Edge case test**
   - Input: [edge case input]
   - Expected: [expected behavior]

## Implementation Plan

### Phase A: [Descriptive Phase Name]
- [ ] **A.1** [Task description]
  - [ ] Specific subtask 1
  - [ ] Specific subtask 2
  - [ ] Test/validation step
- [ ] **A.2** [Another task]
  - [ ] Implementation details
  - [ ] Error handling
  - [ ] Unit tests

### Phase B: [Another Phase Name]  
- [ ] **B.1** [Task description]
  - [ ] Specific implementation
  - [ ] Integration steps
  - [ ] Testing

## Risk Assessment
- **Technical Risks**: Potential technical challenges
- **Dependencies**: External dependency risks
- **Mitigation**: Strategies to address identified risks

## Reference Documentation
- **Development Methodology**: @docs/methodology.md (TDD, refactoring principles)
- **Database Design**: @docs/database-design.md (schema design, migration guidelines)

## Commands Reference
*Document complex commands (not basic ones like npm test)*

### Category Name
*Command description*
command here

## Implementation Notes
*Record discoveries, decisions, and important findings during implementation - BE COMPREHENSIVE. Include specific technical details, code snippets, command outputs, error messages, and solutions. Document the complete context to preserve knowledge across sessions and token limits.*

### YYYY-MM-DD - Topic Name
*Record implementation discoveries, decisions, and important findings here*

**Remember**: Comprehensive plan documentation during implementation saves multiples of that time in future development and maintenance.

---

## 📖 PLAN DOCUMENT OPERATION GUIDE

### Progress Tracking
**Update Plan Documents:**
- Update checkbox [ ] → [x] when completing tasks
- Mark TodoWrite tasks as "completed" immediately
- Record discoveries and changes in Implementation Notes

### Plan Updates During Implementation
**Plans can evolve during implementation:**
- Add new tasks when requirements change
- Update phases when better patterns are discovered
- Modify scope based on user feedback or technical discoveries

### TDD Implementation
Follow @docs/methodology.md for Red-Green-Refactor cycles:
- 🔴 **RED**: Write failing test
- 🟢 **GREEN**: Make test pass  
- 🔵 **REFACTOR**: Improve code quality

Note: 🔴🟢🔵 appear in terminal during implementation, not in plan documents

---

**Status**: 📋 Ready for implementation
**Next Step**: Begin implementation using TDD methodology and update progress in this document
```


## Key Principles

- **Pre-Plan Required**: Must have completed `[feature-name]-pre-plan.md` before planning
- **Strict Verification**: Never trust status alone - verify actual checkbox states
- **Investigation-Based**: Uses investigation findings to create implementation design
- **Template-Driven**: Ensures consistency across all plan documents
- **Implementation-Ready**: Creates actionable tasks for development
- **Fail-Safe**: Stop immediately when verification fails