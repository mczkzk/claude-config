---
description: Create a git commit with proper format following repository conventions
allowed-tools: 
  - Bash(git:*)
---

Create a git commit following these steps:

1. Run `git status` to see all untracked files
2. Run `git diff` to see both staged and unstaged changes
3. Run `git log --oneline -5` to see recent commit messages for style reference
4. Analyze all changes and draft an appropriate commit message
5. Add relevant untracked files to staging area if needed
6. Create the commit with an appropriate message
   - Follow repository's commit message conventions

Follow the repository's existing commit message style and focus on the "why" rather than the "what" of the changes.