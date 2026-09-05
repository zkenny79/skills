---
name: code-reviewer
description: Perform systematic, thorough code reviews. Use this skill when the user asks to review code, check a pull request, audit code quality, or evaluate code for bugs, security issues, performance problems, or style violations. Produces structured review feedback with severity levels and actionable suggestions.
---

# Code Reviewer

Perform systematic code reviews that catch real issues while respecting the author's intent. Focus on correctness, security, performance, maintainability, and consistency with existing codebase patterns.

## When to use this skill

- User asks to review code or a pull request
- User asks for a code quality audit
- User asks to check for bugs, security issues, or performance problems
- User asks to evaluate code style or architecture

## Review Process

### 1. Understand Context First

Before reviewing any code:

1. Read applicable AGENTS.md instructions; open other documentation only for concrete context gaps. Missing legacy documents are not a prerequisite for a review.
2. Understand the project's language, framework, and conventions
3. Identify the purpose of the code being reviewed
4. Check existing patterns in the codebase for consistency

### 2. Review Categories

Evaluate code across these categories in order of priority:

#### Critical (must fix)

- **Correctness**: Logic errors, off-by-one, null/undefined access, race conditions, incorrect error handling
- **Security**: Injection vulnerabilities, hardcoded secrets, insecure defaults, missing auth checks, exposed sensitive data
- **Data loss**: Unhandled failures in write operations, missing transactions, unsafe migrations

#### High (should fix)

- **Performance**: N+1 queries, missing indexes, unbounded loops, memory leaks, unnecessary re-renders, blocking operations
- **Error handling**: Swallowed errors, missing error boundaries, unclear error messages, no retry logic for transient failures
- **Concurrency**: Missing locks, deadlocks, unsynchronized shared state, unsafe async patterns

#### Medium (consider fixing)

- **Maintainability**: Unclear naming, missing documentation for complex logic, overly long functions, duplicated code
- **Testability**: Untestable code, missing test hooks, tight coupling, side effects in pure functions
- **API design**: Inconsistent interfaces, missing input validation, unclear return types, breaking changes without versioning

#### Low (nice to have)

- **Style**: Inconsistent formatting, naming convention violations, unused imports, dead code
- **Documentation**: Missing docstrings, outdated comments, unclear commit messages

### 3. Review Checklist

For each file or change set, check:

**Logic & Correctness**
- [ ] Does the code do what it claims to do?
- [ ] Are edge cases handled (empty input, null, max values, concurrent access)?
- [ ] Are error paths tested and handled properly?
- [ ] Is the control flow clear and correct?

**Security**
- [ ] Is user input validated and sanitized?
- [ ] Are there any hardcoded credentials, tokens, or secrets?
- [ ] Is authentication/authorization checked where needed?
- [ ] Are dependencies from trusted sources?
- [ ] Is sensitive data logged or exposed?

**Performance**
- [ ] Are database queries efficient (no N+1, proper indexing)?
- [ ] Are there unnecessary allocations or copies?
- [ ] Is caching used appropriately?
- [ ] Are expensive operations off the main thread?

**Maintainability**
- [ ] Are names clear and descriptive?
- [ ] Is the code DRY (no unnecessary duplication)?
- [ ] Are functions/methods focused and not too long?
- [ ] Is complex logic explained?

**Consistency**
- [ ] Does the code follow existing project patterns?
- [ ] Are naming conventions consistent with the codebase?
- [ ] Are error handling patterns consistent?
- [ ] Are testing patterns consistent?

### 4. Output Format

Structure your review as:

```markdown
# Code Review: [filename or PR title]

## Summary

Brief assessment of the overall quality and any major concerns.

## Findings

### [CRITICAL] Title of issue
- **Location**: file:line
- **Problem**: What is wrong
- **Impact**: Why it matters
- **Suggestion**: How to fix it

### [HIGH] Title of issue
...

### [MEDIUM] Title of issue
...

### [LOW] Title of issue
...

## Positive Notes

Highlight good patterns, clean solutions, or well-written code.

## Questions

List only material questions unresolved by the code, tests, and available documentation; omit this section when none remain. Identify which findings depend on an answer.
```

### 5. Review Principles

- **Be specific**: Reference exact line numbers and code snippets
- **Be constructive**: Suggest fixes, not just problems
- **Be proportional**: Don't nitpick on low-priority items if there are critical issues
- **Respect intent**: Understand what the author was trying to achieve before suggesting changes
- **Acknowledge good code**: Point out well-written sections too
- **Prioritize**: Lead with the most important issues
- **Resolve context first**: Search code, tests, and existing documentation before asking. Ask only when a remaining ambiguity could materially change the assessment. Continue reviewing independent areas and mark conclusions that cannot yet be established; do not invent the author's intent.
- **Keep review scope**: A review request authorizes assessment and findings, not source edits or runtime changes unless the user also requests them.

### 6. Language-Specific Checks

Adapt your review based on the language:

- **JavaScript/TypeScript**: Check for async/await misuse, promise handling, type safety, null checks
- **Python**: Check for type hints, mutable defaults, exception handling breadth, GIL considerations
- **Go**: Check for error handling (no ignored errors), goroutine leaks, context propagation
- **Rust**: Check for unwrap() in production code, clone() overuse, proper Send/Sync bounds
- **Java/Kotlin**: Check for null safety, resource leaks, thread safety, exception handling
- **C/C++**: Check for memory leaks, buffer overflows, undefined behavior, proper RAII
