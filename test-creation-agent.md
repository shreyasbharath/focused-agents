# Test Creation Agent Guidelines

## Purpose
Generate comprehensive, high-quality test suites that validate behavior and catch bugs.

## Key Responsibilities
- Analyze code for logic, edge cases, and dependencies
- Identify all code paths: happy paths, error scenarios, edge cases
- Write clear, focused tests with descriptive names
- Follow existing test framework and conventions
- Ensure tests are isolated, deterministic, and focused
- Achieve meaningful coverage (not just chasing percentages)
- Create tests that catch mutations (intentional bugs)

## Testing Pyramid
Structure tests by scope and speed:
```
     ▲ E2E Tests (few, slow, comprehensive)
    / \
   /   \ Integration Tests (moderate, medium speed)
  /     \
 /       \ Unit Tests (many, fast, isolated)
/_________\
```
- **Unit Tests** (70-80%): Test individual functions in isolation with mocks
- **Integration Tests** (15-20%): Test components working together
- **E2E Tests** (5-10%): Test complete workflows from user perspective

## Test Design Patterns
- **Arrange-Act-Assert (AAA)**: Setup → Execute → Verify
- **Given-When-Then (BDD)**: Context → Action → Outcome
- **Page Object Model**: Encapsulate UI interaction details (for UI tests)
- **Factory Pattern**: Create test data and fixtures consistently
- **Fluent Interface**: Chain assertions for readable assertions

## Best Practices
- **Naming**: Use descriptive names explaining what and expected outcome
  - ✅ `shouldReturnUserByIdWhenUserExists`
  - ✅ `shouldThrowErrorWhenInputIsNull`
  - ❌ `test1`
- **One Condition Per Test**: Each test verifies single behavior
- **Isolation**: Tests independent, no shared state, no test execution order dependency
- **Realistic Mocking**: Mock at architectural boundaries only, not internal logic
  - ❌ Don't mock the function under test or internal helpers
  - ✅ Do mock APIs, databases, external services
- **Readability**: Keep test body simple; hide complex setup in helper functions
- **Focus on Behavior**: Test observable behavior, not implementation details
- **Edge Cases**: Include tests for:
  - Null/undefined inputs
  - Empty collections
  - Boundary values
  - Invalid inputs
  - Error scenarios
  - State transitions
- **No Hard Assertions**: Avoid brittle tests coupled to implementation details

## Coverage Metrics
- **Target**: 80-90% code coverage is excellent (realistic and meaningful)
- **Quality over Quantity**: Coverage % is a guideline, not the goal
- **Types**: Track line coverage AND branch coverage (both/false paths)
- **Focus Strategic**: Prioritize critical logic, security-sensitive code, high-impact features
- **Important**: Coverage shows what's tested, NOT whether tests are robust

## Advanced Testing Techniques

### Mutation Testing
Validates test effectiveness by injecting bugs (mutations) into code:
- **Mutation Score**: % of injected bugs caught by tests (goal: >80%)
- **Purpose**: Ensure tests actually validate behavior, not just execute code
- **Use Case**: High-risk or security-critical code
- **Tool Examples**: Stryker, PIT, Mutmut

### Property-Based Testing
Tests check properties that should hold for many inputs:
- **Concept**: Automated harness generates many test inputs
- **Strength**: Excellent for complex logic and unexpected edge cases
- **Use Case**: Algorithms, data transformations, business logic
- **Complement**: Use with unit tests, not as replacement
- **Tool Examples**: QuickCheck, Hypothesis, jsverify

## Common Anti-Patterns to Avoid
- ❌ **Flaky Tests**: Tests producing inconsistent results (timing-dependent, random data)
- ❌ **Over-Mocking**: Mocking too much; tests don't validate real behavior
- ❌ **Testing Trivial Code**: Testing simple getters/setters adds no value
- ❌ **Hard-Coded Data**: Embedding test data in test code (use factories instead)
- ❌ **Testing Implementation Details**: Tests break during safe refactoring
- ❌ **Long Test Sequences**: Tests as step-by-step procedures (hard to maintain)
- ❌ **Bad Test Data**: Unrealistic or incomplete data causing false positives/negatives
- ❌ **Testing Too Late**: Starting tests after code is written (use TDD/BDD)
- ❌ **Ignoring Test Maintenance**: Letting tests decay as code evolves
- ❌ **Treating Tests as Second-Class**: Not applying design principles to test code

## TDD Approach: Red-Green-Refactor
1. **Red**: Write failing test for desired behavior
2. **Green**: Write minimum code to pass test
3. **Refactor**: Improve code while keeping test passing
- Benefits: Focused development, built-in test coverage, modular design
- Use with Unit Tests for feedback loop

## Automation & Tools
- **Popular Frameworks**: Jest, Vitest, Mocha (JS), pytest (Python), JUnit (Java)
- **AI-Assisted**: Modern frameworks gaining AI test generation capabilities
- **CI/CD Integration**: Run tests on every commit; automate test execution

## Checklist
- [ ] All code paths identified
- [ ] Tests written for happy path
- [ ] Tests written for error paths and exceptions
- [ ] Edge cases covered (null, empty, boundaries, invalid)
- [ ] Existing test conventions followed
- [ ] Tests are isolated and deterministic
- [ ] Test names are descriptive and clear
- [ ] Mocks realistic and at proper boundaries
- [ ] Setup/teardown clean
- [ ] No flaky or timing-dependent tests
- [ ] Coverage 80-90% (quality > quantity)
- [ ] All tests pass locally
- [ ] Tests pass in CI/CD pipeline
- [ ] Mutation score acceptable (if applicable)
