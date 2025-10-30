# Agent Guidelines

Focused task guidelines for specialized agents handling specific software engineering tasks. Each agent has clear responsibilities, best practices, evidence-based techniques, and comprehensive checklists.

These agents are available as Claude Code subagents in `~/.claude/agents/` and can be invoked to handle specialized tasks.

**Reference**: [Augmented Coding Patterns - Focused Agent](https://lexler.github.io/augmented-coding-patterns/patterns/focused-agent/)

## 🚀 Quick Start (TL;DR)

```bash
# Start Claude Code
claude

# In the session, view available agents
/agents

# Select an agent and describe your task
# Agent will follow its specialized guidelines
```

That's it! The agent will handle your task using evidence-based best practices.

## Full Usage Guide

### 1. Load an Agent in Claude Code

Start a Claude Code session:
```bash
claude
```

In the session, type `/agents` to see all available agents:
```
/agents
```

You'll see a list of agents to choose from. Select the agent you need for your task.

### 2. Invoke an Agent for a Specific Task

Once in a Claude Code session, you can reference agents in your prompts:
```
Use the Test Creation Agent to write comprehensive tests for the payment processor.
```

Or directly invoke with `/agents` and select the agent, then describe your task.

### 3. Agent Location

Agents are stored at: `~/.claude/agents/`

They're available globally across all your projects.

## Available Agents

### [Solutioning Agent](solutioning-agent.md)
**Analyze problems deeply and design comprehensive solutions** - Frame problems correctly, research approaches, design with documented trade-offs, validate before implementation.

### [Test Creation Agent](test-creation-agent.md)
**Generate comprehensive, high-quality test suites** - Cover happy paths, edge cases, errors; use mutation testing and property-based testing; achieve meaningful coverage (80-90%).

### [Test Review & Coverage Agent](test-review-agent.md)
**Critically evaluate test effectiveness and quality** - Assess coverage gaps, mutation scores, flaky tests; identify brittle tests and over-mocking; recommend improvements with business impact.

### [Code Review Agent](code-review-agent.md)
**Perform thorough code review with architectural focus** - Verify logic and security; check SOLID principles; assess architectural impact; provide 5-6 focused comments; 24-hour SLA.

### [Commit Readiness Agent](commit-readiness-agent.md)
**Verify code meets all quality gates** - Tests, linting, types, formatting; secrets scanning; Conventional Commits; pre-commit hooks automation; CI/CD gate integration.

### [Refactoring Agent](refactoring-agent.md)
**Improve code structure while preserving functionality** - Use code smells as signals; track cyclomatic complexity; apply refactoring patterns; measure and document improvements.

### [Documentation Agent](documentation-agent.md)
**Create maintainable documentation synchronized with code** - Keep docs in sync with code; link to specific locations; provide realistic examples; ensure accessibility; avoid anti-patterns.

### [Debugging Agent](debugging-agent.md)
**Systematically find and fix bugs using scientific method** - Reproduce consistently; form and test hypotheses; use structured logging and observability; document findings for team learning.

## Structure of Each Guideline

Each guideline document includes:
- **Purpose**: Clear statement of what the agent does
- **Key Responsibilities**: Primary duties and focus areas
- **Core Principles**: Foundational approaches and philosophies
- **Process/Techniques**: Detailed methods and workflows
- **Best Practices**: Evidence-based recommendations
- **Tools & Automation**: Relevant tools and technologies
- **Common Anti-Patterns**: Pitfalls and what to avoid
- **Comprehensive Checklist**: Verification items before completion

## Key Features of These Guidelines

### Evidence-Based
- Research-backed best practices (not just opinions)
- Industry standards and proven approaches
- Modern tools and methodologies (2024-2025)
- Trade-offs clearly documented

### Practical
- Actionable steps and concrete examples
- Real-world scenarios
- Tool recommendations with rationale
- Applicable to different tech stacks

### Comprehensive
- Cover both happy path and edge cases
- Include common pitfalls to avoid
- Detail anti-patterns to watch for
- Provide templates and checklists

### Collaborative
- Designed for team use
- Include communication approaches
- Consider multiple expertise levels
- Support pair programming and pair review

## Detailed Usage Guide

### Using Agents in Claude Code Sessions

#### Option 1: Use `/agents` Command
```bash
claude
/agents
```
Select the agent from the menu. You can then describe your task and the agent will follow its specialized guidelines.

#### Option 2: Reference Agent in Your Prompt
```bash
claude
```
Then in the session:
```
Use the Code Review Agent to review this PR: [paste code]
```

#### Option 3: Load Agent with Specific Instructions
```bash
claude
/agents
# Select Test Creation Agent
Write tests for the user authentication module with focus on edge cases.
```

### Example Workflows

#### Writing Tests
```
1. Run: claude
2. Type: /agents
3. Select: Test Creation Agent
4. Ask: "Write comprehensive tests for the payment validation function"
5. Agent will: 
   - Analyze the code
   - Identify all code paths
   - Create tests using AAA pattern
   - Achieve 80-90% coverage
   - Include edge cases and error scenarios
```

#### Code Review
```
1. Run: claude
2. Type: /agents
3. Select: Code Review Agent
4. Paste: The code to review
5. Agent will:
   - Check SOLID principles
   - Verify security
   - Provide 5-6 focused comments
   - Assess architectural impact
```

#### Debugging Issues
```
1. Run: claude
2. Type: /agents
3. Select: Debugging Agent
4. Describe: The bug and symptoms
5. Agent will:
   - Form hypotheses
   - Suggest structured debugging
   - Recommend logging strategy
   - Help root cause analysis
```

#### Refactoring Code
```
1. Run: claude
2. Type: /agents
3. Select: Refactoring Agent
4. Show: The code to refactor
5. Agent will:
   - Identify code smells
   - Track cyclomatic complexity
   - Suggest refactoring patterns
   - Measure improvements
```

### In Team Processes
1. Reference agents in pull request templates
2. Use agent checklists in code review process
3. Link to relevant agent when discussing approach
4. Train team on agent frameworks

### Customization for Your Project
These agents are comprehensive. Customize by:
- Adding project-specific conventions to agent prompts
- Adjusting quality thresholds (e.g., coverage targets)
- Including project-specific tools and frameworks
- Adding team-specific standards and practices

### Evolution
- Update agents as standards evolve
- Share learnings from actual project experience
- Add new agents as specialized needs arise
- Refine existing agents based on experience

## Integration & Workflow

### Example Workflow
1. **Solutioning Agent** - Design solution for new feature
2. **Refactoring Agent** - Improve existing code in that area
3. **Code Creation** - Implement the solution
4. **Test Creation Agent** - Write comprehensive tests
5. **Code Review Agent** - Review code before merge
6. **Commit Readiness Agent** - Verify everything before committing
7. **Documentation Agent** - Write/update docs
8. **Debugging Agent** - Fix any issues found later

### Key Success Factors
1. Agents specialize in specific tasks
2. Guidelines are referenced explicitly in work
3. Checklists are used before sign-off
4. Guidelines are kept current with team standards
5. Different agents collaborate naturally on complex work
6. Team gets training on guideline approaches
7. Guidelines become part of team culture

## Philosophy

These guidelines embody several principles:
- **Quality Over Quantity**: Meaningful results matter more than metrics
- **Systematic Over Intuitive**: Structured approaches catch more issues
- **Prevention Over Correction**: Good design prevents expensive rework
- **Collaboration Over Gatekeeping**: Guidelines enable better teamwork
- **Evidence Over Opinion**: Recommendations based on research and experience
- **Practical Over Perfect**: Good enough that works beats perfect that doesn't
- **Continuous Learning**: Share findings and update guidelines based on learnings
