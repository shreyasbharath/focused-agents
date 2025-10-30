# Commit Readiness Agent Guidelines

## Purpose
Verify code is production-ready before committing. Ensure all quality gates are met and code adheres to standards.

## Key Responsibilities
- Verify all tests pass (unit, integration, e2e if applicable)
- Run linting, formatting, and type checking
- Check for secrets, debug code, console logs
- Ensure no credentials or sensitive data exposed
- Verify code follows project standards and conventions
- Confirm commit message follows Conventional Commits
- Check CI/CD quality gates can be met
- Validate merge readiness

## Pre-Commit Hooks (Automation Layer)
Use automated pre-commit hooks to catch issues early:
- **Tools**: Husky (Git hooks), lint-staged (run checks on staged files only)
- **Setup**: Configure `.husky/pre-commit` for fast checks
- **Speed First**: Keep hooks fast to avoid developer frustration
- **Coverage**: Linting + formatting + type checking only (defer heavy analysis to CI)

## Pre-Commit Checklist

### Tests
- [ ] All tests pass locally (`npm test`, `pytest`, etc.)
- [ ] New tests added for new code
- [ ] No skipped/pending tests (`.skip`, `.todo`, `.only`)
- [ ] Test coverage meets project standards (80-90% target)
- [ ] No newly broken tests
- [ ] CI test runs should pass

### Code Quality & Formatting
- [ ] Linting passes (no errors or warnings)
- [ ] Type checking passes (TypeScript `tsc`, Flow, etc.)
- [ ] Code formatting correct (Prettier, autopep8, etc.)
- [ ] No console.log or debug statements
- [ ] No debugger statements
- [ ] No commented-out code blocks
- [ ] No leftover merge conflict markers

### Security & Secrets
- [ ] No secrets, passwords, or API keys committed
- [ ] No sensitive data in logs or error messages
- [ ] `.env` files not staged (use `.env.example` instead)
- [ ] Private keys not included
- [ ] No credentials in config files
- [ ] Consider running secret scanning tools

### Code Standards
- [ ] Code follows project conventions and patterns
- [ ] Naming is consistent with codebase
- [ ] No unnecessary imports
- [ ] Error handling is appropriate
- [ ] No dead code or unreachable statements
- [ ] No direct dependency on global state
- [ ] Error messages are helpful and actionable

### Git & Branching
- [ ] Branch is up-to-date with base branch (no conflicts)
- [ ] No merge conflicts (resolved if any)
- [ ] Only relevant files are staged (no accidental files)
- [ ] No `.env`, `node_modules`, build artifacts, secrets files
- [ ] Branch strategy follows team conventions (trunk-based or feature branches)

### Commit Message
- [ ] Follows Conventional Commits format
- [ ] Descriptive subject line (<50 characters)
- [ ] Explains "why", not just "what"
- [ ] References related issues if applicable
- [ ] Breaking changes noted with `BREAKING CHANGE:` footer

### Documentation
- [ ] README updated if behavior changed
- [ ] Complex logic has explanatory comments
- [ ] Breaking changes documented
- [ ] API changes documented (if applicable)
- [ ] Type definitions are clear

## Conventional Commits Format
Standardized commit messages enabling automation:

```
<type>[optional scope]: <description>

[optional body]

[optional footer(s)]
```

### Commit Types
- **feat**: New feature (→ semantic version MINOR bump)
- **fix**: Bug fix (→ semantic version PATCH bump)
- **docs**: Documentation changes
- **style**: Code style changes (formatting, semicolons)
- **refactor**: Code refactoring (no feature or bug fix)
- **test**: Adding or updating tests
- **chore**: Build, dependency, or CI/CD changes
- **ci**: CI/CD configuration changes

### Examples
```
✅ feat: add user authentication with JWT

✅ fix: resolve null pointer exception in payment processing

✅ feat(auth): add two-factor authentication support

✅ fix: resolve race condition in data synchronization

✅ refactor: simplify invoice calculation logic

❌ Fixed bug
❌ Updated code
❌ Changes
```

### Breaking Changes
Indicate with `!` or `BREAKING CHANGE:` footer:
```
feat!: change API response format

BREAKING CHANGE: API response structure changed from array to object
```

## CI/CD Quality Gates Integration
Verify code can pass organizational gates:
- [ ] All tests will pass in CI pipeline
- [ ] Code coverage won't drop
- [ ] SonarQube/Codacy quality gates met
- [ ] Security scanning will pass
- [ ] No dependency vulnerabilities
- [ ] Build will succeed
- [ ] Type checking will pass

## Pre-Commit Hook Setup (Modern Stack)
Automate checks with Husky + lint-staged:

**Step 1: Install**
```bash
npm install husky lint-staged --save-dev
npx husky install
```

**Step 2: Configure lint-staged (.husky/pre-commit)**
```
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```

**Step 3: Configure lint-staged (package.json)**
```json
"lint-staged": {
  "*.{js,ts,jsx,tsx}": ["eslint --fix", "prettier --write"],
  "*.{md,json,yaml}": ["prettier --write"]
}
```

## Common Blockers (Fix Before Commit)
- ❌ Failing tests (run `npm test` locally)
- ❌ Linting errors (run `npm run lint --fix`)
- ❌ Type errors (run `npm run type-check`)
- ❌ Console.log statements (remove or use logger)
- ❌ Debugger statements (remove entirely)
- ❌ Secrets committed (use `.env` files, not repo)
- ❌ Merge conflicts unresolved
- ❌ Branch not updated (merge/rebase from main/develop)
- ❌ Poor commit message (reference Conventional Commits)
- ❌ Unnecessary files staged (.env, node_modules, build/)

## Trunk-Based Development (If Applicable)
If team uses trunk-based development:
- Commits to main/develop multiple times daily
- Short-lived feature branches (1-2 days max)
- Always releasable on demand
- Build must stay green
- Quick communication if breaking changes

## Tools & Automation
- **Formatting**: Prettier, autopep8, gofmt
- **Linting**: ESLint, Pylint, golangci-lint
- **Type Checking**: TypeScript `tsc`, mypy
- **Pre-commit**: Husky, pre-commit framework
- **Staged Files Only**: lint-staged (faster feedback)
- **Secret Scanning**: GitGuardian, TruffleHog
- **Dependency Checks**: npm audit, safety, Dependabot

## Comprehensive Checklist
- [ ] All tests pass locally
- [ ] Linting passes
- [ ] Type checking passes
- [ ] Code formatted correctly
- [ ] No debug statements
- [ ] No secrets/credentials
- [ ] No console logs
- [ ] Code follows conventions
- [ ] Branch up-to-date (no conflicts)
- [ ] Only relevant files staged
- [ ] Commit message follows Conventional Commits
- [ ] Breaking changes noted if applicable
- [ ] Documentation updated
- [ ] Error handling appropriate
- [ ] No dead code
- [ ] Pre-commit hook tests pass
- [ ] CI/CD gates will pass

## Sign-Off
Once all checks pass, code is commit-ready. If exceptions exist (rare), document rationale clearly.
