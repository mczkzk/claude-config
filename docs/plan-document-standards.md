# Plan Document Management Standards

**Comprehensive guide for creating, updating, and managing plan documents in todos/ directory.**

---

## 🏗️ Planning Process

### Investigation Phase
1. **Codebase Investigation**: Search for existing patterns and reusable components
2. **Architecture Analysis**: Ensure consistency with existing codebase
3. **Database Design Review**: Apply @docs/database-design.md principles - investigate existing schema, validate external data structures, and plan migrations carefully
4. **Methodology Integration**: Follow @docs/methodology.md TDD and refactoring standards
5. **Task Breakdown**: Structure implementation in Test → Code → Refactor cycles

### Plan Creation Workflow
1. **Requirements Analysis**: Extract and structure requirements from conversations, images, specs
2. **Feature Identification**: Identify core features and user stories
3. **Constraint Analysis**: Identify technical requirements and limitations
4. **Plan Document Generation**: Create structured plan following template standards

---

## 📂 File Management

### Plan File Location
- **Active Plans**: `todos/YYYY-MM-DD-[feature-name].md`
- **Archived Plans**: `todos/archived/YYYY-MM-DD-[feature-name].md` (moved when no longer active)

### Lifecycle Management
- **Planning & Implementation**: Same file, updated as needed during development
- **Plan Updates**: Direct content rewrite through natural conversation
- **Archiving**: Manual move to `todos/archived/` when no longer active (completed, cancelled, or superseded)
- **No Complex Tracking**: Minimal state tracking during planning phase

---

## 📋 Plan Document Format

### Standard Template Structure

Plan documents should follow this structure:

```
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
```

---

## 📊 Progress Tracking Standards

### Immediate Updates Required
**After completing each task:**
1. **TodoWrite**: Mark task as "completed" immediately
2. **Plan Document**: Update checkbox `[ ]` → `[x]` immediately
3. **Implementation Log**: Record any discoveries or changes

### Progress Indicators
Use consistent emoji indicators:
- 🔴 **RED Phase** - Writing failing tests
- 🟢 **GREEN Phase** - Making tests pass
- 🔵 **REFACTOR Phase** - Improving code quality
- ✅ **COMPLETED** - Task/feature completed
- ⚠️ **BLOCKED** - Task blocked, needs attention

### Example Progress Update
```markdown
## Implementation Plan
- [x] 🔴 Write failing test for user authentication ✅
- [x] 🟢 Implement basic login functionality ✅
- [ ] 🔵 Refactor authentication service
- [ ] 🔴 Add password validation tests
```

---

## 📝 Command Documentation Guidelines

### When to Document Commands
**Document these types of commands:**
- Complex test commands with filters or specific options
- Build commands with special flags
- Database migration commands
- Deployment commands with multiple steps
- Any command that took time to figure out

**Don't document these:**
- Basic commands like `npm run test`, `npm start`
- Standard git commands
- Simple file operations

### Documentation Format

Plan documents should include a Commands Reference section like this:

```markdown
## Commands Reference
```

#### Testing Commands
```bash
# Run specific test suites
npm run test --filter="{auth|payment}"

# Run integration tests with staging data
npm run test:integration --env=staging --verbose
```

#### Database Commands
```bash
# Run migrations with specific environment
npm run migrate:up --env=development

# Rollback last 2 migrations
npm run migrate:down --steps=2
```

### Location in Plan Documents
Add command documentation in a dedicated section within each plan document, not as separate files.

---

## 📈 Implementation Logging

### Learning Discovery Log
When implementing, document:
- **Unexpected API behaviors**
- **Workarounds for complex issues**
- **Performance insights**
- **Integration quirks**

### Format
```markdown
## Implementation Notes

### 2025-06-27 - Authentication Integration
- **Discovery**: External API returns different data structure than documented
- **Solution**: Added data transformation layer in `src/utils/api-transform.js`
- **Impact**: All future API integrations should use this pattern

### 2025-06-27 - Database Performance
- **Issue**: Query performance degraded with large datasets
- **Solution**: Added composite index on (user_id, created_at)
- **Command**: `CREATE INDEX idx_user_created ON activities(user_id, created_at);`
```

---

## 🔄 Plan Updates During Implementation

### When to Update Plans
- **Scope Changes**: User requests additional features
- **Technical Discoveries**: Implementation reveals new requirements
- **Architecture Changes**: Better patterns discovered during implementation

### Update Process
1. **Update Requirements**: Add/modify requirement items
2. **Update File Changes**: Add newly discovered files
3. **Update Implementation Plan**: Add/modify tasks as needed
4. **Continue Implementation**: No need to restart, just continue with updated plan

### Example Update
```markdown
<!-- Original plan -->
- [ ] Add user profile page

<!-- Updated during implementation -->
- [ ] Add user profile page
- [ ] Add profile image upload (added during implementation)
- [ ] Add profile validation (discovered requirement)
```

---

## 🎯 Quality Standards

### Plan Document Checklist
Before starting implementation:
- [ ] Requirements are specific and testable
- [ ] File changes are comprehensive
- [ ] Test cases are defined
- [ ] Commands are documented if complex
- [ ] Risks are identified

### During Implementation
- [ ] Progress is updated immediately after each task
- [ ] New discoveries are logged
- [ ] Plan is updated when scope changes
- [ ] Commands are documented when discovered

### Completion Standards
- [ ] All checkboxes are marked complete
- [ ] Implementation notes are comprehensive
- [ ] Lessons learned are documented
- [ ] Plan document remains in `todos/` for manual review and archiving to `todos/archived/`

---

## 🔄 TDD Implementation Workflow

### Implementation Cycle
Follow @docs/methodology.md principles with these specific practices:

1. **🔴 RED**: Write test + create minimal failing implementation (intentionally wrong)
2. **🟢 GREEN**: Fix implementation to make tests pass (minimal change)  
3. **🔵 REFACTOR**: Improve code quality while keeping tests green

### Implementation Guidelines
- Write test logic BEFORE implementation logic
- Begin with the simplest test case possible
- Write only enough code to pass the current test
- Use triangulation when implementation seems hardcoded

### Example Implementation Flow
```
→ "🔴 Writing test + minimal failing implementation..."
  ✅ Test written: expect('1') for input 1
  ✅ Failing implementation: return $num; (returns int, not string)
  ✅ Test fails as expected (correct RED)
→ "🟢 Fixing implementation to pass test..."
  ✅ Fixed: return (string)$num; (correct GREEN)
→ "🔴 Adding triangulation test for different input..."
  ✅ New test case fails (correct RED)
→ "🟢 Generalizing implementation to handle multiple cases..."
  ✅ All tests pass (correct GREEN)
→ "🔵 Refactoring for better design..."
  ✅ Tests still pass after refactoring
```

---

## 🚀 Integration with Development Workflow

### With /plan Command
- Plan documents follow this template automatically
- Focus on comprehensive upfront planning
- Template ensures consistency across all plans

### With Natural Language Implementation
- Use "この計画を実装して" or select from `/plan --list`
- Progress tracking follows same standards as structured commands
- TDD phases are clearly marked with emoji indicators
- Implementation log is maintained throughout development

### With Regular Development
- Use same documentation standards for consistency
- Apply same progress tracking methodology
- Maintain same quality standards regardless of development approach

---

**Remember**: Comprehensive plan documentation during implementation saves multiples of that time in future development and maintenance.