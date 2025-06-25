# Command Execution Guidelines

## Claude Code Tool Usage Policy

### Core Principle: Keep Commands Simple
Claude Code requests execution permission for complex commands that use multiple tools or perform many operations. To avoid interruptions, keep individual commands simple and focused.

### Preferred Patterns

#### ✅ Good: Simple, Single-Purpose Commands
```typescript
// Instead of using Task tool for complex multi-step investigation
// Break into simple, direct tool calls:

// Step 1: Find work listing components
Glob pattern: "**/work*" or "**/Work*"

// Step 2: Read specific files
Read: src/app/works/page.tsx

// Step 3: Search for specific patterns
Grep pattern: "useWork|fetchWork" in "**/*.{ts,tsx}"
```

#### ❌ Avoid: Complex Multi-Tool Commands
```typescript
// This triggers permission requests:
Task tool with long prompts asking to:
- Search multiple patterns
- Read multiple files  
- Analyze architecture
- Provide recommendations
- All in one command
```

### Recommended Approach

#### Investigation Workflow
1. **Simple Search**: Use Glob/Grep for specific patterns
2. **Targeted Reading**: Read 1-3 specific files at a time
3. **Incremental Analysis**: Build understanding step by step
4. **Small Batches**: Group related simple operations

#### Implementation Workflow
1. **Single File Edits**: One Edit/MultiEdit per command
2. **Focused Tests**: Test specific functionality only
3. **Simple Validation**: Run one command (lint, test, build)
4. **Progressive Changes**: Make small, verifiable changes

### Tool Usage Best Practices

#### File Operations
- **Glob**: Single pattern searches
- **Grep**: Specific pattern matching
- **Read**: 1-3 files maximum per call
- **Edit/MultiEdit**: Single file modifications

#### Development Operations
- **Bash**: Single commands (npm run test, not npm run test && npm run build)
- **Multiple Bash**: Use parallel execution for independent commands
- **TodoWrite**: Simple task lists, not complex planning

#### Investigation Strategy
- Start with targeted searches using existing knowledge
- Read key files identified from searches
- Use multiple simple commands instead of complex Task tool requests
- Build understanding incrementally

### Command Complexity Guidelines

#### Simple (No Permission Required)
- Single file operations
- Single pattern searches
- Single command execution
- Basic CRUD operations

#### Complex (May Trigger Permission)
- Multi-step investigations
- Cross-cutting changes
- Complex analysis requests
- Multiple tool coordination

### Exception Cases
When complex operations are necessary:
- Break into smaller phases
- Use TodoWrite to track progress
- Execute in small batches
- Validate each step before proceeding

This approach ensures smooth development workflow while maintaining code quality and thorough investigation practices.