# Claude Code User Configuration

This repository manages user configuration and documentation for Claude Code.

## Included Files

- [`CLAUDE.md`](CLAUDE.md) - Claude Code user instruction settings
- `docs/` - Rules and guidelines
  - [`behavioral-control.md`](docs/behavioral-control.md) - Behavioral control guidelines (Normal mode only)
  - [`commands.md`](docs/commands.md) - Command execution guidelines
  - [`continuous-learning.md`](docs/continuous-learning.md) - Continuous learning & documentation guidelines
  - [`database-design.md`](docs/database-design.md) - Database design and migration management guidelines
  - [`production-safety.md`](docs/production-safety.md) - Production environment safety protocol and incident prevention
  - [`date.md`](docs/date.md) - Date management standards for documentation
  - [`methodology.md`](docs/methodology.md) - Programming methodology standards (TDD, refactoring)
- `commands/` - Custom command definitions
  - [`commit.md`](commands/commit.md) - Git commit creation command
  - [`plan-search.md`](commands/plan-search.md) - Investigation and requirements gathering command
  - [`plan-exec.md`](commands/plan-exec.md) - Implementation plan creation command
  - [`plan-verify.md`](commands/plan-verify.md) - Plan verification and quality assurance command
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
- Run `/plan-exec [feature-name]` (requires completed plan-search)
- Creates detailed implementation design document
- Document includes: API design, data structures, component architecture, test strategy

### 3. Plan Verification | Normal Mode
- Run `/plan-verify [feature-name]` to verify plan quality and completeness
- Interactive verification of each plan section
- Quality assurance before implementation begins

### 4. Implementation | Auto-accept Mode
- Use natural language: "go", "この計画を実装して", or specify plan file
- Auto-accept mode enables rapid, uninterrupted development cycles

### 5. Archive
- Move completed, paused, or shelved plan files to `plans/archive/` directory
- Keeps active workspace clean while preserving work for reference

### Context Recovery
When context is lost during development:
- Reference the implementation design document
- Re-paste screenshots if needed
- Ensure all requirements are still captured

## Project Tips

### Incident Documentation
For individual projects, consider creating a `docs/incidents/` directory to document failures, major setbacks, and lessons learned. Add `@docs/incidents/` to your project's CLAUDE.md to help Claude Code learn from past mistakes and prevent similar issues.

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
- `projects/` - Project history
- `statsig/` - Statistics data
- `todos/` - TODO history

These are excluded by `.gitignore`, so they won't be affected during synchronization.