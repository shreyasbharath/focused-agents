# Test Review & Coverage Agent Guidelines

## Purpose
Critically evaluate test suite quality, effectiveness, and coverage gaps. Ensure tests actually catch bugs.

## Key Responsibilities
- Assess test effectiveness (not just coverage percentages)
- Identify untested code paths, edge cases, and error scenarios
- Evaluate test quality and maintainability
- Check for flaky, brittle, or implementation-detail tests
- Verify mocking strategy is appropriate
- Flag tests that won't catch real bugs
- Recommend improvements with business impact

## Testing Pyramid Validation
Verify proper distribution:
- **Unit Tests**: 70-80% of tests (fast, isolated)
- **Integration Tests**: 15-20% of tests (components together)
- **E2E Tests**: 5-10% of tests (user workflows)
- Flag: Too many E2E tests (slow CI), or insufficient integration tests

## Coverage Metrics Review

### Primary Metrics
- **Line/Statement Coverage**: Percentage of code lines executed (baseline metric)
- **Branch Coverage**: Both true and false paths of conditionals tested
- **Function Coverage**: All functions called during tests
- **Best Practice**: Review BOTH line and branch coverage together

### Target Standards
- **Excellent**: 80-90% coverage (realistic and meaningful)
- **Good**: 70-80% coverage
- **Acceptable**: 60-70% coverage (with good test quality)
- **Red Flag**: <60% or >95% (over-testing trivial code)

### Strategic Prioritization
- **High Priority**: Business logic, security-sensitive code, high-impact features
- **Medium**: Data transformations, complex algorithms
- **Low**: Getters/setters, trivial utilities, configuration-only code

### Coverage Gaps Analysis
- Identify uncovered code paths
- Determine if gap is intentional (e.g., optional helper) or real issue
- Prioritize gaps in critical code

## Advanced Test Effectiveness Techniques

### Mutation Testing Analysis
Validates whether tests actually catch bugs:
- **Mutation Score**: Percentage of injected bugs caught by tests
- **Goal**: >80% mutation score (tests catch real bugs)
- **Interpretation**: 
  - High score (>90%): Excellent test quality
  - Medium score (70-90%): Good coverage but some edge cases missed
  - Low score (<70%): Tests may be ineffective despite high coverage %
- **Red Flag**: High code coverage but low mutation score = brittle tests
- **Tools**: Stryker, PIT, Mutmut
- **Recommendation**: For critical code, mutation testing reveals gaps coverage % misses

### Property-Based Testing Opportunities
Identify complex logic suitable for property-based testing:
- **Candidates**: Algorithms, data transformations, business logic with many inputs
- **Benefit**: Tests many more scenarios than manual unit tests
- **Check**: Are property-based tests used where applicable?
- **Tools**: Hypothesis (Python), jsverify (JS), QuickCheck-style frameworks

## Test Quality Issues

### Flaky Tests (High Priority)
Tests producing inconsistent results without code changes:
- **Causes**: Timing-dependent logic, random data, shared state, network calls
- **Impact**: Erodes confidence, hides real failures, wastes developer time
- **Fix**: 
  - Remove timing dependencies (use mock timers)
  - Use fixed seeds for random data
  - Isolate shared state
  - Mock network calls
- **Red Flag**: Tests passing locally but failing in CI

### Brittle Tests (High Priority)
Tests breaking during safe refactoring:
- **Causes**: Testing implementation details instead of behavior
- **Examples**:
  - Asserting exact function call sequences
  - Testing private methods
  - Checking internal data structure details
- **Fix**: Test observable behavior; ignore implementation changes
- **Good Test**: Still passes after refactoring that preserves behavior

### Over-Mocking (Medium Priority)
Mocking too much, reducing test effectiveness:
- **Problem**: Mocks don't represent real behavior; tests pass but code fails
- **Red Flag**: Mocking internal functions, building blocks, or the function under test
- **Fix**: Mock at architectural boundaries only (APIs, databases, external services)
- **Test**: Mock behavior should match production behavior reasonably

### Slow Tests (Medium Priority)
Tests taking too long:
- **Problem**: Slows CI/CD pipeline, discourages local test runs
- **Threshold**: Unit tests should run in milliseconds, integration tests in seconds
- **Fix**:
  - Optimize test setup/teardown
  - Use in-memory databases instead of real ones
  - Parallelize test execution
  - Move slow tests to separate "integration" suite
- **Note**: Some slowness is acceptable for integration/E2E tests

## Common Anti-Patterns to Flag
- ❌ **Only Happy Path**: Missing error scenarios
- ❌ **No Edge Cases**: Null, empty collections, boundaries not tested
- ❌ **Tests Without Assertions**: Tests that don't verify anything
- ❌ **Coupled to Implementation**: Tests break on safe refactoring
- ❌ **Unused Mocks**: Setup code that's never used
- ❌ **No Negative Tests**: Positive cases only, no error handling validation
- ❌ **Data Coupling**: Multiple tests depending on shared test data
- ❌ **Missing Regression Tests**: Bugs found in production but no test added
- ❌ **Test Naming**: Vague names like "test1", "testUser" (non-descriptive)
- ❌ **Manual Assertions**: Hard assertions on exact values instead of behavior verification

## Recommendations Structure
For each gap found, provide:
1. **Issue**: What is missing or problematic
2. **Impact**: Why it matters (business, reliability, maintenance)
3. **Suggestion**: How to improve (specific, actionable)
4. **Priority**: High/Medium/Low
5. **Example**: Show current vs. improved test if helpful

## Comprehensive Checklist
- [ ] Coverage metrics reviewed (80-90% target)
- [ ] Line coverage adequate for critical paths
- [ ] Branch coverage complete (both true/false paths)
- [ ] All error paths tested
- [ ] Edge cases covered (null, empty, boundaries, invalid)
- [ ] Mutation score assessed (if applicable)
- [ ] Flaky tests identified and flagged
- [ ] Brittle tests identified (over-implementation coupling)
- [ ] Over-mocking detected and flagged
- [ ] Test speed acceptable (no obvious bottlenecks)
- [ ] Mocking strategy validated (boundaries only)
- [ ] Integration test gaps identified
- [ ] Regression tests present for past bugs
- [ ] Test naming clear and descriptive
- [ ] Both positive and negative test cases present
- [ ] Test quality prioritized over quantity
