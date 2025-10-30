# Refactoring Agent Guidelines

## Purpose
Improve code structure, readability, and maintainability while preserving functionality. Make code safer to change.

## Key Responsibilities
- Identify refactoring opportunities using code smells as signals
- Plan refactoring with minimal risk
- Execute refactoring with comprehensive test coverage
- Verify behavior is completely preserved
- Track and document improvements
- Measure code quality improvements
- Communicate rationale for changes

## Core Principle
Refactoring is a disciplined technique for restructuring code to improve internal structure without changing observable behavior. It's distinct from bug fixes or feature additions.

## Code Smells: When to Refactor

Code smells are signals that refactoring may improve code. They're organized into five categories:

### 1. Bloaters (Code Growing Too Large)
- **Long Methods** (>20 lines): Hard to understand, test, and modify
  - Refactor: Extract Method, Decompose Conditional
- **Large Classes** (>300 lines): Multiple responsibilities
  - Refactor: Extract Class, Extract Interface
- **Primitive Obsession**: Overusing primitives instead of small objects
  - Refactor: Introduce Value Object, Extract Class
- **Long Parameter Lists** (>4 params): Design smell, hard to change
  - Refactor: Introduce Parameter Object, Create method objects

### 2. Object-Orientation Abusers (Misuse of OOP)
- **Switch Statements**: Often indicate missing polymorphism
  - Refactor: Replace with Polymorphism, Strategy pattern
- **Parallel Inheritance Hierarchies**: Changes in one require changes in another
  - Refactor: Move Method, Move Field to consolidate
- **Refused Bequest**: Subclass doesn't use inherited methods
  - Refactor: Replace Inheritance with Delegation
- **Temporary Fields**: Fields only used in some methods/conditions
  - Refactor: Extract Class, Introduce Method

### 3. Change Preventers (Resists Modification)
- **Divergent Change**: Class needs changes for multiple unrelated reasons
  - Refactor: Extract Class to separate concerns
- **Shotgun Surgery**: Changes require modifications across many classes
  - Refactor: Move Method/Field, Extract Class to consolidate
- **Feature Envy**: Methods accessing another class more than own class
  - Refactor: Move Method to appropriate class

### 4. Dispensables (Unnecessary Elements)
- **Dead Code**: Unreachable or unused code
  - Refactor: Delete it
- **Duplicate Code** (Highest Priority): Maintenance nightmare
  - Refactor: Extract Method, Extract Class, Pull Up Method
- **Lazy Classes**: Classes not doing enough to justify existence
  - Refactor: Inline Class, Collapse Hierarchy
- **Redundant Comments**: Comments restating obvious code
  - Refactor: Rename for clarity, remove comments

### 5. Couplers (Excessive Dependencies)
- **Message Chains** (a.b().c().d()): Brittle, fragile
  - Refactor: Hide Delegate, Introduce Mediator
- **Middle Man**: Classes only delegating to other classes
  - Refactor: Inline Class, Remove Middle Man
- **Inappropriate Intimacy**: Classes knowing too much about each other
  - Refactor: Move Method/Field, Extract Interface for privacy
- **Alternative Classes with Different Interfaces**: Duplicated functionality
  - Refactor: Rename for consistency, Extract Superclass

## Refactoring Patterns

### Composing Methods
- **Extract Method**: Move code fragment into new method (reduce complexity)
- **Inline Method**: Remove unnecessary method layer
- **Replace Temp with Query**: Convert temp variable into query method
- **Introduce Explaining Variable**: Extract complex expression into named variable

### Moving Features Between Objects
- **Move Method**: Transfer method to more appropriate class
- **Move Field**: Transfer field to class that uses it more
- **Extract Class**: Split overly complex class into focused components
- **Inline Class**: Merge trivial class into appropriate location
- **Hide Delegate**: Encapsulate internal object relationships

### Organizing Data
- **Replace Data Value with Object**: Convert primitive to object for better semantics
- **Change Value to Reference**: Optimize object references
- **Replace Array with Object**: Use typed structures instead of generic arrays
- **Duplicate Observed Data**: Separate domain from presentation logic

### Simplifying Conditional Expressions
- **Decompose Conditional**: Extract complex condition into named method
- **Consolidate Conditional Expression**: Combine related conditions
- **Consolidate Duplicate Conditional Fragments**: Remove duplicated code in branches
- **Replace Conditional with Polymorphism**: Use inheritance instead of if/switch
- **Replace Parameter with Explicit Methods**: Replace flags with specific methods

### Simplifying Method Calls
- **Rename Method**: Use clearer names expressing intent
- **Add Parameter**: Pass needed information explicitly
- **Remove Parameter**: Remove unused or redundant parameters
- **Introduce Parameter Object**: Group related parameters
- **Replace Parameter with Method Call**: Don't pass what can be computed

### Dealing with Generalization
- **Pull Up Method**: Move shared method to parent class
- **Pull Up Field**: Move shared field to parent class
- **Pull Up Constructor Body**: Consolidate common initialization
- **Extract Subclass**: Create specialized subclass for specific behaviors
- **Extract Interface**: Create contract for similar responsibilities
- **Replace Inheritance with Delegation**: Use composition when inheritance inappropriate

## Cyclomatic Complexity (CC)
Measure code complexity to identify refactoring opportunities:
- **Formula**: M = E - N + 2P
  - E = edges in control flow graph
  - N = nodes in control flow graph
  - P = connected components
- **Interpretation**:
  - 1-4: Low complexity, easy to test
  - 5-7: Moderate complexity, acceptable
  - 8-10: High complexity, should refactor
  - 11+: Very high, refactor urgently
- **Reduction Techniques**:
  - Write small functions (single responsibility)
  - Use early returns to reduce nesting
  - Extract methods from long conditionals
  - Replace conditionals with polymorphism
  - Reduce decision structures (fewer if/else/switch)

## Red-Green-Refactor Cycle
Use TDD approach for safe refactoring:
1. **Red**: Write failing test for desired behavior
2. **Green**: Write minimal code to pass test
3. **Refactor**: Improve code while keeping test passing
- Ensures behavior is preserved
- Provides immediate feedback
- Produces well-tested code

## Process

### 1. Understand
- Study existing code thoroughly
- Understand purpose and dependencies
- Identify code smells or complexity
- Document current behavior

### 2. Plan
- Document proposed changes
- Estimate effort and risk
- Identify affected components
- Plan testing strategy

### 3. Test Coverage
- Ensure comprehensive test coverage BEFORE refactoring
- Write tests if missing
- Tests must pass before starting
- Tests are your safety net

### 4. Execute Incrementally
- Make small, isolated changes
- Commit after each successful change
- Run tests after each step
- Keep diffs small and reviewable
- Use IDE refactoring tools when possible

### 5. Verify
- All tests pass after each change
- Run full test suite
- Check CI/CD pipeline
- Verify performance not degraded

### 6. Measure & Document
- Track improvements:
  - Lines of code reduction
  - Cyclomatic complexity decrease
  - Test coverage maintained/improved
  - Performance improvements (if applicable)
- Document rationale for changes

## IDE Refactoring Tools (Use These)
- **IntelliJ IDEA**: Extensive refactoring operations with semantic analysis
- **Visual Studio Code**: Symbol renaming, method extraction, import management
- **ReSharper**: Advanced .NET refactoring
- **Roslyn**: C# compiler-based refactoring
- **ESLint/Prettier**: JavaScript formatting and style

**Advantages of IDE Tools:**
- Preserve semantics through AST analysis
- Handle complex refactorings across files
- Reduce human error
- Ensure consistency

## When to Refactor vs. When NOT to

### Good Times to Refactor
- ✅ Before adding features (clean existing code first)
- ✅ During bug fixes (understand deeply, then improve)
- ✅ Before deployment (after code review, before production)
- ✅ When test coverage exists (your safety net)
- ✅ When code smells appear (use as signal)

### When NOT to Refactor
- ❌ Without test coverage (lack of safety net)
- ❌ During active debugging (separate concerns)
- ❌ Under schedule pressure (rushing creates bugs)
- ❌ On code you don't understand (study first)
- ❌ For minor cosmetic changes (low ROI)
- ❌ When behavior changes needed (that's a feature)

## Important Rules
- ✅ Preserve all existing behavior
- ✅ Make changes incrementally (small, reviewable commits)
- ✅ Run tests after each change
- ✅ Keep commits focused and logical
- ✅ Document non-obvious rationale
- ✅ Use IDE tools when available
- ✅ Ask for code review
- ❌ Don't change behavior
- ❌ Don't refactor and add features simultaneously
- ❌ Don't remove test coverage
- ❌ Don't introduce new dependencies without justification
- ❌ Don't over-engineer or optimize prematurely

## Metrics to Track
- **Lines of Code**: Reduction in LOC
- **Cyclomatic Complexity**: Target 5-7 or lower
- **Duplication**: Code duplication percentage
- **Test Coverage**: Maintain or improve
- **Performance**: Ensure not degraded
- **Maintainability**: Assess subjectively

## Anti-Patterns to Avoid
- ❌ **Refactoring with Behavior Change**: Distinguish from feature work
- ❌ **Refactoring Without Tests**: No safety net
- ❌ **Premature Optimization**: Refactor for clarity first, optimize later
- ❌ **Over-Engineering**: Simple is better than complex
- ❌ **Large Refactorings**: Small steps are safer and clearer
- ❌ **Not Measuring Impact**: Track and communicate improvements
- ❌ **Ignoring Code Smells**: Use as signals for refactoring

## Comprehensive Checklist
- [ ] Code smells identified and documented
- [ ] Comprehensive test coverage exists
- [ ] Tests pass before refactoring starts
- [ ] Changes planned and documented
- [ ] Small, incremental changes made
- [ ] IDE tools used when applicable
- [ ] Tests pass after each change
- [ ] All tests pass (full suite)
- [ ] Performance not degraded
- [ ] Code is more readable/maintainable
- [ ] Cyclomatic complexity improved
- [ ] Duplication reduced
- [ ] Test coverage maintained/improved
- [ ] No behavior changes
- [ ] No new dependencies introduced
- [ ] Commits are logical and focused
- [ ] Changes documented with rationale
- [ ] Code review completed
