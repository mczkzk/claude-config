---
description: Create plan document for structured development
allowed-tools:
  - Task
  - Read
  - Glob
  - Grep
  - Write
  - LS
---

# Plan Build Command

Creates detailed plan documents from completed plan-search investigations.

## Usage

```
/plan-build [feature-name]
# Creates plan document for specific feature (requires completed plan-search)

/plan-build
# Creates plan document when feature-name is contextually obvious
```

## Command Execution Steps

1. 🔍 **Find Plan Search**: 
   - If feature-name provided: Look for `plans/[feature-name]-search.md` file
   - If no feature-name: Search `plans/` directory for `*-search.md` files (excluding `archive/` subdirectory) and identify from context
2. ✅ **STRICT Completion Verification**: 
   - Search file for `- [ ]` patterns using grep or manual scan
   - If ANY unchecked items found → STOP, return error message
   - Verify status shows "✅ Investigation completed" 
   - Only proceed if 100% verified complete
3. 🔎 **Verification Command**: Run `grep '\- \[ \]' "plans/[feature-name]-search.md"` to confirm zero results
4. 📝 **Create Plan Document**: Generate `plans/[feature-name].md` using template below ONLY after verification passes
5. 📋 **Populate Content**: Use plan-search investigation findings to fill plan sections
6. 🔍 **MANDATORY Section Completeness Verification**: 
   - Count sections in generated plan document
   - MUST contain exactly 10 sections
   - Run verification command: `grep -c "^## " "plans/[feature-name].md"`
   - Expected result: Exactly 10 sections
   - Verify each required section header is present:
     * 📄 Requirements Summary
     * 🏗️ Architecture Impact
     * 📁 File Changes
     * 🧪 Testing Strategy
     * 📋 Implementation Plan
     * ⚠️ Risk Assessment
     * 📚 Reference Documentation
     * ⌨️ Commands Reference
     * 📝 Implementation Notes
     * 📖 PLAN DOCUMENT OPERATION GUIDE
   - If count ≠ 10 or any section missing → STOP, return error, regenerate missing sections

## Plan Creation Workflow

1. **Database Design Review**: Apply @docs/database-design.md principles for schema changes
2. **Methodology Integration**: Follow @docs/methodology.md TDD and refactoring standards
3. **Task Breakdown**: Structure implementation in Test → Code → Refactor cycles
4. **Plan Document Generation**: Create structured plan following template below

## Plan Document Template

```markdown
# [Feature Name] - Development Plan

**STRICT IMPLEMENTATION PROTOCOL**:

Before marking ANY implementation task complete:
✓ Evidence documented in Implementation Notes with specific details (code snippets, test results, file paths)
✓ Can answer "How do you know this works?" for this task
✓ Implementation Notes contain proof of functionality (test output, screenshots, working code)
✓ Next person reading notes can verify your implementation

**Rule: If Implementation Notes don't prove the task completion, uncheck the box**

**INCREMENTAL COMPLETION PROTOCOL**:
✓ Mark tasks complete ONE AT A TIME as you finish each implementation step
✓ Update checkboxes [ ] → [x] immediately when task is verified complete
✓ Do NOT batch multiple completions - check boxes individually upon completion
✓ Record implementation evidence in Implementation Notes before marking checkbox complete

---

## 📄 Requirements Summary
- [ ] Feature requirement 1
- [ ] Feature requirement 2
- [ ] Feature requirement 3

## 🏗️ Architecture Impact
- **Affected Components**: List of components that will be modified
- **Integration Points**: How this feature connects with existing systems
- **Dependencies**: External libraries, APIs, or services required

## 📁 File Changes

### Modified Files
- `src/component1.js` - Add new functionality
- `src/component2.js` - Update existing method
- `tests/component1.test.js` - Add test cases

### New Files
- `src/features/new-feature.js` - Core implementation
- `src/features/new-feature.test.js` - Test suite

## 🧪 Testing Strategy
### Test Cases (TDD)
1. **Basic functionality test**
   - Input: [specific input]
   - Expected: [expected output]
   
2. **Edge case test**
   - Input: [edge case input]
   - Expected: [expected behavior]

## 📋 Implementation Plan

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

## ⚠️ Risk Assessment
- **Technical Risks**: Potential technical challenges
- **Dependencies**: External dependency risks
- **Mitigation**: Strategies to address identified risks

## 📚 Reference Documentation
- **TDD**: @docs/development/tdd.md (Test-Driven Development principles)
- **Refactoring**: @docs/development/refactoring.md (code improvement techniques)
- **Database Design**: @docs/development/database-design.md (schema design, migration guidelines)
- **Production Safety**: @docs/development/production-safety.md (environment safety protocol, incident prevention)

## ⌨️ Commands Reference

### Category Name
Command description
*command here*

## 📝 Implementation Notes
Record ALL discoveries that impact development - BE COMPREHENSIVE! Include technical details, code snippets, command outputs, error solutions, performance insights, useful patterns, shortcuts, unsolved issues, failed approaches, and any knowledge that helps future implementation. Document complete context to preserve knowledge across sessions.

*Record here*

**Remember**: Comprehensive plan documentation during implementation saves multiples of that time in future development and maintenance.

---

## 📖 PLAN DOCUMENT OPERATION GUIDE

### Progress Tracking
**Update Plan Documents:**
- Update checkbox [ ] → [x] ONE AT A TIME when completing each individual task
- Mark TodoWrite tasks as "completed" immediately after finishing each task
- Record discoveries and changes in Implementation Notes before checking boxes
- Never batch multiple checkbox updates - complete tasks incrementally

### Plan Updates During Implementation
**Plans can evolve during implementation:**
- Add new tasks when requirements change
- Update phases when better patterns are discovered
- Modify scope based on user feedback or technical discoveries

### TDD Implementation
Follow @docs/development/tdd.md for Red-Green-Refactor cycles:
- 🔴 **RED**: Write failing test
- 🟢 **GREEN**: Make test pass  
- 🔵 **REFACTOR**: Improve code quality

Note: 🔴🟢🔵 appear in terminal during implementation, not in plan documents

---

**Status**: ✅ Ready for implementation
**Next Step**: Begin implementation using plan document
```

## Key Principles

- **Plan Search Required**: Must have completed `[feature-name]-search.md` before planning
- **Strict Verification**: Never trust status alone - verify actual checkbox states
- **Investigation-Based**: Uses investigation findings to create plan document
- **Template-Driven**: Ensures consistency across all plan documents
- **Section Completeness**: Generated plan MUST contain exactly 10 template sections
- **Automatic Verification**: Command automatically checks section count and headers
- **Fail-Safe Regeneration**: Incomplete plans trigger error and regeneration
- **Implementation-Ready**: Creates actionable tasks for development