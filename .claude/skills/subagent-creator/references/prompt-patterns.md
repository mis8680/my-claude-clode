# Sub-Agent Prompt Engineering Patterns

Effective system prompts for sub-agents follow specific patterns that improve focus, reliability, and output quality.

## Core Prompt Structure

Every sub-agent prompt should have:

```markdown
[ROLE DEFINITION]
You are a [specific role]. Your goal is to [primary objective].

[SCOPE AND BOUNDARIES]
You should:
- [Expected behavior 1]
- [Expected behavior 2]

You must NOT:
- [Forbidden action 1]
- [Forbidden action 2]

[PROCESS/METHODOLOGY]
[Step-by-step workflow or approach]

[OUTPUT FORMAT]
[Specific structure for results]

[QUALITY STANDARDS]
[What defines success]
```

## Pattern 1: The Checklist Agent

**Use case**: Tasks requiring systematic verification against criteria

**Structure**:
```markdown
You are a [role]. Your goal is to verify [what] against [standards].

## Checklist

For each [item]:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Process

1. [Step 1]
2. For each item, check all criteria
3. [Step 3]

## Output

### [Item Name]
✓ Pass | ⚠ Warning | ✗ Fail

**Findings**:
- [Criterion]: [Status] - [Details]
```

**Examples**: Code review, security audit, accessibility checker, style guide validator

**Benefits**:
- Systematic coverage
- Consistent evaluation
- Easy to verify completeness

---

## Pattern 2: The Analyzer Agent

**Use case**: Deep analysis of code, data, or systems

**Structure**:
```markdown
You are a [domain] analyst. Your goal is to understand and explain [subject].

## Analysis Framework

1. **Overview** - What is this?
2. **Components** - What are the parts?
3. **Relationships** - How do parts connect?
4. **Patterns** - What patterns are used?
5. **Issues** - What problems exist?
6. **Recommendations** - What should change?

## Output Format

### Summary
[High-level findings]

### Detailed Analysis
[Component-by-component breakdown]

### Architecture Diagram
[Text representation if applicable]

### Recommendations
[Prioritized suggestions]
```

**Examples**: Codebase analyzer, dependency analyzer, architecture reviewer

**Benefits**:
- Structured understanding
- Comprehensive coverage
- Actionable insights

---

## Pattern 3: The Generator Agent

**Use case**: Creating artifacts following templates or standards

**Structure**:
```markdown
You are a [type] generator. Your goal is to create [artifact] following [standards].

## Standards

[Specific requirements the output must meet]

## Template

[Exact structure to follow]

## Quality Checklist

Generated [artifact] must:
- [ ] [Requirement 1]
- [ ] [Requirement 2]
- [ ] [Requirement 3]

## Process

1. [Gather information]
2. [Apply template]
3. [Validate against checklist]
4. [Output result]
```

**Examples**: Documentation generator, test generator, boilerplate creator, API spec generator

**Benefits**:
- Consistent output
- Standards compliance
- Reduced variability

---

## Pattern 4: The Transformer Agent

**Use case**: Converting from one format/style to another

**Structure**:
```markdown
You are a [source] to [target] transformer. Your goal is to convert [input] into [output].

## Transformation Rules

1. [Input element A] → [Output element X]
2. [Input element B] → [Output element Y]
3. [Special case handling]

## Preservation Requirements

Maintain:
- [Aspect 1]
- [Aspect 2]

## Process

1. Parse [source format]
2. Map elements to [target format]
3. Apply transformations
4. Validate output
5. Report any loss of information

## Output

[Transformed content]

### Transformation Notes
[Any information that couldn't be preserved or required decisions]
```

**Examples**: Code migrator, format converter, API version upgrader, syntax modernizer

**Benefits**:
- Clear transformation logic
- Information preservation tracking
- Systematic conversion

---

## Pattern 5: The Orchestrator Agent

**Use case**: Coordinating multi-step workflows with decision points

**Structure**:
```markdown
You are a [domain] orchestrator. Your goal is to [high-level objective] by coordinating multiple steps.

## Workflow

1. **[Phase 1 Name]**
   - Do: [Actions]
   - Check: [Conditions]
   - If [condition]: go to [step]
   - Otherwise: [alternative action]

2. **[Phase 2 Name]**
   - Do: [Actions]
   - Decide: [Decision point]
   - Options:
     - If [case A]: [action A]
     - If [case B]: [action B]

3. **[Phase 3 Name]**
   - [Final steps]

## Decision Criteria

For [decision point]:
- [Criterion 1]: Choose [option X]
- [Criterion 2]: Choose [option Y]

## Output Format

### Execution Log
[Step-by-step record of what was done]

### Decisions Made
[What decisions were made and why]

### Results
[Final output]
```

**Examples**: CI/CD coordinator, migration orchestrator, feature implementer

**Benefits**:
- Handles complexity
- Adaptive workflow
- Clear decision trail

---

## Pattern 6: The Expert Advisor

**Use case**: Providing specialized domain knowledge and recommendations

**Structure**:
```markdown
You are a [domain] expert specializing in [specialty]. Your goal is to provide expert guidance on [topic].

## Expertise Areas

- [Area 1]: [Your knowledge/capabilities]
- [Area 2]: [Your knowledge/capabilities]

## Analysis Approach

When analyzing [subject]:
1. [First consideration]
2. [Second consideration]
3. [Third consideration]

## Recommendation Framework

Recommendations should include:
- **Option**: [What to do]
- **Rationale**: [Why this is good]
- **Tradeoffs**: [Pros and cons]
- **Implementation**: [How to do it]

## Output Format

### Assessment
[Expert evaluation of current state]

### Recommendations

#### Option 1: [Name]
**Rationale**: [Why]
**Pros**: [Benefits]
**Cons**: [Drawbacks]
**Best for**: [Use cases]

#### Option 2: [Name]
[Same structure]

### Recommended Approach
[Which option and why]
```

**Examples**: Architecture advisor, library selector, deployment strategist

**Benefits**:
- Informed decision making
- Clear tradeoffs
- Expert context

---

## Advanced Prompt Techniques

### Technique 1: Progressive Refinement

For tasks that benefit from iteration:

```markdown
## Process

1. **First Pass** - Quick analysis to identify scope
2. **Deep Dive** - Detailed examination of identified areas
3. **Synthesis** - Combine findings
4. **Refinement** - Review and improve

After each pass, pause and decide:
- Is more detail needed? → Continue deeper
- Is coverage sufficient? → Move to next phase
```

### Technique 2: Confidence Indicators

For agents that make judgments:

```markdown
## Confidence Levels

When reporting findings, include confidence:
- 🟢 **High confidence**: Clear evidence, well-established patterns
- 🟡 **Medium confidence**: Some evidence, common patterns
- 🔴 **Low confidence**: Limited evidence, unclear

Example:
- 🟢 Security vulnerability in line 42 (SQL injection)
- 🟡 Possible performance issue in line 89 (nested loops)
- 🔴 May benefit from refactoring (subjective)
```

### Technique 3: Example-Driven Instructions

Show don't just tell:

```markdown
## Output Format

Good example:
```
✓ Function `validateEmail` has comprehensive tests
  - Happy path: valid emails accepted
  - Edge cases: empty, malformed, special chars
  - Coverage: 95%
```

Bad example:
```
Function has tests. Coverage: 95%
```

Always follow the good example format.
```

### Technique 4: Explicit Priorities

When agents juggle multiple concerns:

```markdown
## Priority Order

When conflicts arise, prioritize in this order:
1. **Correctness** - Never break functionality
2. **Security** - Never introduce vulnerabilities
3. **Performance** - Optimize when safe to do so
4. **Readability** - Make code clear
5. **Brevity** - Keep code concise

Example: If a security fix makes code longer, choose security over brevity.
```

### Technique 5: Error Handling Instructions

Tell agents what to do when things go wrong:

```markdown
## Error Handling

If you encounter:

**Missing information**:
- State what's missing
- Proceed with reasonable assumptions
- Mark assumptions clearly in output

**Ambiguous requirements**:
- List possible interpretations
- Choose most common/safe interpretation
- Document the choice

**Unable to complete task**:
- Explain what blocked completion
- Report partial results
- Suggest what's needed to continue
```

---

## Anti-Patterns (Avoid These)

### ❌ Anti-Pattern 1: Vague Goals

```markdown
You are a code helper. Help with code.
```

**Problem**: No clear role, objective, or process

**Fix**: Be specific about role, goal, and methodology

### ❌ Anti-Pattern 2: Over-Specification

```markdown
You are a TypeScript React Next.js 14 App Router with TailwindCSS and Shadcn UI
using Zustand for state management and React Query for data fetching specialist...
[10 more paragraphs of technology specifics]
```

**Problem**: Too much detail drowns the core purpose

**Fix**: Focus on process and objectives, mention tech stack briefly

### ❌ Anti-Pattern 3: Missing Output Format

```markdown
You are a code reviewer. Review the code.
```

**Problem**: No guidance on what the output should look like

**Fix**: Always specify output structure and format

### ❌ Anti-Pattern 4: No Boundaries

```markdown
You are a helpful assistant. Do whatever the user asks.
```

**Problem**: Too broad, loses specialization benefits

**Fix**: Clearly define what the agent should and shouldn't do

### ❌ Anti-Pattern 5: Process-less Instructions

```markdown
You are an API documenter. Document APIs well.
```

**Problem**: No methodology for how to accomplish the goal

**Fix**: Provide step-by-step process or framework

---

## Prompt Debugging

If your sub-agent isn't working well:

### Issue: Agent misses important checks

**Solution**: Add explicit checklist
```markdown
## Required Checks

For each [item], verify:
- [ ] [Check 1]
- [ ] [Check 2]
- [ ] [Check 3]
```

### Issue: Output format is inconsistent

**Solution**: Add concrete examples
```markdown
## Output Format

Example:
```
[Exact format you want]
```

Match this format exactly.
```

### Issue: Agent goes out of scope

**Solution**: Strengthen boundaries
```markdown
You must NOT:
- [Specific out-of-scope action 1]
- [Specific out-of-scope action 2]

If asked to do these, respond: "This is outside my scope as a [role]."
```

### Issue: Agent doesn't follow process

**Solution**: Add numbered steps and checkpoints
```markdown
## Process (Follow in Order)

1. [Step 1]
   - Checkpoint: You should now have [X]

2. [Step 2]
   - Checkpoint: Verify [Y] before continuing

3. [Step 3]
```

### Issue: Quality is inconsistent

**Solution**: Add explicit quality standards
```markdown
## Quality Standards

Every output must:
- [ ] [Standard 1]
- [ ] [Standard 2]

Before returning results, verify all standards are met.
```

---

## Testing Your Prompts

### 1. Test with Edge Cases

Run your sub-agent on:
- Minimal input (nearly empty files)
- Maximum input (large, complex files)
- Ambiguous cases (unclear requirements)
- Error conditions (missing dependencies, broken code)

### 2. Test Different Domains

If your agent should work across contexts, test it on:
- Different programming languages
- Different frameworks
- Different project sizes
- Different code quality levels

### 3. Compare Outputs

Run the same task multiple times and check:
- Consistency (same findings each time?)
- Completeness (nothing missed?)
- Quality (meets your standards?)

### 4. Iterate Based on Failures

When the agent fails or produces poor output:
1. Identify what went wrong
2. Update the prompt to prevent that failure
3. Re-test to verify the fix
4. Test that fix didn't break other cases

---

## Quick Reference

### Minimal Viable Prompt

```markdown
You are a [role].
Your goal is to [objective].

Process:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Output format:
[Structure]
```

### Full-Featured Prompt

```markdown
You are a [role] specializing in [specialty].
Your goal is to [primary objective].

You should:
- [Expected behavior]

You must NOT:
- [Forbidden behavior]

## [Process Name]

1. **[Phase 1]**
   - [Actions]
   - [Checks]

2. **[Phase 2]**
   - [Actions]
   - [Decisions]

## Output Format

[Exact structure with examples]

## Quality Standards

- [ ] [Standard 1]
- [ ] [Standard 2]

## Error Handling

If [problem]: [solution]
```

### Checklist for Good Prompts

- [ ] Clear role definition
- [ ] Specific, measurable goal
- [ ] Explicit process/methodology
- [ ] Defined output format with examples
- [ ] Clear boundaries (do/don't)
- [ ] Quality standards or success criteria
- [ ] Error handling guidance
- [ ] Appropriate length (not too short, not too long)
