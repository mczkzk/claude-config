# Claude Code User Configuration

This repository manages user configuration and documentation for Claude Code.

## Included Files

- `CLAUDE.md` - Claude Code user instruction settings
- `docs/` - Rules and guidelines
  - `investigation.md` - Investigation guidelines
  - `commands.md` - Command execution guidelines
- `commands/` - Custom command definitions
  - `commit.md` - Git commit creation command
  - `plan.md` - Implementation plan creation command
  - `tdd.md` - Test-driven development command
- `settings.json` - Claude Code configuration file

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