# Agent Guidelines Context & Progress

## Project Overview
Creating comprehensive, evidence-based guidelines for specialized software engineering agents. Each agent handles specific tasks with clear responsibilities, best practices, and verification checklists.

**Reference**: [Augmented Coding Patterns - Focused Agent](https://lexler.github.io/augmented-coding-patterns/patterns/focused-agent/)

## Completed Work

### Research Phase ✅
Conducted extensive research on:
- Modern software testing best practices (mutation testing, property-based testing, TDD, testing pyramid)
- Code review best practices (SOLID principles, tiered reviews, 24-hour SLAs, AI-assisted reviews)
- Refactoring techniques (code smells, refactoring patterns, cyclomatic complexity, IDE tools)
- Debugging methodology (scientific method, structured logging, observability)
- Technical documentation (keeping docs in sync, accessibility, examples, anti-patterns)
- Quality gates & pre-commit checks (Conventional Commits, Husky, lint-staged, CI/CD integration)

### Documents Created/Enhanced ✅

1. **solutioning-agent.md** (NEW)
   - Phase 1: Problem understanding (define, root cause, context)
   - Phase 2: Research & exploration
   - **Phase 2.5: Brownfields context capture** (visual diagrams)
   - Phase 3: Solution design with trade-offs
   - Phase 4: Validation
   - Phase 5: Implementation planning
   - Two templates: Standard + Brownfields-specific
   - Brownfields-specific features:
     - Before/After architecture diagrams
     - Current vs. proposed data flows (sequence diagrams)
     - Pain points annotation
     - Metrics baseline → target comparisons
     - Migration strategies (gradual/big-bang/parallel)
     - Rollback plans with triggers
     - Code structure comparison (before/after)
     - Feature flag strategy
     - Phased rollout approach

2. **test-creation-agent.md** (Enhanced)
   - Testing pyramid (unit/integration/E2E distribution)
   - Test design patterns (AAA, BDD, POM, Factory, Fluent Interface)
   - Mutation testing (validates test effectiveness)
   - Property-based testing (for complex logic)
   - Coverage metrics (80-90% target, quality over quantity)
   - TDD red-green-refactor cycle
   - 10+ anti-patterns to avoid

3. **test-review-agent.md** (Enhanced)
   - Testing pyramid validation
   - Coverage metrics review (line, branch, function)
   - Mutation testing analysis
   - Property-based testing opportunities
   - Flaky test detection and fixes
   - Brittle test identification
   - Over-mocking detection
   - Slow test optimization
   - 10+ anti-patterns to flag

4. **code-review-agent.md** (Enhanced)
   - SOLID principles checklist
   - Tiered review process (critical/standard/low-risk)
   - 24-hour initial response SLA
   - Business context understanding emphasis
   - Comment guidelines with structured feedback
   - Comment levels (Critical/Major/Minor/Question)
   - Alternative review methods (pair programming, pair reviewing)
   - AI-assisted review tools
   - Comprehensive 16-item checklist

5. **commit-readiness-agent.md** (Enhanced)
   - Conventional Commits format with types
   - Breaking change documentation
   - Pre-commit hooks automation (Husky + lint-staged)
   - CI/CD quality gate integration
   - Secret scanning integration
   - Trunk-based development support
   - 18-item comprehensive checklist

6. **refactoring-agent.md** (Enhanced)
   - 5 categories of code smells (25+ specific smells):
     - Bloaters (long methods, large classes, primitive obsession, long parameters)
     - OO Abusers (switch statements, inheritance hierarchies, refused bequest)
     - Change Preventers (divergent change, shotgun surgery, feature envy)
     - Dispensables (dead code, duplication, lazy classes)
     - Couplers (message chains, middle man, inappropriate intimacy)
   - 6 refactoring pattern categories (24+ specific patterns):
     - Composing Methods
     - Moving Features Between Objects
     - Organizing Data
     - Simplifying Conditional Expressions
     - Simplifying Method Calls
     - Dealing with Generalization
   - Cyclomatic complexity (CC) measurement and reduction
   - Red-green-refactor cycle
   - IDE refactoring tools guide
   - When to refactor vs. when not to
   - 20-item comprehensive checklist

7. **documentation-agent.md** (Enhanced)
   - Keeping docs in sync with code (strategies)
   - Single source of truth principle
   - Link to specific code locations
   - Versioning and update discipline
   - Automation opportunities
   - Code example quality standards
   - Good vs. bad examples required
   - Tested examples (CI integration)
   - Accessibility requirements (WCAG)
   - Readability standards (sentence length, line length, font size)
   - 6 anti-patterns with fixes:
     - Docs falling behind code
     - Lack of practical examples
     - Excessive jargon
     - Ticket numbers (GO-30731 anti-pattern)
     - Duplicate content
     - Missing context
   - 17-item comprehensive checklist

8. **debugging-agent.md** (Enhanced)
   - Scientific method framework (observation→hypothesis→experiment→analysis→conclusion)
   - Structured debugging techniques (logging, breakpoints, binary search, hypothesis testing)
   - Structured logging best practices
   - Logging levels (DEBUG, INFO, WARN, ERROR)
   - Context & metadata requirements
   - Observability three pillars (logging, metrics, tracing)
   - Common anti-patterns to avoid
   - Tooling recommendations (debuggers, APM, testing)
   - Rubber duck debugging
   - Testing as debugging tool
   - 12-item comprehensive checklist

9. **README.md** (Updated)
   - All 9 agents documented with descriptions
   - Structure of guidelines
   - Key features (evidence-based, practical, comprehensive, collaborative)
   - Using guidelines in task prompts
   - Team integration workflow
   - Philosophy section
   - Example workflow showing agent collaboration

## Key Design Decisions

### Evidence-Based Approach
- All recommendations backed by research (2024-2025 industry standards)
- Included tool recommendations with rationale
- Trade-offs explicitly documented
- Modern methodologies and best practices

### Practical & Actionable
- Real-world examples and scenarios
- Concrete checklists and templates
- Tool setup instructions
- Anti-patterns identified with fixes

### Brownfields-First Thinking
- Solutioning agent includes dedicated brownfields section
- Before/After snapshots for visual context
- Migration strategies and rollback plans
- Feature flag approach for gradual rollout
- Metrics baseline → target tracking

### Visual Documentation
- Mermaid diagram templates (architecture, sequences, flows)
- ASCII art examples
- Code structure comparisons (before/after)
- Tables for trade-offs and comparisons

## File Structure
```
focused-agents/
├── README.md                          # Overview and integration guide
├── CONTEXT.md                         # This file
├── solutioning-agent.md               # Design solutions for brownfields
├── test-creation-agent.md             # Write comprehensive test suites
├── test-review-agent.md               # Review test quality and coverage
├── code-review-agent.md               # Thorough code review with architecture focus
├── commit-readiness-agent.md          # Verify code meets quality gates
├── refactoring-agent.md               # Improve code while preserving functionality
├── documentation-agent.md             # Create maintainable, synced documentation
└── debugging-agent.md                 # Find and fix bugs systematically
```

## Future Enhancements

### Potential New Agents
- **Performance Analysis Agent**: Profile and optimize code
- **Security Review Agent**: Focused on security vulnerabilities
- **Architecture Design Agent**: System-wide design decisions
- **API Design Agent**: RESTful/GraphQL API design
- **Data Migration Agent**: Safe data schema changes

### Potential Enhancements to Existing Agents
- Add language/framework-specific variants
- Include project-specific customization examples
- Add metrics collection and reporting templates
- Create training/onboarding materials for teams
- Build decision trees for agent selection

### Integration Opportunities
- Create PR template referencing relevant agents
- Build CI/CD integration for guideline validation
- Create Slack/Teams bot for guideline access
- Build IDE plugins for guideline reminders
- Create automated tests validating guideline adherence

## How to Use This Context

### For Continuing Work
1. Review this CONTEXT.md for what was completed
2. Check individual agent files for specific details
3. Reference the checklist sections for validation requirements
4. Use templates as starting points for new solutions

### For Adding New Content
1. Research modern best practices for the new agent
2. Follow the established format and structure
3. Include anti-patterns and pitfalls sections
4. Create comprehensive checklists
5. Add brownfields considerations where applicable

### For Team Adoption
1. Start with README.md and philosophy section
2. Reference specific agents in task prompts
3. Use checklists before sign-off
4. Share learnings and update guidelines
5. Customize for project-specific needs

## Team Reference

### Quick Links
- **Solutioning**: Start here for major changes, especially brownfields work
- **Testing**: Test Creation → Test Review → Code Review workflow
- **Quality Gates**: Commit Readiness ensures production readiness
- **Maintenance**: Refactoring, Documentation, Debugging agents
- **Integration**: See README.md for example workflow

### Common Workflows

**New Feature Development**
1. Solutioning Agent → Design approach
2. Test Creation Agent → Write tests
3. Code Creation → Implementation
4. Code Review Agent → Review changes
5. Commit Readiness → Verify quality
6. Documentation Agent → Update docs

**Brownfields Improvement**
1. Solutioning Agent → Analyze brownfields area with before/after
2. Refactoring Agent → Plan structural improvements
3. Code Creation → Implement changes
4. Test Review Agent → Validate coverage
5. Debugging Agent → Fix any issues
6. Documentation Agent → Update architecture docs

**Bug Investigation**
1. Debugging Agent → Find root cause
2. Test Creation Agent → Add regression test
3. Code Review Agent → Review fix
4. Commit Readiness → Quality check

## Notes for Next Session

### Current State Summary
- ✅ All 9 agent guidelines created and enhanced with research
- ✅ Brownfields-specific guidance added to Solutioning Agent
- ✅ Comprehensive checklists and templates created
- ✅ Evidence-based recommendations throughout
- ✅ Modern tools and methodologies (2024-2025)
- ✅ Anti-patterns identified and documented
- ✅ README updated with philosophy and integration

### Ready to Build
- Agent guidelines are comprehensive and ready for team use
- All research findings have been incorporated
- Brownfields workflow is well-documented
- Templates are ready for immediate use
- Checklists provide clear verification criteria

### Potential Next Steps
1. Create project-specific customization guide
2. Build training materials for team onboarding
3. Add language/framework-specific variations
4. Create PR templates and CI/CD integration
5. Build additional specialized agents as needed
6. Develop team metrics to track guideline adoption
7. Create quarterly review process for guideline updates

## Research Summary

### Key Findings Incorporated
- **Testing**: Mutation testing and property-based testing are critical for ensuring test quality beyond coverage %
- **Code Review**: Limited focused comments (5-6) are more effective than extensive feedback; architectural context matters
- **Refactoring**: Code smells are reliable signals for refactoring; cyclomatic complexity helps identify complexity hotspots
- **Debugging**: Scientific method and structured logging prevent guessing; observability across three pillars (logs, metrics, traces) is essential
- **Documentation**: Docs-as-code with single source of truth prevents staleness; accessibility and plain language critical
- **Quality Gates**: Pre-commit hooks catch issues fast; CI/CD gates ensure quality; Conventional Commits enable automation
- **Brownfields**: Before/After snapshots + migration strategies + rollback plans are essential for existing system changes

### Industry Standards Applied
- SOLID principles (code review)
- Conventional Commits specification
- Testing pyramid (unit/integration/E2E)
- Code smells from Refactoring literature
- Cyclomatic complexity metrics
- WCAG accessibility standards
- Three pillars of observability
- Red-Green-Refactor cycle (TDD)

---

**Last Updated**: Current session
**Status**: ✅ Complete and ready for team use
**Files**: 9 comprehensive agent guidelines
**Total Content**: ~15,000 words of research-backed guidance
