---
description: Execute test-driven development for structured implementation
allowed-tools:
  - Read
  - Write
  - Edit
  - MultiEdit
  - LS
  - Glob
  - Grep
  - Task
  - TodoWrite
  - TodoRead
  - Bash
---

# Test-Driven Development Command

Executes test-driven development process for plans created by /plan command.

## Usage

```
/tdd                    # Auto-detect plan from current session
/tdd feature-name       # Specify plan explicitly by name
```

## Command Scope

**This command handles**:
- Implementation of plans created by `/plan` command
- Plan updates during implementation
- Test-driven development cycle execution
- Progress tracking and task completion

**This command does NOT handle**:
- Direct implementation without plans (use regular workflow + TodoWrite)
- Planning phase (use `/plan` command)

## Implementation Process

### Plan Detection & Confirmation

**Auto-detection priority**:
1. Plans updated in current session
2. Plans matching current conversation context
3. Manual selection from existing plans

**File scanning**: Scan `todos/YYYY-MM-DD-*.md` files, exclude `todos/completed/`

**Smart confirmation**:
- Single clear candidate: "Implement [plan-name]? [Y/n]" → **WAIT for explicit user response**
- Multiple candidates: Present numbered selection → **WAIT for user selection**
- **CRITICAL**: Never proceed without explicit user confirmation

**Example**:
```
/tdd
→ "todos/2025-06-25-payment-system.md was updated this session. Implement? [Y/n]"
→ User: "Y" 
→ "Starting TDD implementation..."
```

### TDD Implementation Cycle
1. **🔴 RED**: Write test + create minimal failing implementation (intentionally wrong)
2. **🟢 GREEN**: Fix implementation to make tests pass (minimal change)
3. **🔵 REFACTOR**: Improve code quality while keeping tests green

**Implementation Guidelines**:
- Write test logic BEFORE implementation logic
- Begin with the simplest test case possible
- Write only enough code to pass the current test
- Use triangulation when implementation seems hardcoded

**Example flow**:
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

### Plan Updates During Implementation

**When implementation reveals plan changes needed**:
- User mentions: "Add mobile support to the plan", "Database optimization needed"
- Update File Changes list when new files are created or additional modifications needed
- Update plan content as needed
- Continue implementation with updated plan

### Progress Tracking

**Immediate Updates**:
- Mark TodoWrite tasks as "completed" right after finishing each task
- Update plan document checkboxes `[ ]` → `[x]` immediately after task completion
- Run lint/typecheck after major changes

**Test Command Documentation**:
- When discovering complex test commands during TDD cycles, document them in the plan file
- Simple commands like `npm run test` don't need documentation
- Complex commands with filters/options should be recorded for future reference
- Example: `npm run test --filter="{testFile1|testFile2}"` → add to plan's command section

**Progress Indicators**:
- 🔴 **RED Phase** → "🔴 Creating failing test for [feature]..."
- 🟢 **GREEN Phase** → "🟢 Implementing [feature] to pass test..."
- 🔵 **REFACTOR Phase** → "🔵 Refactoring [component] for better design..."
- ✅ **Completed** → "✅ [Feature] implementation complete"

### Implementation Completion

**When all implementation tasks are completed**:
- Mark all relevant checkboxes as complete
- Notify user of implementation completion
- Plan file remains in `todos/` for user review and manual archiving

## Key Principles

- **User Confirmation**: Never proceeds without explicit consent
- **Methodology Reference**: Follows @docs/methodology.md for TDD and refactoring standards