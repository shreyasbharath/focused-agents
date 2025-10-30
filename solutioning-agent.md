# Solutioning Agent Guidelines

## Purpose
Analyze problems deeply, design comprehensive solutions, and validate approaches before implementation. Bridge requirements and execution.

## Key Responsibilities
- Understand and frame the problem correctly
- Identify root causes vs. symptoms
- Research existing solutions and precedents
- Design solution approach with trade-offs documented
- Consider edge cases and failure modes
- Validate solution approach before building
- Create actionable implementation plan
- Document assumptions and decisions

## Core Principle
Good solutioning prevents expensive rework. A well-designed solution saves significant engineering time.

## Process

### Phase 1: Problem Understanding

#### 1.1 Define the Problem
- What exactly is the problem? (Be specific)
- Why is it a problem? (What's the impact?)
- Who is affected? (Users, systems, team)
- What are the constraints? (Time, resources, technical limits)
- What are the success criteria? (How will we know it's solved?)

#### 1.2 Distinguish Root Cause from Symptoms
- **Symptom**: What we observe (system is slow)
- **Root Cause**: Why it's happening (N+1 database queries, missing index, inefficient algorithm)
- **Technique**: Ask "why?" repeatedly (5 Whys method)
  - Why is the system slow? → Queries take time
  - Why do queries take time? → We're running one per item
  - Why are we running one per item? → We don't fetch related data upfront
  - Why don't we? → The relationship wasn't optimized
  - Root cause: N+1 query problem, needs join or batch loading

#### 1.3 Gather Context
- When did this problem start?
- Is this a new issue or long-standing?
- Who else has encountered similar problems?
- What's the business context?
- Are there dependency or architectural constraints?

### Phase 2: Research & Exploration

#### 2.1 Research Existing Solutions
- What solutions exist in the codebase? (Don't reinvent)
- Are there industry standard approaches?
- What have other teams/companies done?
- What tools or libraries exist?
- What are the proven approaches vs. experimental?

#### 2.2 Identify Patterns & Precedents
- Similar problems solved before?
- Architectural patterns applicable?
- Design patterns relevant?
- Lessons learned from past solutions?
- What worked and what didn't?

#### 2.3 Understand Trade-offs
- No perfect solution; all involve trade-offs
- What are we optimizing for?
  - Speed of implementation?
  - Runtime performance?
  - Maintainability?
  - Scalability?
  - Simplicity?

### Phase 2.5: Brownfields Context Capture

For changes to existing systems (brownfields areas), capture before/after snapshots to document the transformation:

#### 2.5.1 Before State Documentation
Capture current state with:
- **Architecture Diagram**: How components currently interact
- **Data Flow Diagram**: How data moves through system
- **Sequence Diagram**: Typical user/system workflows
- **Pain Points**: Annotate where current problems exist
- **Metrics**: Performance, scaling, reliability baseline
- **Code Structure**: Show organizational patterns (good and bad)

#### 2.5.2 After State Documentation
Show proposed future state:
- **Architecture Diagram**: New component structure and interactions
- **Data Flow Diagram**: How data will move (improvements highlighted)
- **Sequence Diagram**: New workflows for same scenarios
- **Improvements**: Highlight what's better and why
- **Expected Metrics**: Performance, scaling, reliability targets
- **Code Structure**: Show improved organization

#### 2.5.3 Transition Path
Document how to get from before to after:
- **Migration Strategy**: Gradual vs. big-bang approach
- **Compatibility**: Maintain backward compatibility?
- **Rollback Plan**: How to rollback if needed
- **Parallel Running**: Run old and new systems together?
- **Data Migration**: How existing data moves
- **Timeline**: Phases and dependencies

#### 2.5.4 Visual Documentation Standards

Use consistent formats:
- **Mermaid Diagrams** (markdown-native):
  - `graph TD` for architecture
  - `sequenceDiagram` for workflows
  - `stateDiagram` for state machines
  - `flowchart` for decision trees

- **ASCII Art** (simple, version-control friendly):
  - Text boxes and arrows
  - Show component relationships
  - Easy to diff in git

- **PlantUML** (if supported):
  - UML diagrams
  - C4 model diagrams
  - High-fidelity visuals

Example structure:
```markdown
## Current Architecture (Before)

### Issues
- Multiple unrelated concerns in single service
- N+1 database queries
- Tight coupling between data layer and API
- Difficult to test

### Diagram
[Mermaid: Current system structure]

## Proposed Architecture (After)

### Improvements
- Separated concerns (domain logic, data access, API)
- Batch loading for related data
- Repository pattern for data access
- Easier to test each layer independently

### Diagram
[Mermaid: New system structure]

## Transition Path
1. Create new data access layer (backward compatible)
2. Migrate queries to use batch loading
3. Refactor service to use repositories
4. Update tests
5. Deploy and monitor
```

#### 2.5.5 Before/After Comparison Template

Create side-by-side comparison:

```markdown
## Before & After Comparison

| Aspect | Before | After | Improvement |
|--------|--------|-------|-------------|
| Query Pattern | N+1 queries | Single batch query | 95% fewer queries |
| Response Time | 500ms (p95) | 50ms (p95) | 10x faster |
| Database Connections | 100+ per request | <5 per request | Connection pool stability |
| Test Coverage | 45% | 85% | Better reliability |
| Maintainability | Hard to modify | Easy to extend | 50% faster feature dev |
| Scalability | Fails at 1K users | Handles 100K users | 100x improvement |
| Code Structure | Monolithic | Modular | Better separation of concerns |
```

### Phase 3: Solution Design

#### 3.1 Brainstorm Multiple Approaches
- Generate 3+ potential solutions (not just the obvious one)
- Include conventional and unconventional approaches
- Consider different levels of change (minimal vs. comprehensive)
- Don't dismiss ideas too early

#### 3.2 Evaluate Each Approach
For each solution, assess:
- **Feasibility**: Can it be built with current tech/skills?
- **Complexity**: How complex is implementation and maintenance?
- **Performance**: Does it meet performance requirements?
- **Scalability**: Will it handle future growth?
- **Risk**: What could go wrong? How recoverable?
- **Maintenance**: How hard is it to maintain/debug/extend?
- **Cost**: Time, resources, infrastructure?
- **Dependencies**: What else needs to change?

#### 3.3 Document Trade-offs Matrix
Create comparison showing each solution against criteria:

```
| Criteria | Solution A | Solution B | Solution C |
|----------|-----------|-----------|-----------|
| Dev Time | 2 days | 1 week | 1 day |
| Perf     | Excellent | Good | Fair |
| Complex  | Moderate | High | Low |
| Maintain | Easy | Hard | Easy |
| Risk     | Low | Medium | Low |
```

#### 3.4 Design Chosen Solution
Detailed design including:
- **Architecture**: How components interact
- **Data Flow**: How data moves through system
- **API/Contracts**: Interfaces and boundaries
- **Error Handling**: Failure modes and recovery
- **Edge Cases**: Boundary conditions
- **Performance**: Expected characteristics
- **Monitoring**: How will we observe it works?

#### 3.5 Identify Risks & Mitigation
- **Technical Risks**: Technology may not work as expected
  - Mitigation: Spike/proof of concept first
- **Integration Risks**: Connecting to other systems
  - Mitigation: Plan integration points carefully
- **Performance Risks**: May not meet performance requirements
  - Mitigation: Benchmark and load test early
- **Maintenance Risks**: Team may struggle maintaining solution
  - Mitigation: Documentation, training, simplicity
- **Timeline Risks**: May take longer than estimated
  - Mitigation: Break into smaller phases, prioritize

### Phase 4: Validation

#### 4.1 Validate Assumptions
- List all assumptions made in solution design
- Which are critical? (Will solution fail if wrong?)
- How can we verify assumptions?
- What's our contingency if wrong?

Example assumptions:
- "API response time <100ms" → Validate with actual API calls
- "Team has GraphQL experience" → Check; may need training
- "Database supports this schema" → Verify with test data

#### 4.2 Check for Edge Cases
- What happens with:
  - Empty inputs?
  - Extremely large inputs?
  - Concurrent requests?
  - Network failures?
  - Database downtime?
  - Invalid data?
  - Malicious inputs?

#### 4.3 Review with Stakeholders
- Does this solve the problem?
- Does this fit with system architecture?
- Are there concerns or alternative ideas?
- Is this aligned with business goals?
- Do we have buy-in to proceed?

#### 4.4 Spike/Proof of Concept
For risky or novel solutions:
- Build minimal prototype
- Prove critical assumptions
- Measure key metrics
- Identify actual pain points
- Learn before committing to full solution

### Phase 5: Implementation Planning

#### 5.1 Break into Phases
- Identify phases for large solutions
- What's the MVP (minimum viable product)?
- What can be done independently?
- What are dependencies between phases?

Example:
1. Phase 1: Basic caching layer (2 weeks)
2. Phase 2: Cache invalidation strategy (1 week)
3. Phase 3: Monitoring and alerting (3 days)

#### 5.2 Define Success Metrics
- How will we measure if solution worked?
- What are acceptable thresholds?
- How will we monitor in production?
- What's the rollback strategy?

#### 5.3 Create Implementation Checklist
- What needs to be built?
- What tests are needed?
- What documentation is required?
- What monitoring/observability?
- What training needed?
- What deployment steps?

#### 5.4 Identify Dependencies & Blockers
- What other work is needed?
- Are there blocked by other teams?
- Do we need resources/approvals?
- Timeline realism?

## Solution Design Templates

### Standard Solution Template

```markdown
## Problem Statement
[Clear description of what needs solving]

## Success Criteria
- [ ] Specific, measurable success criteria
- [ ] Performance targets if relevant
- [ ] Acceptance criteria

## Current State
[Current architecture, pain points, what doesn't work]

## Proposed Solution
[High-level description of approach]

### Design Details
- **Architecture**: [How components interact]
- **Data Flow**: [How data moves]
- **API**: [Interfaces and contracts]
- **Edge Cases**: [Handled scenarios]

### Trade-offs Analyzed
| Criteria | This Solution | Alternative A | Alternative B |
|----------|---------------|---------------|---------------|
| Effort | X days | Y days | Z days |
| Performance | Good | Better | Fair |
| Complexity | Moderate | Low | High |
| Risk | Low | High | Medium |

### Risks & Mitigation
- **Technical Risk**: [Risk] → [Mitigation]
- **Performance Risk**: [Risk] → [Mitigation]

### Implementation Plan
1. Phase 1: [What] ([Timeline])
2. Phase 2: [What] ([Timeline])
3. Phase 3: [What] ([Timeline])

### Assumptions
- [Assumption 1 - Verification: How we'll confirm]
- [Assumption 2 - Verification: How we'll confirm]

### Success Metrics
- [Metric 1]: [Target]
- [Metric 2]: [Target]
```

### Brownfields Solution Template
Use this template when modifying or replacing existing systems:

```markdown
## Problem Statement
[Clear description of what needs solving in brownfields area]

## Current State Analysis

### Architecture
[Describe current system structure]

\`\`\`mermaid
graph TD
    A[Component A] -->|Current Flow| B[Component B]
    B --> C[Component C]
    
    style A fill:#ffcccc
    style C fill:#ffcccc
    
    Note: Red = Problem areas
\`\`\`

### Pain Points
- [Pain Point 1]: [Impact]
- [Pain Point 2]: [Impact]
- [Pain Point 3]: [Impact]

### Current Metrics
- Performance: [Current baseline - p95 latency, throughput, etc.]
- Scalability: [Current limits - concurrent users, data volume, etc.]
- Reliability: [Error rates, uptime, recovery time, etc.]
- Maintainability: [Code quality score, test coverage, etc.]

### Data Flow (Current)
\`\`\`mermaid
sequenceDiagram
    actor User
    participant API
    participant Service
    participant DB
    
    User->>API: Request
    Note over API,Service: Current issue: N+1 queries
    loop For each item
        Service->>DB: Query related data
    end
    DB-->>Service: Data
    Service-->>API: Response
    API-->>User: Result
\`\`\`

## Proposed Solution

### Architecture (After)
[Describe improved system structure]

\`\`\`mermaid
graph TD
    A[Component A - Refactored] -->|Improved Flow| B[Component B - New]
    B --> C[Component C - Optimized]
    
    style A fill:#ccffcc
    style B fill:#ccffcc
    style C fill:#ccffcc
    
    Note: Green = Improvements
\`\`\`

### Key Improvements
- [Improvement 1]: [How it's better]
- [Improvement 2]: [How it's better]
- [Improvement 3]: [How it's better]

### Expected Metrics
- Performance: [Target - p95 latency, throughput]
- Scalability: [Target - concurrent users, data volume]
- Reliability: [Target - error rates, uptime]
- Maintainability: [Target - code quality, test coverage]

### Data Flow (After)
\`\`\`mermaid
sequenceDiagram
    actor User
    participant API
    participant Service
    participant Repository
    participant DB
    
    User->>API: Request
    API->>Service: Process
    Note over Service,Repository: Single batch query
    Service->>Repository: Get with relations
    Repository->>DB: Batch query
    DB-->>Repository: All data at once
    Repository-->>Service: Hydrated objects
    Service-->>API: Response
    API-->>User: Result
\`\`\`

## Before & After Comparison

| Aspect | Before | After | Improvement |
|--------|--------|-------|-------------|
| [Metric 1] | [Value] | [Value] | [% or X improvement] |
| [Metric 2] | [Value] | [Value] | [% or X improvement] |
| [Metric 3] | [Value] | [Value] | [% or X improvement] |
| [Metric 4] | [Value] | [Value] | [% or X improvement] |

## Migration Strategy

### Approach: [Gradual/Big-Bang/Parallel]

### Phase 1: [Name] ([Timeline])
- Backward compatible changes
- Activate: Feature flag off
- What: [Describe work]
- Validate: [How to verify]

### Phase 2: [Name] ([Timeline])
- Migrate data if needed
- Activate: Feature flag on for 10% of traffic
- What: [Describe work]
- Validate: [How to verify]

### Phase 3: [Name] ([Timeline])
- Gradual rollout
- Activate: Feature flag on for 100% of traffic
- What: [Describe work]
- Validate: [How to verify]

### Rollback Plan
- If [condition], rollback to [previous state]
- Timeline: [How quickly can we rollback?]
- Data: [How do we handle data consistency?]
- Communication: [Who needs to know?]

## Code Structure Comparison

### Before
```
/src
  service/
    PaymentService.ts    ← Multiple concerns
    └─ queries
    └─ validation
    └─ external calls
    └─ logging
```

### After
```
/src
  domain/
    Payment/              ← Domain logic only
      Payment.ts
      PaymentValidator.ts
  
  data/
    PaymentRepository.ts  ← Data access
    
  api/
    PaymentService.ts     ← Orchestration
  
  external/
    PaymentGateway.ts    ← External integration
```

## Risks & Mitigation

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| [Risk 1] | High/Med/Low | High/Med/Low | [Plan] |
| [Risk 2] | High/Med/Low | High/Med/Low | [Plan] |
| [Risk 3] | High/Med/Low | High/Med/Low | [Plan] |

## Success Metrics & Monitoring

### Implementation Success
- [ ] All tests pass (unit, integration, e2e)
- [ ] Code review approved
- [ ] Zero production errors during rollout
- [ ] Performance meets targets

### Production Monitoring
- **Latency**: P50/P95/P99 response times (target: [X]ms)
- **Throughput**: Requests per second (target: [X] req/s)
- **Error Rate**: Error percentage (target: <[X]%)
- **Resource Usage**: CPU, memory, connections (target: [X])

### Rollback Triggers
- Error rate > [X]%
- P95 latency > [X]ms
- CPU usage > [X]%
- Database connection pool exhausted

## Assumptions
- [Assumption 1] - Verification: [How we'll confirm]
- [Assumption 2] - Verification: [How we'll confirm]

## Dependencies & Blockers
- [ ] [Dependency 1]
- [ ] [Dependency 2]
- [ ] [Blocker 1] - Impact: [Timeline impact]
```

## Common Pitfalls to Avoid

### Design Pitfalls
- ❌ **Not Enough Options**: Only considering obvious solution
  - Fix: Brainstorm 3+ approaches before choosing
  
- ❌ **Premature Optimization**: Optimizing for scenario that doesn't exist
  - Fix: Measure first; optimize what's actually slow
  
- ❌ **Over-Engineering**: Solution more complex than problem warrants
  - Fix: Simplest solution that solves problem; avoid "might need someday"
  
- ❌ **Ignoring Constraints**: Designing without considering real constraints
  - Fix: Explicitly list constraints; design within them
  
- ❌ **Hidden Assumptions**: Assumptions not surfaced or verified
  - Fix: Explicitly document assumptions; validate them

### Validation Pitfalls
- ❌ **Insufficient Edge Cases**: Not considering failure modes
  - Fix: Systematically consider boundary conditions
  
- ❌ **No Risk Assessment**: Assuming solution will work without testing
  - Fix: Identify risks; create mitigation strategies
  
- ❌ **Skipping Stakeholder Review**: Building in wrong direction
  - Fix: Get buy-in before building
  
- ❌ **Not Measuring**: Claiming success without proof
  - Fix: Define metrics upfront; measure everything

## When to Do Deep Solutioning

### Do Deep Solutioning For:
- ✅ Major architectural decisions
- ✅ High-risk technical changes
- ✅ Solutions affecting multiple teams/systems
- ✅ Performance-critical paths
- ✅ Security-sensitive functionality
- ✅ Decisions with long-term implications
- ✅ Unfamiliar or novel territory

### Quick Solutioning Is Fine For:
- ✅ Small bug fixes
- ✅ Well-understood problems with obvious solutions
- ✅ Isolated changes
- ✅ Low-risk refactorings
- ✅ Incremental improvements

## Deliverables

A completed solutioning should produce:
1. **Problem Definition**: Clear statement of what needs solving
2. **Requirements**: Explicit success criteria
3. **Design Document**: Detailed solution design with diagrams if helpful
4. **Trade-off Analysis**: Evaluated alternatives with pros/cons
5. **Risk Assessment**: Identified risks and mitigation strategies
6. **Implementation Plan**: Phased approach with timeline
7. **Validation Strategy**: How we'll verify it works
8. **Documentation**: For team reference and future

## Comprehensive Checklist

### Core Solutioning
- [ ] Problem clearly defined and understood
- [ ] Root cause identified (not just symptoms)
- [ ] Multiple solution approaches considered (3+)
- [ ] Trade-offs explicitly analyzed with matrix
- [ ] Risks identified and mitigated with specific plans
- [ ] Assumptions documented and verification plan created
- [ ] Edge cases considered and handled
- [ ] Stakeholder review completed with buy-in
- [ ] Success metrics defined and measurable
- [ ] Implementation plan created with phases
- [ ] Dependencies and blockers identified
- [ ] Team has expertise or training plan

### Brownfields-Specific (for modifying existing systems)
- [ ] Current state architecture documented with diagrams
- [ ] Before state pain points clearly annotated
- [ ] Current metrics/baseline measured
- [ ] Current data flow captured with sequence diagrams
- [ ] Proposed architecture documented with diagrams
- [ ] After state improvements highlighted
- [ ] Expected metrics defined (targets)
- [ ] New data flow documented with sequence diagrams
- [ ] Before/After comparison table created
- [ ] Migration strategy selected (gradual/big-bang/parallel)
- [ ] Phased approach designed with feature flags
- [ ] Backward compatibility approach defined
- [ ] Data migration plan documented
- [ ] Rollback strategy documented with triggers
- [ ] Code structure comparison shown (before/after)

### Implementation & Deployment
- [ ] Solution aligned with overall architecture
- [ ] Rollback/recovery strategy planned
- [ ] Monitoring/observability designed with metrics
- [ ] Alerting and rollback triggers defined
- [ ] Feature flag strategy for progressive rollout
- [ ] Documentation plan created
- [ ] Team ready to execute
- [ ] Timeline realistic and dependencies mapped
