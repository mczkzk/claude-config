# Claude Code User Configuration

This repository manages user configuration and documentation for Claude Code.

## Included Files

- [`CLAUDE.md`](CLAUDE.md) - Claude Code user instruction settings
- `docs/` - Rules and guidelines
  - `claude-behavior/` - Claude Code's behavioral principles
    - [`command-policy.md`](docs/claude-behavior/command-policy.md) - Command execution policy
    - [`learning-suggestions.md`](docs/claude-behavior/learning-suggestions.md) - Continuous learning & documentation
    - [`date-handling.md`](docs/claude-behavior/date-handling.md) - Date management standards
    - [`confidence-indicators.md`](docs/claude-behavior/confidence-indicators.md) - Confidence level indication system
  - `user-input/` - User input interpretation and response
    - [`shortcuts.md`](docs/user-input/shortcuts.md) - Basic response shortcuts (y/n/u)
    - [`investigation-keywords.md`](docs/user-input/investigation-keywords.md) - Investigation request handling
  - `development/` - Development methodologies and technical guidelines
    - [`tdd.md`](docs/development/tdd.md) - Test-Driven Development principles
    - [`refactoring.md`](docs/development/refactoring.md) - Code refactoring techniques
    - [`database-design.md`](docs/development/database-design.md) - Database design and migration guidelines
    - [`production-safety.md`](docs/development/production-safety.md) - Production environment safety protocol
    - [`api-design.md`](docs/development/api-design.md) - API design guidelines with Richardson Maturity Model
- `commands/` - Custom command definitions
  - [`commit.md`](commands/commit.md) - Git commit creation command
  - [`plan-search.md`](commands/plan-search.md) - Investigation and requirements gathering command
  - [`plan-build.md`](commands/plan-build.md) - Plan document creation command
- [`settings.json`](settings.json) - Claude Code configuration file


## Development Workflow

For larger implementations, use this structured approach:

### 1. Investigation & Requirements | Normal Mode
- Run `/plan-search [feature-name]` to create investigation checklist
- System prompts for specifications, screenshots, requirements
- Complete all investigation items through interactive conversation
- Thorough codebase, database, and dependency analysis
- **Tip**: Save screenshots in `plans/` directory for easy reference during search phase

### 2. Plan Creation | Normal Mode  
- Run `/plan-build [feature-name]` (requires completed plan-search)
- Creates detailed plan document with automatic section completeness verification
- Document includes: API design, data structures, component architecture, test strategy

### 3. Implementation | Auto-accept Mode
- Use natural language: "go", "この計画を実装して", or specify plan document
- Auto-accept mode enables rapid, uninterrupted development cycles

### 4. Archive
- Move completed or shelved plan documents to `plans/archive/` directory
- Keeps active workspace clean while preserving work for reference

### Context Recovery
When context is lost during development:
- Reference the plan document
- Re-paste screenshots if needed
- Ensure all requirements are still captured


## Project Tips

### Incident Documentation
For individual projects, consider creating a `docs/incidents/` directory to document failures, major setbacks, and lessons learned. Add `@docs/incidents/` to your project's CLAUDE.md to help Claude Code learn from past mistakes and prevent similar issues.

### Temporary Notes and Records
Create a `notes/` directory in your project for quick notes and records from Claude Code conversations. This is useful for capturing insights, debugging information, or temporary findings that you want to preserve but aren't ready to formalize into documentation.


## Advanced Techniques

### Documentation Re-reading Technique
For any complex task or project, you can trade token consumption for comprehensive context by asking Claude Code to:
```
Re-read ALL documentation in both project `docs/` AND user global `~/.claude/docs/`
```
This technique loads all available guidelines and rules at conversation start, ensuring Claude Code has full context of your development standards and practices across all types of work.


## How to Sync Settings on Another PC

If you have an existing `~/.claude` directory, you can sync only the configuration files using the following steps:

```bash
# Navigate to .claude directory
cd ~/.claude

# Initialize git repository
git init

# Add remote repository
git remote add origin https://github.com/mczkzk/claude-config.git

# Fetch from remote
git fetch origin

# Create local branch tracking remote main branch
git checkout -b main origin/main

# Checkout individual files if needed
git checkout origin/main -- docs/
git checkout origin/main -- commands/
git checkout origin/main -- CLAUDE.md
git checkout origin/main -- settings.json
git checkout origin/main -- .gitignore
```


## Notes

The following directories contain PC-specific data and are excluded from synchronization:
- `ide/` - IDE-related temporary files
- `projects/` - Chat session conversation logs
- `statsig/` - Statsig (Feature Flag) related files
- `todos/` - Todo list storage for TodoRead/TodoWrite tools

These are excluded by `.gitignore`, so they won't be affected during synchronization.