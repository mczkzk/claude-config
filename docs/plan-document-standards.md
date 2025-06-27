# Plan Document Management Standards

**Guidelines for creating, updating, and maintaining implementation plan documents in todos/ directory.**

---

## 📋 Plan Document Format

### Standard Template Structure
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

### Test Command Documentation
```bash
# Standard test command
npm run test

# Complex test commands (document these)
npm run test --filter="{feature1|feature2}"
npm run test:integration --env=staging
```

## Implementation Plan
- [ ] 🔴 Write failing test for core functionality
- [ ] 🟢 Implement minimal solution to pass test
- [ ] 🔵 Refactor for better design
- [ ] 🔴 Add edge case tests
- [ ] 🟢 Handle edge cases
- [ ] 🔵 Final refactoring and optimization

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
```markdown
## Commands Reference

### Testing
```bash
# Run specific test suites
npm run test --filter="{auth|payment}"

# Run integration tests with staging data
npm run test:integration --env=staging --verbose
```

### Database
```bash
# Run migrations with specific environment
npm run migrate:up --env=development

# Rollback last 2 migrations
npm run migrate:down --steps=2
```
```

### Location in Plan Documents
Add command documentation in a dedicated section within each plan file, not as separate files.

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
- [ ] File remains in `todos/` for manual review and archiving

---

## 🚀 Integration with Development Workflow

### With /plan Command
- Plan documents follow this template automatically
- Focus on comprehensive upfront planning
- Template ensures consistency

### With /tdd Command
- Progress tracking happens automatically
- TDD phases are clearly marked
- Implementation log is maintained

### With Regular Development
- Use same documentation standards
- Apply same progress tracking
- Maintain same quality standards

---

**Remember**: Good plan documentation during implementation saves multiples of that time in future development and maintenance.