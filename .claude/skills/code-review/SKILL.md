---
name: code-review
description: Review code for quality, security, performance, and best practices. Use when reviewing pull requests, analyzing code changes, checking for bugs, or ensuring code quality standards.
allowed-tools: Read, Grep, Glob, Bash(git diff:*), Bash(git log:*)
---

# Code Review Skill

Perform comprehensive code reviews focusing on quality, security, and maintainability.

## Instructions

When reviewing code:

1. **Understand Context**
   - Read the changed files completely
   - Understand the purpose of changes
   - Check related files for context
   - Review commit messages

2. **Code Quality**
   - Check naming conventions (descriptive variable names)
   - Review code organization and structure
   - Look for code duplication
   - Verify consistency with project patterns
   - Check for proper error handling

3. **Security**
   - Check for common vulnerabilities (XSS, SQL injection, etc.)
   - Verify input validation
   - Check for hardcoded secrets or credentials
   - Review authentication/authorization logic
   - Ensure sensitive data is properly handled

4. **Performance**
   - Identify inefficient algorithms or loops
   - Look for memory leaks or resource waste
   - Check for unnecessary computations
   - Review database query efficiency
   - Suggest caching strategies where appropriate

5. **Testing**
   - Verify test coverage for new code
   - Check that tests are meaningful
   - Ensure edge cases are covered
   - Verify error cases are tested

6. **Documentation**
   - Check that complex logic is documented
   - Verify public APIs have documentation
   - Ensure README is updated if needed

## Output Format

Structure your review as:

### Summary
Brief overview of changes and overall assessment.

### Issues Found

#### Critical
- Issues that must be fixed (security, bugs, breaking changes)

#### Major
- Issues that should be fixed (performance, maintainability)

#### Minor
- Suggestions for improvement (style, optimization)

### Positive Observations
Highlight good practices and quality code.

### Recommendations
Specific, actionable suggestions for improvement.

## Examples

### Example 1: PR Review
User: "Review this pull request"
Steps:
1. Get git diff to see changes
2. Read modified files
3. Check for common issues
4. Provide structured feedback

### Example 2: Security Review
User: "Check this authentication code for security issues"
Steps:
1. Read the authentication code
2. Check for common auth vulnerabilities
3. Verify password handling
4. Check session management
5. Provide security-focused feedback

## Checklist

- [ ] Code follows project conventions
- [ ] Descriptive variable and function names used
- [ ] No security vulnerabilities present
- [ ] Error handling is comprehensive
- [ ] Performance is acceptable
- [ ] Tests cover new functionality
- [ ] Documentation is updated
- [ ] No code duplication
- [ ] Changes are focused and atomic
