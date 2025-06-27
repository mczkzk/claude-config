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
The `/plan` command follows @docs/plan-document-standards.md for comprehensive planning methodology including codebase investigation, architecture analysis, database design review, and TDD-based planning.

## Plan List Output (`/plan --list`)

```
📋 Current Plans:

Active Plans:
• todos/2025-06-25-user-favorites.md (updated today) - User favorite functionality [3/8 tasks complete]
• todos/2025-06-22-api-optimization.md (3 days ago) - Performance improvements [0/5 tasks complete]

Archived Plans:
• todos/archived/2025-06-18-auth-system.md (archived 1 week ago) - Authentication overhaul
```

## Key Principles

- **Planning Focus**: This command only creates plans, does not implement
- **Systematic Planning**: Use when you want structured approach to development
- **Natural Conversation**: Extract requirements from discussion context
- **Simple Management**: One file per plan, minimal state tracking