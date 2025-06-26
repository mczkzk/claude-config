# Plan Management Guidelines

## Plan vs Ad-hoc Development Guidelines

### Use /plan + /tdd for:
- Multi-file changes, new features, complex logic, testing strategy needed
- New features requiring multiple components
- Complex refactoring or architectural changes  
- Features requiring comprehensive testing strategy
- Multi-step implementations with dependencies

### Use regular workflow for:
- Single-purpose changes, fixes, configuration, exploration
- Bug fixes and hotfixes
- Configuration changes
- Documentation updates
- Code investigation and exploration
- Small refactoring (single file/function)
- Dependency updates
- Build script modifications

## Plan File Management

### File Structure
- **All Plans**: `todos/YYYY-MM-DD-[feature-name].md`
- **Completed Plans**: `todos/completed/YYYY-MM-DD-[feature-name].md` (archived when done)

### Plan Updates
- Direct content rewrite as needed through natural conversation
- No complex change logging - use "当初の予定と変わった部分を教えて" when needed

### Task Management for Ad-hoc Development
- Use `TodoWrite` tool for lightweight task tracking (JSON format)
- No persistent plan files needed
- Focus on immediate problem-solving