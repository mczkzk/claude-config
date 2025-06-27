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

Creates detailed implementation plans when you want to plan systematically before implementation.

## Usage

```
/plan
# Analyzes entire conversation history to create implementation plan

/plan [specifications, requirements, mockups, or descriptions]
# Creates plan directly from provided specifications

/plan --list
# Shows all existing plans
```

## Core Features

### Conversation Analysis Mode (`/plan`)
1. **Full Session Analysis**: Reviews entire conversation from beginning
2. **Requirement Extraction**: Pulls specs from discussions, images, and context
3. **Feature Name Generation**: Auto-creates appropriate feature names
4. **Context Integration**: Consolidates scattered requirements into structured specs

### Direct Specification Mode (`/plan [specs]`)
1. **Requirement Parsing**: Structures provided specifications
2. **Feature Identification**: Extracts core features and user stories
3. **Constraint Analysis**: Identifies technical requirements and limitations

### Planning Process
1. **Codebase Investigation**: Searches for existing patterns and reusable components
2. **Architecture Analysis**: Ensures consistency with existing codebase
3. **TDD Design**: Creates comprehensive test cases first
4. **Task Breakdown**: Structures implementation in Test → Code → Refactor cycles
5. **Plan Document Creation**: Generates detailed markdown plan files

## Planning Workflow

### 1. Plan Creation
- Have natural conversation about requirements OR provide direct specifications
- Run `/plan` to generate plan file in `todos/YYYY-MM-DD-[feature-name].md`
- Discuss and refine plan through conversation

### 2. Plan Updates
Plans can be updated anytime through natural conversation:
```
"Update the plan to include bulk operations"
"Add mobile support to the current plan"
"Remove the complex authentication - use simple login instead"
```
- Direct content rewrite as needed
- No complex change tracking during planning

### 3. Implementation Handoff
- Run `/tdd` to begin implementation
- Implementation managed by `/tdd` command

## File Management

### Plan File Location
- **All Plans**: `todos/YYYY-MM-DD-[feature-name].md`
- **Completed Plans**: `todos/completed/YYYY-MM-DD-[feature-name].md` (archived after completion)

### Simple Lifecycle
- **Planning & Implementation**: Same file, updated as needed
- **Completion**: Manual move to `todos/completed/` when done

## Plan Output Format

Generated plans include:
- **Requirements Summary**: Structured list of what needs to be built
- **Architecture Impact**: How this fits into existing codebase
- **File Changes**: List of Modified Files and New Files to be created
- **Testing Strategy**: Test cases and TDD cycles (written first)
- **Implementation Plan**: Step-by-step TDD development tasks with checkboxes
- **Risk Assessment**: Potential challenges and mitigation strategies

## Plan List Output (`/plan --list`)

```
📋 Current Plans:

Active Plans:
• todos/2025-06-25-user-favorites.md (updated today) - User favorite functionality [3/8 tasks complete]
• todos/2025-06-22-api-optimization.md (3 days ago) - Performance improvements [0/5 tasks complete]

Completed Plans:
• todos/completed/2025-06-18-auth-system.md (completed 1 week ago) - Authentication overhaul
```


## Supported Input Formats

- Slack text, JIRA screenshots, informal requirements
- Conversation context and natural language descriptions
- Technical specifications and mockups
- Images and visual references (automatically extracted to text during planning to preserve design details beyond token limits)

## Key Principles

- **Planning Focus**: This command only creates plans, does not implement
- **Systematic Planning**: Use when you want structured approach to development
- **Natural Conversation**: Extract requirements from discussion context
- **TDD-Based Planning**: Creates plans following @docs/methodology.md TDD and refactoring standards
- **Simple Management**: One file per plan, minimal state tracking