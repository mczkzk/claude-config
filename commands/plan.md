---
description: Create implementation plan from specifications and requirements
allowed-tools:
  - Task
  - Read
  - Glob
  - Grep
  - Write
  - LS
---

# Implementation Planning Command

Analyzes specifications/requirements and creates a detailed implementation plan without starting actual implementation.

## Usage
```
/plan
[specifications, requirements, mockups, or feature descriptions]

/plan --update [feature-name]
[changes, new requirements, or modifications to existing plan]

/plan --list
# Shows all existing draft and active plans
```

## What it does

1. **Requirement Analysis**
   - Parse and structure the provided specifications
   - Identify core features and user stories
   - Extract technical requirements and constraints

2. **Codebase Investigation**
   - Search for related existing code patterns
   - Identify reusable components and services
   - Check architecture consistency requirements

3. **Implementation Design**
   - Design comprehensive test cases first (TDD approach)
   - Break down features into testable units
   - Define component hierarchy and data flow
   - Specify API endpoints and database changes needed
   - Structure tasks in Test → Implementation → Refactor cycles

4. **Plan Document Creation & Management**
   - Creates `todos/draft/YYYY-MM-DD-[feature-name].md` file
   - Includes detailed implementation tasks
   - Can be iteratively refined through discussion
   - Auto-confirmed when `/tdd` command is executed (moves to `todos/active/`)
   - Supports in-place updates with automatic change logging

## Output Format
- **Requirements Summary**: Structured list of what needs to be built
- **Architecture Impact**: How this fits into existing codebase
- **Testing Strategy**: Test cases and TDD cycles (written first)
- **Implementation Plan**: Step-by-step TDD development tasks with checkboxes
- **Risk Assessment**: Potential challenges and mitigation strategies

## File Management
- **Draft Phase**: `todos/draft/YYYY-MM-DD-[feature-name].md` - Plan under discussion
- **Active Phase**: `todos/active/YYYY-MM-DD-[feature-name].md` - Confirmed plan during implementation
- **Completed Phase**: `todos/completed/YYYY-MM-DD-[feature-name].md` - Archived completed plans
- **Refinement**: Plan can be updated through iterative conversation or `/plan --update`
- **Confirmation**: Automatically moved to `active/` when `/tdd` is executed
- **Change Tracking**: Updates to active plans automatically logged with timestamps and reasons (draft plans do not include change logs)

## Planning Workflow
1. `/plan` creates initial draft plan
2. Discuss and refine plan through conversation
3. `/tdd` confirms plan and begins implementation
4. Progress tracked through TodoWrite tool and plan document updates
5. **Implementation adjustments**: `/plan --update [feature-name]` for mid-implementation changes
6. **Plan history**: All changes logged with automatic change tracking

## Plan Update Command (`/plan --update`)

### Usage
```
/plan --update feature-name
[Describe changes needed]
- Found issue with database schema
- Need to add bulk operations
- Performance requirements changed
- New UI requirements from feedback
```

### What Plan Update Does
1. **Identifies Target Plan**: Finds active plan file (draft plans are updated without change logging)
2. **Change Analysis**: Analyzes impact of requested changes
3. **Automatic Logging**: Adds timestamped change log entry (active plans only)
4. **Smart Updates**: Updates relevant sections while preserving completed work
5. **Task Adjustment**: Modifies task lists, adds new tasks, marks obsolete tasks
6. **Progress Preservation**: Maintains existing checkbox states and completion status

### Change Log Format
```markdown
## Change Log

### 2025-06-25 14:30 - Architecture Update
**Reason**: Performance concerns with N+1 queries discovered during Phase 2
**Changes**: 
- Modified API design to include favorite count in work responses
- Added database indexing strategy for UserFavorite queries
- Updated Phase 2 tasks 2.1-2.3 for optimized queries
**Impact**: Medium - affects API design but not UI components
**Status**: Tasks updated, no completed work affected

### 2025-06-26 09:15 - UI Enhancement
**Reason**: User feedback requested bulk favorite operations
**Changes**:
- Added Phase 4.4: Bulk favorite selection UI
- Added Phase 2.5: Bulk favorite API endpoints
- Updated testing requirements in Phase 7
**Impact**: Low - additive changes only
**Status**: New tasks added, existing progress maintained
```

## Plan List Command (`/plan --list`)

Shows all existing plans with status and progress information:

```
📋 Current Plans:

Draft Plans:
• todos/draft/2025-06-25-user-favorites.md (created today) - User favorite functionality 
• todos/draft/2025-06-22-api-optimization.md (3 days ago) - Performance improvements

Active Plans:
• todos/active/2025-06-20-payment-system.md (in progress) - Payment processing [3/8 phases complete]
• todos/active/2025-06-18-notifications.md (paused) - Push notification system [1/5 phases complete]

Completed Plans:
• todos/completed/2025-06-18-auth-system.md (completed 1 week ago) - Authentication overhaul
```

## Important Notes
- This command does NOT implement code - only creates and manages plans
- Plans are saved as persistent files for tracking across sessions
- Use `/tdd` command to confirm plan and begin test-driven implementation
- Supports various input formats: Slack text, JIRA screenshots, informal requirements
- Change tracking maintains full history of plan evolution
- Progress preservation ensures completed work is never lost during updates