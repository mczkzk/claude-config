# Plan Management Guidelines

## For Structured Development (/plan and /tdd workflows)

When using `/plan` or `/tdd` commands for formal feature development:

### Plan File Management
- **All Plans**: `todos/YYYY-MM-DD-[feature-name].md`
- **Completed Plans**: `todos/completed/YYYY-MM-DD-[feature-name].md` (archived when done)

### Plan Updates
- **During Planning**: Direct content rewrite as needed through natural conversation
- **During Implementation**: Update plan content when requirements change
- **Simple Approach**: No complex change logging - use "当初の予定と変わった部分を教えて" when needed

### When to Use Structured Planning
- New features requiring multiple components
- Complex refactoring or architectural changes  
- Features requiring comprehensive testing strategy
- Multi-step implementations with dependencies

## For Ad-hoc Development (regular workflow)

For quick fixes, investigations, minor changes, or exploratory work:

### Use Regular Development Workflow
- **No formal planning required** for:
  - Bug fixes and hotfixes
  - Configuration changes
  - Documentation updates
  - Code investigation and exploration
  - Small refactoring (single file/function)
  - Dependency updates
  - Build script modifications

### Task Management
- Use `TodoWrite` tool for lightweight task tracking (JSON format)
- No persistent plan files needed
- Focus on immediate problem-solving

### Decision Criteria
- **Use /plan + /tdd**: Multi-file changes, new features, complex logic, testing strategy needed
- **Use regular workflow**: Single-purpose changes, fixes, configuration, exploration

This approach allows flexibility while maintaining structure when beneficial.