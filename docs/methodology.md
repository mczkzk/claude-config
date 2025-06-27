# Programming Methodology Guidelines

This document defines the programming methodologies and practices to follow when working with code.

## Test-Driven Development (TDD)

**Methodology**: Follow t-wada (和田卓人) practices

### Core Principles
- **Red-Green-Refactor Cycle**: Write failing test → Make it pass → Improve design
- **Test-First**: Always write tests before implementation
- **Minimal Implementation**: Write only enough code to pass current test
- **Triangulation**: Add test cases to force generalization when needed

### Key References
- t-wada's TDD approach emphasizes disciplined cycles and minimal code changes
- Focus on sustainable development through comprehensive test coverage

## Refactoring

**Methodology**: Follow Martin Fowler techniques

### Core Principles
- **Preserve Behavior**: Never change external behavior during refactoring
- **Small Steps**: Make incremental improvements with frequent testing
- **Green Bar**: Keep all tests passing throughout refactoring process
- **Catalog-Based**: Use established refactoring patterns and techniques

### Code Smell Detection & Response
- **Smell Detection**: Actively identify code smells that indicate design problems
- **Small Fixes**: Address smells through small, focused refactoring steps
- **Test-Driven Refactoring**: Run tests after each small refactoring step
- **Iterative Improvement**: "Detect smell → Apply refactoring → Test → Repeat"

### Common Code Smells to Watch For
- **Duplicated Code**: Identical or similar code in multiple places
- **Long Method**: Methods that are too long and do too much
- **Large Class**: Classes with too many responsibilities
- **Feature Envy**: Methods that use data from other classes extensively
- **Data Clumps**: Groups of data that appear together frequently

### Key References
- Martin Fowler's "Refactoring: Improving the Design of Existing Code"
- Apply proven refactoring techniques rather than ad-hoc code changes

## Application Across Modes

### All Development Modes
- **Refactoring principles** apply universally (Normal, Auto-accept, Plan modes)
- **Code quality standards** remain consistent regardless of execution mode

### TDD-Specific Contexts
- **TDD methodology** applies during implementation phases following plan documents
- **Test-first approach** is integrated into plan document structure and implementation workflow

## Integration with Commands

- **`/plan`**: Consider refactoring opportunities during design phase, structure TDD cycles in implementation tasks
- **Natural language implementation**: Apply TDD methodology with Red-Green-Refactor cycles
- **Manual development**: Apply refactoring principles for code improvements