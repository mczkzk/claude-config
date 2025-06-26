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

Executes **structured implementation** using test-driven development process. See CLAUDE.md for structured vs. ad-hoc development guidelines.

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
- Ad-hoc development (use regular workflow + TodoWrite)
- Simple bug fixes (direct implementation)
- Planning phase (use `/plan` command)

## Implementation Process

### 1. Plan Detection & Confirmation

**Auto-detection priority**:
1. Plans updated in current session
2. Plans matching current conversation context
3. Manual selection from existing plans

**Smart confirmation**:
- Single clear candidate: "Implement [plan-name]? [Y/n]" → **WAIT for explicit user response**
- Multiple candidates: Present numbered selection → **WAIT for user selection**
- **CRITICAL**: Never proceed without explicit user confirmation

### 2. TDD Implementation Cycle

#### ⚠️ CRITICAL: TEST-FIRST RULE
**Tests are the specification. Without tests first, specifications are unclear.**
- **NEVER create implementation files before tests exist**
- **ALWAYS start with test file creation**

#### Implementation Cycle (Strict Order)
1. **🔴 RED**: Write test first to define specification, create minimal stub that fails
2. **🟢 GREEN**: Write implementation to make tests pass
3. **🔵 REFACTOR**: Improve code quality while keeping tests green

#### Mandatory Test Execution Pattern
**EVERY TDD cycle MUST include these test runs**:
1. **After creating stub + test**: Confirm RED (test fails due to missing implementation)
2. **After initial implementation**: Confirm GREEN (all tests pass)  
3. **After refactoring**: Confirm tests still pass (no regression)

### 3. Plan Updates During Implementation

**When implementation reveals plan changes needed**:
- User mentions: "Add mobile support to the plan", "Database optimization needed"
- Update plan content as needed
- Continue implementation with updated plan

### 4. Progress Tracking

**Immediate Updates**:
- Mark TodoWrite tasks as "completed" right after finishing each task
- Update plan document checkboxes `[ ]` → `[x]` immediately after task completion
- Run lint/typecheck after major changes

**Progress Indicators**:
- 📋 **Planning** → "📋 Setting up [task]..."
- 🔴 **RED Phase** → "🔴 Creating failing test for [feature]..."
- 🟢 **GREEN Phase** → "🟢 Implementing [feature] to pass test..."
- 🔵 **REFACTOR Phase** → "🔵 Refactoring [component] for better design..."
- 🧪 **Testing** → "🧪 Running test suite..."
- ✅ **Completed** → "✅ [Feature] implementation complete"

### 5. Implementation Completion

**When all implementation tasks are completed**:
- Mark all relevant checkboxes as complete
- Notify user of implementation completion
- Plan file remains in `todos/` for user review and manual archiving

## Plan Detection Logic

### File Scanning
- Scan `todos/YYYY-MM-DD-*.md` files
- Exclude `todos/completed/` directory
- Prioritize files modified in current session

### Context Matching
- Files modified during current conversation session
- Topics mentioned in recent messages
- Explicit references to feature names

### Fallback Behavior
- **Never auto-execute without explicit user confirmation** 
- Always ask "Which plan?" when multiple candidates exist
- **If user doesn't respond**: Stop and wait, do not assume consent

## Examples

### Clear Context
```
/tdd
→ "todos/2025-06-25-payment-system.md was updated this session. Implement? [Y/n]"
→ **WAIT FOR USER INPUT** 
→ User: "Y" 
→ "Starting TDD implementation..."
```

### Multiple Options
```
/tdd  
→ "Multiple plans found:
   1. todos/2025-06-24-search-filter.md (updated today) ⭐️
   2. todos/2025-06-25-payment-system.md (3 days ago)
   Which would you like to implement?"
→ **WAIT FOR USER SELECTION**
→ User: "1"
→ "Starting search-filter implementation..."
```

### Implementation Flow with Changes
```
/tdd search-filter
→ User: "Y"
→ "🔴 Creating failing test for SkillFilter..."
   ✅ Tests fail due to missing implementation (correct RED)
→ "🟢 Implementing SkillFilter to make tests pass..."
   ✅ All tests pass (correct GREEN)
→ User: "Add mobile support to the plan"
→ "Updating plan with mobile support..."
   ✅ Plan updated
→ "🔵 Refactoring SkillFilter for mobile compatibility..."
   ✅ Tests still pass after refactoring
→ "✅ Task completed, moving to next phase..."
```

## Integration Notes

### With /plan Command
- Seamless continuation from planning to implementation
- Maintains plan structure and TDD design
- Preserves TodoWrite tool state

### With Regular Development
- Coexists with ad-hoc TodoWrite tasks
- No interference with simple fixes and changes
- Focuses on structured implementation only

### With Existing Codebase
- Respects existing code patterns and architecture
- Follows repository testing guidelines
- Integrates with project-specific test commands

## Key Principles

- **Test-First Development**: Always write tests before implementation
- **Implementation Focus**: Manages execution, not planning
- **Simple Updates**: Plan changes integrated naturally
- **Progress Transparency**: Clear status reporting throughout process
- **User Confirmation**: Never proceeds without explicit consent