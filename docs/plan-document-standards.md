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
```

---

## 📊 Implementation & Progress Management

### Progress Tracking
**Update Plan Documents:**
- Update checkbox `[ ]` → `[x]` when completing tasks
- Mark TodoWrite tasks as "completed" immediately
- Record discoveries and changes in Implementation Notes

**Example:**
```markdown
### Phase 1: Database Setup
- [x] Create migration file
- [x] Test migration up/down
- [ ] Add indexes (pending: performance analysis needed)
```

### TDD Implementation
Follow @docs/methodology.md for Red-Green-Refactor cycles:
- 🔴 **RED**: Write failing test
- 🟢 **GREEN**: Make test pass  
- 🔵 **REFACTOR**: Improve code quality

(Note: 🔴🟢🔵 appear in terminal during implementation, not in plan documents)

### Plan Updates During Implementation
Update plan documents when:
- User requests additional features
- Implementation reveals new requirements
- Better architecture patterns are discovered

Simply add new tasks to existing phases:
```markdown
### Phase 1: User Profile
- [x] Basic profile page
- [ ] Profile validation (added during implementation)
- [ ] Image upload (new requirement)
```

### Implementation Notes
Document discoveries in plan documents:

```markdown
## Implementation Notes

### 2025-06-27 - API Integration
- **Discovery**: External API returns different structure than documented
- **Solution**: Added transformation layer in `src/utils/api-transform.js`
- **Command**: `npm run test:api -- --verbose` (for debugging)
```

### Command Documentation
Include complex commands in plan documents:

```markdown
## Commands Reference

### Testing
# Run filtered tests
npm run test --filter="{auth|payment}"

### Database  
# Migration with specific env
npm run migrate:up --env=development
```

Don't document basic commands like `npm test` or `git commit`.

---

## 🚀 Development Workflow Integration

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