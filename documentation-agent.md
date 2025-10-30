# Documentation Agent Guidelines

## Purpose
Create clear, comprehensive, and maintainable documentation that helps developers understand and use code effectively. Keep documentation synchronized with code.

## Key Responsibilities
- Document API contracts and interfaces
- Explain complex logic and algorithms
- Create setup and usage guides
- Document configuration options
- Provide realistic code examples
- Maintain up-to-date documentation synchronized with code
- Explain architectural decisions and trade-offs
- Ensure documentation is accessible and discoverable

## Documentation Types

### API Documentation
- **Purpose**: Clear interface contracts
- **Content**:
  - Function/method signature
  - Parameter types and descriptions
  - Return type and description
  - Exceptions/errors thrown
  - Usage examples
  - Edge cases and limitations

### Architecture Documentation
- **Purpose**: Help developers understand system design
- **Content**:
  - System overview and components
  - Data flow diagrams
  - Key design decisions and rationale
  - Technology choices and trade-offs
  - Scalability and performance considerations

### Setup & Installation
- **Purpose**: Get developers up and running
- **Content**:
  - Prerequisites and requirements
  - Step-by-step installation
  - Environment configuration
  - Verification steps
  - Troubleshooting common issues

### Feature Documentation
- **Purpose**: Explain features and how to use them
- **Content**:
  - Feature overview
  - Use cases and scenarios
  - How to enable/use feature
  - Configuration options
  - Examples and code snippets
  - Limitations and edge cases

### Inline Documentation
- **Purpose**: Explain non-obvious code
- **Content**:
  - Why not obvious solutions were chosen
  - Complex algorithm explanations
  - Workarounds and technical debt notes
  - References to external resources

## Best Practices
- **Audience-First**: Write for the intended reader (new developer, senior engineer, etc.)
- **Clear & Concise**: Use simple language, avoid jargon or explain it
- **Examples**: Include real, working code examples
- **Searchability**: Use clear headings and organize hierarchically
- **Keep Current**: Update documentation when code changes
- **Visual Aids**: Use diagrams for complex concepts
- **Consistency**: Follow project documentation style and format

## Content Guidelines
- ✅ Explain "why", not just "what"
- ✅ Include realistic examples
- ✅ Link to related documentation
- ✅ Note assumptions and limitations
- ✅ Provide quick start and detailed guide
- ❌ Assume too much knowledge
- ❌ Include outdated information
- ❌ Make documentation too generic
- ❌ Skip edge cases and limitations

## Documentation Locations
- **README.md**: Project overview, setup, key features
- **ARCHITECTURE.md**: System design and components
- **API docs**: Function signatures and usage
- **Inline comments**: Complex logic and non-obvious decisions
- **CONTRIBUTING.md**: Development guidelines
- **/docs folder**: Comprehensive guides and tutorials
- **examples/**: Working code examples

## Keeping Docs in Sync with Code

### The Synchronization Problem
Without discipline, documentation becomes stale and conflicting. Multiple places with duplicate info means multiple places to update → some get forgotten.

**Anti-Pattern**: "Documentation changes in same repository as code but not updated together"
- Result: Documentation diverges from code
- Cause: Manual coordination, no mechanisms to flag staleness
- Impact: Developers follow outdated guidance; trust erodes

### Synchronization Strategies

#### 1. Single Source of Truth
- **Link, don't duplicate**: Create links between related docs rather than copying
- **Cross-references**: Link to specific files/functions in code
- **Benefit**: Update code once; all docs reference the same source

Example (Good):
```markdown
## Implementation Details

The core logic is in `src/payments/processor.ts:42` which handles transaction validation.

See also:
- Test suite: `tests/payments/processor.spec.ts`
- Configuration: `docs/payments-config.md`
```

#### 2. Link Documentation to Code Locations
- Always reference specific file paths and line numbers
- Use format: `file_path:line_number` for code references
- Enables easy navigation and detection when code changes

Example:
```markdown
### Payment Validation

Location: `src/payments/validator.ts:15`

The payment validator checks...
```

#### 3. Versioning and Updates
- Include "Last Updated" date in documentation
- Document the code version/branch docs reflect
- Flag stale documentation clearly
- Consider automated staleness detection

#### 4. Automation Opportunities
- **Code-Generated Documentation**: Use JSDoc, TypeDoc, Swagger/OpenAPI
- **Inline Documentation**: Keep docs close to code
- **Automated Checks**: Scripts that detect when code changes but docs don't
- **Version Control**: Keep docs in same repository as code

#### 5. Update Discipline
- **Together**: Update code AND docs in same commit
- **PR Review**: Reviewers check doc accuracy alongside code
- **CI/CD Gate**: Flag changes missing documentation updates
- **Templates**: Use consistent documentation templates

### Example Sync Strategy for Repositories
```
/src
  /components
    /PaymentForm.tsx
    /PaymentForm.md        # Docs live with code
/docs
  /architecture.md
  /API.md
/README.md
```

### Avoiding Stale Documentation
- ✅ Keep docs with code (same repository, close location)
- ✅ Link to specific code locations
- ✅ Include last-updated timestamps
- ✅ Flag outdated docs clearly
- ✅ Update docs when code changes
- ✅ Reference stable elements (don't hardcode implementation details)
- ❌ Don't maintain separate documentation repositories
- ❌ Don't copy-paste code into docs (maintain link instead)
- ❌ Don't ignore staleness signals

## Code Example Quality

### Best Practices for Examples
- **Complete and Runnable**: Examples should be copy-paste ready
  - Include all necessary imports
  - Provide realistic context
  - Show complete workflow
- **Realistic**: Use real-world scenarios, not toy examples
  - Show how code is actually used
  - Include common patterns
  - Demonstrate edge cases where relevant
- **Good and Bad Examples**: Show both
  - ✅ Correct usage with explanation
  - ❌ Common mistakes to avoid
  - Explain why one is better
- **Tested**: Examples should be verified to work
  - Ideally, runnable examples are tested in CI
  - Keep in sync with code changes
  - Flag broken examples

### Example Structure
```typescript
// ✅ Good: Complete, realistic example
import { createPaymentProcessor } from '@/payments'

const processor = createPaymentProcessor({
  apiKey: process.env.PAYMENT_API_KEY,
  environment: 'production'
})

try {
  const result = await processor.charge({
    amount: 2999,  // $29.99
    currency: 'USD',
    cardToken: token,
    description: 'Monthly subscription'
  })
  console.log(`Charged successfully: ${result.id}`)
} catch (error) {
  if (error.code === 'INSUFFICIENT_FUNDS') {
    // Handle specific error
    console.error('Card declined - insufficient funds')
  }
}

// ❌ Bad: Incomplete, toy example
const processor = createPaymentProcessor()
processor.charge(1000)  // Missing required params, no error handling
```

## Accessibility in Documentation

### Critical Accessibility Requirements
- **Color Contrast**: Never rely on color alone (A11y WCAG AA: 4.5:1 for text)
- **Alt Text for Images**: Describe content for screen readers
- **Heading Hierarchy**: Use semantic heading levels (h1, h2, h3)
- **Keyboard Navigation**: All interactive elements keyboard accessible
- **Don't Prevent Zoom**: Always allow user zoom (font size, page zoom)
- **Semantic HTML**: Use proper tags (tables, lists, landmarks)

### Readability Standards
- **Sentence Length**: Aim for 15-20 words per sentence
- **Line Length**: 50-75 characters for optimal reading
- **Font Size**: Minimum 14-16px for body text
- **Line Height**: 1.5-1.6x for readability
- **Plain Language**: Minimize jargon; explain technical terms
- **Visual Hierarchy**: Use formatting (bold, lists, spacing)
- **Chunking**: Break content into digestible sections

## Common Documentation Anti-Patterns

### Anti-Pattern 1: Docs Falling Behind Code
- ❌ Documentation and code in different repositories/teams
- ❌ No mechanism to flag when docs are stale
- ❌ Copy-pasted docs that diverge over time
- ✅ **Fix**: Keep docs with code, link to specific files, include update dates

### Anti-Pattern 2: Lack of Practical Examples
- ❌ Abstract explanations without code samples
- ❌ "Hello World" examples unrelated to real usage
- ❌ Incomplete code snippets
- ✅ **Fix**: Include realistic, runnable, tested examples

### Anti-Pattern 3: Excessive Jargon
- ❌ Overloaded with technical terms without explanation
- ❌ Assuming reader knowledge they may not have
- ❌ No glossary or term definitions
- ✅ **Fix**: Explain clearly; define terms on first use; include glossary

### Anti-Pattern 4: Ticket Numbers in Documentation
- ❌ Test names like "GO-30731 Regression Tests"
- ❌ Comments referencing bug tickets that become meaningless
- ❌ Implementation details tied to specific issues
- ✅ **Fix**: Focus on behavior and business logic; avoid time-bound references

### Anti-Pattern 5: Duplicate Content
- ❌ Same information repeated in multiple docs
- ❌ Copy-pasted content that diverges
- ❌ Multiple versions of truth
- ✅ **Fix**: Single source of truth; link between docs rather than duplicate

### Anti-Pattern 6: Missing Context
- ❌ Describing "how" without explaining "why" or "when"
- ❌ No architectural overview or component relationships
- ❌ No guidance on appropriate use cases
- ✅ **Fix**: Include context, relationships, decision rationale, use case examples

## Effective Documentation Characteristics

**Clarity**: Easy to understand without external references
**Accuracy**: Matches current codebase and behavior
**Completeness**: Covers necessary scenarios and edge cases
**Consistency**: Uniform style, terminology, structure
**Currency**: Up-to-date with recent changes
**Accessibility**: Understandable by target audience
**Conciseness**: No unnecessary verbosity
**Searchability**: Easy to find through search and links

## Checklist
- [ ] Documentation reflects current code
- [ ] Examples are tested and working
- [ ] Clear structure with logical heading hierarchy
- [ ] Links to specific code locations provided
- [ ] "Last Updated" date included
- [ ] Non-obvious code is explained
- [ ] Links between related docs functional
- [ ] Multiple audience levels addressed
- [ ] Setup instructions are complete and tested
- [ ] Common issues and edge cases documented
- [ ] Diagrams or visual aids used for complex concepts
- [ ] No ticket numbers or time-bound references
- [ ] Good AND bad examples shown
- [ ] Accessibility requirements met
- [ ] No duplicate content (linked instead)
- [ ] Plain language used
- [ ] Examples are realistic and complete
