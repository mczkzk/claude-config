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
# No arguments → Analyzes recent conversation history to create implementation plan

/plan [specifications, requirements, mockups, or feature descriptions]
# With arguments → Creates plan directly from provided specifications

/plan --list
# Shows all existing draft and active plans
```

## What it does

### When used without arguments (`/plan`)
1. **Conversation History Analysis**
   - Analyzes entire conversation session from beginning
   - Extracts requirements from user discussions, images, and context
   - Identifies technical specifications and user intent
   - Auto-generates appropriate feature name from conversation content

2. **Context Integration**
   - Consolidates scattered requirements into structured specifications
   - Identifies contradictions and unclear points
   - Lists additional questions that may need clarification

### When used with arguments (`/plan [specifications]`)
1. **Direct Requirement Analysis**
   - Parse and structure the provided specifications
   - Identify core features and user stories
   - Extract technical requirements and constraints

### Common Steps for Both Modes
3. **Codebase Investigation**
   - Search for related existing code patterns
   - Identify reusable components and services
   - Check architecture consistency requirements

4. **Implementation Design**
   - Design comprehensive test cases first (TDD approach)
   - Break down features into testable units
   - Define component hierarchy and data flow
   - Specify API endpoints and database changes needed
   - Structure tasks in Test → Implementation → Refactor cycles

5. **Plan Document Creation & Management**
   - Creates `todos/draft/YYYY-MM-DD-[feature-name].md` file
   - Feature name auto-generated from conversation context (when no arguments) or user-specified
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
- **Refinement**: Plan can be updated through natural conversation (e.g., "Update the plan to include bulk operations")
- **Confirmation**: Automatically moved to `active/` when `/tdd` is executed
- **Change Tracking**: 
  - **Draft Phase**: Direct content updates without change logs (in-place editing)
  - **Active Phase**: All updates automatically logged with timestamps and reasons

## Planning Workflow

### Conversation-Based Planning
1. Have natural conversation about requirements, features, or show screenshots/mockups
2. `/plan` (no arguments) → Analyzes conversation and creates initial draft plan
3. Discuss and refine plan through conversation
4. `/tdd` confirms plan and begins implementation
5. Progress tracked through TodoWrite tool and plan document updates
6. **Implementation adjustments**: Natural conversation for mid-implementation changes ("Add bulk operation support to the plan")

### Direct Specification Planning
1. `/plan [detailed specifications]` creates initial draft plan
2. Discuss and refine plan through conversation
3. `/tdd` confirms plan and begins implementation
4. Progress tracked through TodoWrite tool and plan document updates
5. **Implementation adjustments**: Natural conversation for mid-implementation changes ("The plan needs database optimization")

### Common Steps
6. **Plan history**: All changes logged with automatic change tracking

## Plan Updates via Natural Conversation

### Usage Examples
```
"Update the plan to include bulk operations"
"The plan needs database optimization due to performance issues"
"Add mobile support to the current plan"
"Remove the complex authentication - we'll use simple login instead"
```

### How Plan Updates Work
1. **Detects Update Intent**: Recognizes when conversation indicates plan changes needed
2. **Identifies Target Plan**: Finds active or draft plan file automatically
3. **Change Analysis**: Analyzes impact of requested changes from conversation context
4. **Update Method**:
   - **Draft Plans**: Direct in-place content updates (no change log)
   - **Active Plans**: Content updates + automatic timestamped change log entry
5. **Smart Updates**: Updates relevant sections while preserving completed work
6. **Task Adjustment**: Modifies task lists, adds new tasks, marks obsolete tasks
7. **Progress Preservation**: Maintains existing checkbox states and completion status (active plans only)

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
- **Conversation Mode**: `/plan` without arguments analyzes recent conversation history automatically
- **Direct Mode**: `/plan [specs]` with arguments creates plan from provided specifications
- Supports various input formats: Slack text, JIRA screenshots, informal requirements, conversation context
- **Natural Updates**: Simply mention changes needed in conversation - no special commands required
- Change tracking maintains full history of plan evolution with automatic logging
- Progress preservation ensures completed work is never lost during updates