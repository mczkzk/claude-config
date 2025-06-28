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
2. **Verify Completion**: Ensure all checklist items are marked `[x]` in pre-plan file
3. **Create Plan Document**: Generate `todos/[feature-name].md` using template below
4. **Populate Content**: Use pre-plan investigation findings to fill plan sections

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

## Implementation Notes
*Record discoveries, decisions, and important findings during implementation - BE COMPREHENSIVE. Include specific technical details, code snippets, command outputs, error messages, and solutions. Document the complete context to preserve knowledge across sessions and token limits.*

---

# 📖 PLAN DOCUMENT OPERATION GUIDE

## Progress Tracking
**Update Plan Documents:**
- Update checkbox `[ ]` → `[x]` when completing tasks
- Mark TodoWrite tasks as "completed" immediately
- Record discoveries and changes in Implementation Notes

**Example:**

### Phase 1: Database Setup
- [x] Create migration file
- [x] Test migration up/down
- [ ] Add indexes (pending: performance analysis needed)

## TDD Implementation
Follow @docs/methodology.md for Red-Green-Refactor cycles:
- 🔴 **RED**: Write failing test
- 🟢 **GREEN**: Make test pass  
- 🔵 **REFACTOR**: Improve code quality

(Note: 🔴🟢🔵 appear in terminal during implementation, not in plan documents)

## Plan Updates During Implementation
Update plan documents when:
- User requests additional features
- Implementation reveals new requirements
- Better architecture patterns are discovered

Simply add new tasks to existing phases:

### Phase 1: User Profile
- [x] Basic profile page
- [ ] Profile validation (added during implementation)
- [ ] Image upload (new requirement)

## Implementation Notes Format
Document discoveries in plan documents - BE COMPREHENSIVE AND DETAILED:

## Implementation Notes

### 2025-06-28 - API Integration
- **Discovery**: External API returns different structure than documented
  - Expected: {user: {id, name, email}}
  - Actual: {data: {user_id, full_name, email_address, created_at}}
  - API version: v2.1.3, affects all user endpoints
- **Root Cause**: Documentation outdated, confirmed via support ticket #12345
- **Solution**: Added transformation layer in src/utils/api-transform.js
  - Maps field names: user_id → id, full_name → name, etc.
  - Handles both old and new formats for backward compatibility
- **Testing**: npm run test:api -- --verbose shows all 47 test cases passing
- **Performance**: Transformation adds ~2ms overhead, acceptable for non-critical path

## Commands Reference Format
Include complex commands in plan documents:

## Commands Reference

### Testing
# Run filtered tests
npm run test --filter="{auth|payment}"

### Database  
# Migration with specific env
npm run migrate:up --env=development

Don't document basic commands like `npm test` or `git commit`.

**Remember**: Comprehensive plan documentation during implementation saves multiples of that time in future development and maintenance.
```

## Key Principles

- **Pre-Plan Required**: Must have completed `[feature-name]-pre-plan.md` before planning
- **Investigation-Based**: Uses investigation findings to create implementation design
- **Template-Driven**: Ensures consistency across all plan documents
- **Implementation-Ready**: Creates actionable tasks for development