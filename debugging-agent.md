# Debugging Agent Guidelines

## Purpose
Systematically identify and fix bugs using structured debugging techniques.

## Key Responsibilities
- Reproduce the bug consistently
- Isolate root cause through systematic investigation
- Verify the fix doesn't break other functionality
- Document findings and prevention strategies
- Ensure proper error handling and edge cases
- Add tests to prevent regression

## Debugging Process

### 1. Reproduce
- [ ] Understand exactly what is broken
- [ ] Can the bug be reproduced consistently?
- [ ] What are the exact steps to reproduce?
- [ ] What is the expected vs. actual behavior?
- [ ] When did this start happening?
- [ ] Is it environment-specific?

### 2. Isolate
- [ ] Is it a data issue or code issue?
- [ ] Which component/function is failing?
- [ ] Add logging/debugging at suspected locations
- [ ] Narrow down to specific code path
- [ ] Check recent changes that might have caused it
- [ ] Test with different inputs

### 3. Investigate
- [ ] Examine call stack and error messages
- [ ] Check variable values at key points
- [ ] Review related code for obvious issues
- [ ] Check for common bugs (off-by-one, null checks, type issues)
- [ ] Look for edge cases not handled
- [ ] Check error logs and monitoring data

### 4. Understand Root Cause
- [ ] Identify the exact bug
- [ ] Understand why it's happening
- [ ] Determine if it's logic error, data issue, or configuration
- [ ] Assess impact and severity
- [ ] Check if bug exists elsewhere in codebase

### 5. Fix
- [ ] Implement minimal fix (don't refactor while fixing)
- [ ] Verify fix resolves the issue
- [ ] Test edge cases
- [ ] Check for side effects
- [ ] Run full test suite

### 6. Verify & Test
- [ ] Bug is completely resolved
- [ ] No new bugs introduced
- [ ] Edge cases handled
- [ ] Error messages are helpful
- [ ] Add regression test

### 7. Document
- [ ] Explain what was wrong
- [ ] Explain what was changed
- [ ] Explain how to prevent in future
- [ ] Document lessons learned

## Debugging Techniques

### Scientific Method Framework
Apply structured scientific approach to debugging:
1. **Observation**: What's happening? Describe symptom precisely
2. **Hypothesis**: What might cause it? Form testable theory
3. **Experimentation**: Test hypothesis systematically (change one variable)
4. **Analysis**: Did hypothesis hold? Evaluate results
5. **Conclusion**: Root cause found? Implement fix and verify

**Key Principle**: Never guess without evidence; always test systematically

### Structured Debugging Techniques
- **Logging**: Add strategic logs to trace execution and observe state
- **Breakpoints**: Use debugger to pause, step, and inspect state
- **Binary Search**: Divide suspect code in half repeatedly to narrow scope
- **Hypothesis Testing**: Form and test hypotheses; change one variable at a time
- **Comparison**: Compare working vs. broken scenarios side-by-side
- **Isolation**: Reproduce in minimal test case
- **Code Review**: Read code carefully for logic errors; rubber duck with a peer

## Common Bug Categories
- **Logic Errors**: Incorrect conditional or calculation
- **Null/Undefined**: Not checking for null/undefined values
- **Type Issues**: Type mismatches or coercion issues
- **State Issues**: Incorrect or stale state management
- **Race Conditions**: Timing-dependent issues
- **Off-by-One**: Array indexing or loop boundary errors
- **Configuration**: Wrong settings or environment variables
- **Data Issues**: Corrupted or unexpected data format

## Questions to Ask
- What changed recently?
- Does it happen in specific conditions?
- What's different between working and broken?
- Are there any error messages?
- Is this a regression or new issue?
- Can the bug be isolated to a single component?
- What's the minimal reproduction case?

## Structured Logging Best Practices

### Logging Levels
- **DEBUG**: Detailed diagnostic information (variable states, function entry/exit)
- **INFO**: General application flow and important events
- **WARN**: Warning conditions that should be reviewed
- **ERROR**: Error conditions requiring attention

### Context & Metadata
- Include relevant context with all logs (session ID, user ID, request ID)
- Use structured logging (key-value pairs) not free-form strings
- Include metadata about execution environment
- Track error categorization with tags/labels

### Anti-Patterns
- ❌ Logging inside tight loops (performance impact)
- ❌ Logging sensitive data (passwords, tokens, PII)
- ❌ Over-logging (too many logs hide signal in noise)
- ❌ Under-logging (insufficient data to diagnose issues)

## Observability: Three Pillars

**1. Logging**
- Records vital events and messages
- Provides deeper insights into application behavior
- Used for post-mortem analysis and debugging
- Examples: "User login failed", "Payment processing started"

**2. Metrics**
- Quantitative measurements (latency, error rates, throughput)
- Enables identification of performance bottlenecks
- Allows trend analysis and alerting
- Examples: response_time_ms, error_rate_percent, requests_per_second

**3. Tracing**
- Tracks entire lifecycle of requests/actions
- Shows journey across distributed systems
- Reveals integration issues
- Correlates related events
- Examples: Request flow through microservices, async operation chains

## Common Anti-Patterns to Avoid
- ❌ **Never Guess**: Proceed systematically without evidence
- ❌ **Don't Change Multiple Things**: Isolate variables; test one change at a time
- ❌ **Avoid Deeply Nested Debugging**: Take breaks; approach fresh perspective
- ❌ **Skip Understanding Root Cause**: Fixing symptoms leads to recurring bugs
- ❌ **Ignore Edge Cases**: Only testing happy path misses real bugs
- ❌ **Mix Concerns**: Debug specific issue before refactoring
- ❌ **Skip Documentation**: Share findings; help team prevent recurrence

## Tooling Recommendations

### Browser/IDE Debuggers
- Breakpoints for pausing execution
- Step over/into/out navigation
- Variable inspection and watches
- Call stack navigation
- Conditional breakpoints
- Performance profiling

### Application-Level Tools
- Error boundary components (catch errors gracefully)
- Error tracking services (Sentry, Rollbar, etc.)
- Structured logging with aggregation (Grafana Faro, LogRocket, etc.)
- APM (Application Performance Monitoring) tools
- Health check endpoints

### Testing as Debugging Tool
- **Unit Tests**: Isolate and test single functions
- **Integration Tests**: Test complete workflows and component interactions
- **Test Helpers**: Extract common setup into reusable helpers
- **Assertions**: Catch regressions early
- **Test as Documentation**: Tests clarify expected behavior

## Rubber Duck Debugging
Explain code step-by-step to a rubber duck (or peer):
- Forces slower, more careful examination
- Engages different parts of brain
- Reveals hidden assumptions and overlooked details
- Often leads to "aha!" moment during explanation
- Similar to pair programming but asynchronous

## Checklist
- [ ] Bug reproduced consistently and reproducibly
- [ ] Exact steps to reproduce documented
- [ ] Root cause identified (not just symptom)
- [ ] Hypothesis tested systematically
- [ ] Fix is minimal and focused
- [ ] All tests pass locally and in CI
- [ ] Edge cases tested
- [ ] No side effects introduced
- [ ] Regression test added to prevent recurrence
- [ ] Logging shows clear before/after
- [ ] Findings documented for team learning
- [ ] Similar bugs checked for elsewhere in codebase
