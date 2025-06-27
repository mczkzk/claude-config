# Claude Code User Configuration

This repository manages user configuration and documentation for Claude Code.

## Included Files

- `CLAUDE.md` - Claude Code user instruction settings
- `docs/` - Rules and guidelines
  - `behavioral-control.md` - Behavioral control guidelines (investigation & implementation)
  - `commands.md` - Command execution guidelines
  - `continuous-learning.md` - Continuous learning & documentation guidelines
- `commands/` - Custom command definitions
  - `commit.md` - Git commit creation command
  - `plan.md` - Implementation plan creation command
  - `tdd.md` - Test-driven development command
- `settings.json` - Claude Code configuration file

## Development Workflow

For larger implementations, use this structured approach:

### 1. Requirements Analysis | Plan Mode
- Load specifications, screenshots, and requirements
- Use Plan mode to understand and organize requirements

### 2. Design Documentation | Normal Mode  
- Plan mode will create initial plan - decline it with "No"
- Run `/plan ultrathink` to create detailed implementation design document
- Document includes: API design, data structures, component architecture, test strategy

### 3. Implementation | Auto-accept Mode
- Run `/tdd` to implement using test-driven development
- Auto-accept mode enables rapid, uninterrupted development cycles

### 4. Manual Review & Fixes | Normal Mode
- Manual corrections and refinements
- Run lint, type checking, and integration tests
- Final verification before completion

### Context Recovery
When context is lost during development:
- Reference the implementation design document
- Re-paste screenshots if needed
- Ensure all requirements are still captured

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