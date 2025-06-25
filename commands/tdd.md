---
description: Begin test-driven development from implementation plan
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

Confirms implementation plan and begins test-driven development process.

## Usage
```
/tdd                    # Auto-detect plan from current draft/active plans
/tdd feature-name       # Specify plan explicitly by name
```

## What it does

### 1. Plan Detection & Confirmation
- **Auto-detection priority**:
  1. Plans created/updated in current session
  2. Most recently updated feature files (implementation-ready plans)
  3. Plans matching current conversation context
  4. Most recently updated draft files (work-in-progress plans)

- **Smart confirmation**:
  - Single clear candidate: "Implement [plan-name]? [Y/n]" → **WAIT for explicit user response**
  - Multiple candidates: Present numbered selection → **WAIT for user selection**
  - Context match: "You mentioned [topic], implement [matching-plan]?" → **WAIT for confirmation**
  - **CRITICAL**: Never proceed without explicit user confirmation (Y/yes/1/etc.)

### 2. Plan Finalization
- Convert `todos/draft/YYYY-MM-DD-[name].md` → `todos/active/YYYY-MM-DD-[name].md`
- Initialize Change Log section if not present
- **Create initial phase tasks only** (not entire plan at once)
- Mark first task as "in_progress"
- **Progressive task creation**: Add subsequent phases as current phase nears completion

### 3. TDD Implementation Process

#### ⚠️ CRITICAL: TEST-FIRST RULE
**Tests are the specification. Without tests first, specifications are unclear.**
- **NEVER create implementation files before tests exist**
- **ALWAYS start with test file creation**

#### Implementation Cycle (Strict Order)
1. **🔴 RED**: Write test first to define specification, create minimal stub that fails
2. **🟢 GREEN**: Write implementation to make tests pass
3. **🔵 REFACTOR**: Improve code quality while keeping tests green

#### RED Phase Process
1. **Create test file FIRST** - Write comprehensive test cases
2. **Create minimal stub** - Only enough to make tests compile but fail
3. **Run tests to confirm RED** - Tests must fail due to missing implementation

**Success Criteria:**
- ✅ Test executes without compilation errors
- ✅ Test fails due to missing implementation (not syntax issues)
- ❌ **Implementation file created before test file** ⚠️ MOST COMMON MISTAKE

**Progress Tracking:**
- Update TodoWrite tool and plan document checkboxes after each step

#### TDD Cycle Visual Indicators
Each implementation step shows current phase:
- 🔴 **RED Phase** → "🔴 Creating failing test for [feature] (test runs but fails)..."
- 🟢 **GREEN Phase** → "🟢 Implementing [feature] to pass test..."
- 🔵 **REFACTOR Phase** → "🔵 Refactoring [component] for better design..."
- ✅ **Complete** → "✅ [Feature] implementation complete, moving to next task"

#### Mandatory Test Execution Pattern
**EVERY TDD cycle MUST include these test runs**:
1. **After creating stub + test**: Confirm RED (test fails due to missing implementation)
2. **After initial implementation**: Confirm GREEN (all tests pass)  
3. **After refactoring**: Confirm tests still pass (no regression)
4. **Never skip validation steps** - each phase must be verified with actual test execution

### 4. Continuous Progress Tracking
- **Immediate TodoWrite updates**: Mark tasks as "completed" right after finishing each task
- **Plan document checkbox sync**: Update `todos/active/YYYY-MM-DD-[name].md` checkboxes `[ ]` → `[x]` immediately after task completion
- **Progressive task addition**: Add next phase tasks only when current phase is 80% complete
- **Dual progress tracking**: Both TodoWrite tool AND plan document must stay synchronized
- Automated lint/typecheck execution after major changes
- Change log updates when plan modifications occur during implementation
- **Status reporting**: Regularly inform user of current progress and next steps

#### Progress Indicators
- 📋 **Planning** → "📋 Setting up [task]..."
- 🧪 **Testing** → "🧪 Running test suite..."
- ✅ **Completed** → "✅ Task completed successfully"
- 🚨 **Error** → "🚨 Issue detected, investigating..."

### 5. Plan Completion Management
- **Completion Detection**: When all phases are ✅ completed
- **Archive Action**: Move `todos/active/YYYY-MM-DD-[name].md` → `todos/completed/YYYY-MM-DD-[name].md`
- **Plan Detection Logic**: Scan `todos/draft/` and `todos/active/`, exclude `todos/completed/`
- **Preservation**: Completed plans retain full implementation history and Change Log
- **Final Documentation**: Add completion timestamp and summary to Change Log

## Plan Detection Logic

### Current Session Priority
- Files modified during this conversation session
- Topics mentioned in recent messages
- Explicit references to feature names

### Plan File Scanning
- **Draft plans**: Scan `todos/draft/YYYY-MM-DD-*.md`
- **Active plans**: Scan `todos/active/YYYY-MM-DD-*.md`
- **Exclude completed**: Skip `todos/completed/` directory entirely
- **Priority order**: 
  1. Most recently updated active files (implementation-ready plans)
  2. Plans matching current conversation context  
  3. Most recently updated draft files (work-in-progress plans)

### Fallback Behavior
- **Never auto-execute without explicit user confirmation** 
- Always ask "Which plan?" when multiple candidates exist
- Provide context clues: "(updated today)", "(current session)", etc.
- **If user doesn't respond**: Stop and wait, do not assume consent

## Examples

```
# Clear context
/tdd
→ "todos/draft/2025-06-25-payment-system.md was updated this session. Implement? [Y/n]"
→ **WAIT FOR USER INPUT** 
→ User: "Y" 
→ "Starting TDD implementation..."

# Multiple options
/tdd  
→ "Multiple plans found:
   1. todos/active/2025-06-24-search-filter.md (implementation-ready) ⭐️
   2. todos/draft/2025-06-25-payment-system.md (draft)
   Which would you like to implement?"
→ **WAIT FOR USER SELECTION**
→ User: "1"
→ "Starting search-filter implementation..."

# User declines
/tdd
→ "Implement search-filter? [Y/n]"
→ User: "n"
→ "Implementation cancelled. Plan remains in draft state."

# TDD Cycle Example
/tdd search-filter
→ User: "Y"
→ "🔴 Creating failing test for SkillFilter..."
   ✅ Tests fail due to missing checkboxes and legend (correct RED)
→ "🟢 Implementing SkillFilter to make tests pass..."
   ✅ All tests pass (correct GREEN)  
→ "🔵 Refactoring SkillFilter for better code quality..."
   ✅ Tests still pass after refactoring
→ "✅ Phase 2.2 completed, starting Phase 2.3..."
```

## Integration Notes
- Works seamlessly with `/plan` command output
- Maintains TodoWrite tool state across implementation
- Follows repository testing guidelines
- Respects existing code patterns and architecture