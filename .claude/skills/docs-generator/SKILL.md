---
name: docs-generator
description: Generate structured documentation including ADRs, task planning docs, research notes, and session summaries. Use when creating documentation, recording decisions, planning tasks, or documenting research.
allowed-tools: Read, Write, Grep, Glob, Bash(git log:*)
---

# Documentation Generator Skill

Automatically generate well-structured documentation following project standards.

## Instructions

Generate documentation in the `docs/` folder following this structure:
- `docs/prd/` - Product requirements
- `docs/decisions/` - Architecture Decision Records (ADR)
- `docs/research/` - Investigations and spikes
- `docs/tasks/` - Planning and progress logs

### Filename Convention
Use format: `YYYYMMDD-{kebab-case-title}.md`

## Document Types

### 1. Architecture Decision Record (ADR)

**When to create**: Recording significant architectural or technical decisions.

**Structure**:
```markdown
# [Decision Title]

**Date**: YYYY-MM-DD
**Status**: Proposed | Accepted | Deprecated | Superseded

## Context
What is the issue we're trying to solve? What are the constraints and requirements?

## Decision
What is the change we're making? What approach did we choose?

## Alternatives Considered
What other options did we evaluate?
- Option 1: pros/cons
- Option 2: pros/cons

## Consequences
What becomes easier or harder as a result of this decision?

### Positive
- Benefit 1
- Benefit 2

### Negative
- Trade-off 1
- Trade-off 2

## References
- Links to documentation
- Related ADRs
- Code examples
```

### 2. Research Document

**When to create**: Investigating options, comparing solutions, or exploring new technologies.

**Structure**:
```markdown
# [Research Topic]

**Date**: YYYY-MM-DD
**Researcher**: [Name/Role]

## Goal
What are we trying to learn or decide?

## Questions
- What specific questions are we investigating?
- What alternatives are we comparing?
- What criteria matter?

## Findings

### [Option/Approach 1]
- Description
- Pros
- Cons
- Key considerations

### [Option/Approach 2]
- Description
- Pros
- Cons
- Key considerations

## Data & Metrics
Relevant data, benchmarks, or measurements.

## Recommendations
Based on the research, what should we do and why?

## References
- Documentation links
- Articles
- Code examples
- Related research
```

### 3. Task Planning Document

**When to create**: Planning implementation of features, migrations, or significant changes.

**Structure**:
```markdown
# [Task Name]

**Date**: YYYY-MM-DD
**Status**: Planning | In Progress | Completed | Blocked

## Objective
What are we trying to accomplish?

## Context
- Why is this needed?
- What's the current state?
- What dependencies exist?
- What constraints apply?

## Approach

### Phase 1: [Name]
1. Step 1
2. Step 2
3. ...

### Phase 2: [Name]
1. Step 1
2. Step 2

## Technical Details
- Key files to modify
- APIs or integrations involved
- Database changes needed
- Testing strategy

## Acceptance Criteria
- [ ] Criterion 1
- [ ] Criterion 2
- [ ] Tests passing
- [ ] Documentation updated
- [ ] Code reviewed

## Risks & Mitigations
- **Risk**: Description
  - **Mitigation**: How to address it

## Timeline Estimate
Rough estimate of effort (no specific dates).

## Notes
Any additional context, decisions made during implementation, or lessons learned.
```

### 4. Session Summary

**When to create**: After complex debugging, investigation, or implementation sessions.

**Structure**:
```markdown
# Session: [Topic]

**Date**: YYYY-MM-DD
**Duration**: [Approximate time]

## Goal
What were we trying to accomplish?

## What Happened

### Initial State
Brief description of starting point.

### Actions Taken
1. First action and result
2. Second action and result
3. ...

### Key Discoveries
- Important finding 1
- Important finding 2

## Outcome
What was accomplished or learned?

## Follow-up Items
- [ ] Todo 1
- [ ] Todo 2

## References
- Files modified
- Commands run
- Documentation consulted
```

## Best Practices

1. **Use descriptive titles**: Clear, specific titles help future reference
2. **Date everything**: Always include creation date
3. **Link related docs**: Reference other ADRs, tasks, or research
4. **Update status**: Keep status fields current
5. **Be concise**: Focus on key information, avoid unnecessary details
6. **Use examples**: Include code snippets or examples where helpful
7. **Track decisions**: Document why decisions were made, not just what

## Examples

### Example 1: Creating an ADR
User: "We need to document our decision to use PostgreSQL over MongoDB"
Steps:
1. Create file: `docs/decisions/YYYYMMDD-use-postgresql-for-primary-database.md`
2. Fill in ADR structure
3. Include context about requirements
4. List alternatives considered
5. Document consequences

### Example 2: Creating Research Doc
User: "Research state management options for the React app"
Steps:
1. Create file: `docs/research/YYYYMMDD-react-state-management-comparison.md`
2. List questions to answer
3. Compare Redux, Zustand, Context, etc.
4. Include pros/cons for each
5. Provide recommendation based on project needs

### Example 3: Creating Task Plan
User: "Plan the migration to Node.js 20"
Steps:
1. Create file: `docs/tasks/YYYYMMDD-migrate-to-nodejs-20.md`
2. Define objective and context
3. Break down into phases
4. List acceptance criteria
5. Identify risks and mitigations
