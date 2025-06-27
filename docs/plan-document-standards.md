# Plan Document Progress Management

**Guide for updating and managing plan documents during implementation.**

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

### Implementation Notes Format
Document discoveries in plan documents:

```markdown
## Implementation Notes

### 2025-06-27 - API Integration
- **Discovery**: External API returns different structure than documented
- **Solution**: Added transformation layer in `src/utils/api-transform.js`
- **Command**: `npm run test:api -- --verbose` (for debugging)
```

### Commands Reference Format
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

**Remember**: Comprehensive plan documentation during implementation saves multiples of that time in future development and maintenance.