# Refactoring

**Methodology**: Follow Martin Fowler techniques

## Core Principles
- **Preserve Behavior**: Never change external behavior during refactoring
- **Small Steps**: Make incremental improvements with frequent testing
- **Green Bar**: Keep all tests passing throughout refactoring process
- **Catalog-Based**: Use established refactoring patterns and techniques

## Code Smell Detection & Response
- **Smell Detection**: Actively identify code smells that indicate design problems
- **Small Fixes**: Address smells through small, focused refactoring steps
- **Test-Driven Refactoring**: Run tests after each small refactoring step
- **Iterative Improvement**: "Detect smell → Apply refactoring → Test → Repeat"

## Common Code Smells to Watch For
- **Duplicated Code**: Identical or similar code in multiple places
- **Long Method**: Methods that are too long and do too much
- **Large Class**: Classes with too many responsibilities
- **Feature Envy**: Methods that use data from other classes extensively
- **Data Clumps**: Groups of data that appear together frequently

## Key References
- Martin Fowler's "Refactoring: Improving the Design of Existing Code"
- Apply proven refactoring techniques rather than ad-hoc code changes

## Application Across Modes

### All Development Modes
- **Refactoring principles** apply universally (Normal, Auto-accept, Plan modes)
- **Code quality standards** remain consistent regardless of execution mode

## Integration with Commands

- **Natural language implementation**: Apply refactoring principles for code improvements
- **Manual development**: Use refactoring techniques for continuous improvement