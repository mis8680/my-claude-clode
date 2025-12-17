---
name: subagent-creator
description: Create specialized Claude Code custom subagents with system prompts and tool configurations. Use when users ask to create a new subagent, custom agent, specialized assistant, or want to configure reusable AI workflows for Claude Code.
---

# Custom Subagent Creator

Create specialized custom subagents for Claude Code that are automatically invoked based on task context or explicitly requested by users.

## About Custom Subagents

Custom subagents are pre-configured AI personalities stored as files that Claude Code can automatically delegate tasks to. Each subagent:

- Has a specific purpose and expertise area defined in its system prompt
- Uses its own context window separate from the main conversation
- Can be configured with specific tools it's allowed to use
- Is automatically invoked by Claude when tasks match its description
- Can be explicitly requested by users
- Can be shared across projects or team members

### Key Benefits

- **Context preservation**: Each subagent operates in its own context, keeping the main conversation focused
- **Specialized expertise**: Fine-tuned with detailed instructions for specific domains
- **Reusability**: Once created, available across different projects
- **Flexible permissions**: Each subagent can have different tool access levels

### When to Create a Custom Subagent

Create a custom subagent when:
- A workflow requires specialized prompting or behavior
- Tasks need restricted/specific tool access for safety or focus
- Domain expertise needs to be packaged and reusable
- You want Claude to automatically handle certain types of tasks
- You want consistent behavior for specific task types

### Built-in vs Custom Subagents

**Built-in subagents** (cannot be modified):
- `general-purpose` - Complex multi-step tasks with full tool access
- `Explore` - Fast, read-only codebase exploration
- `Plan` - Used during plan mode for research

**Custom subagents** (what this skill helps you create):
- Defined in `.claude/agents/` (project) or `~/.claude/agents/` (user)
- Fully customizable system prompts and tool access
- Automatically discovered and available to Claude

## Subagent Creation Process

### Recommended Approach: Use /agents Command

The easiest way to create a custom subagent is using the `/agents` command:

```bash
/agents
```

This opens an interactive interface where you can:
1. Select "Create New Agent"
2. Choose project-level (`.claude/agents/`) or user-level (`~/.claude/agents/`)
3. Generate with Claude (recommended) or write manually
4. Define name, description, system prompt, and tool access
5. Edit in your preferred editor by pressing `e`

### Alternative: Manual File Creation

You can also create subagent files directly:

```bash
# Project-level subagent (available in this project only)
mkdir -p .claude/agents

# User-level subagent (available in all projects)
mkdir -p ~/.claude/agents
```

### Step 1: Define the Subagent Purpose

Clearly articulate:
- **What tasks** will this subagent perform?
- **When** should it be invoked? (triggers, use cases)
- **What outputs** should it produce?
- **What constraints** or focus areas matter?

Ask the user concrete questions:
- "What specific task should this subagent handle?"
- "Can you give examples of when you'd use this?"
- "What should the subagent always do or never do?"
- "Should it have access to all tools or a restricted set?"
- "Should it be available in all projects (user-level) or just this one (project-level)?"

### Step 2: Design the System Prompt

A sub-agent's system prompt defines its behavior and expertise.

**For detailed prompt engineering patterns**, see [references/prompt-patterns.md](references/prompt-patterns.md)

Design prompts that:

**Provide clear role and objectives:**
```
You are a specialized [ROLE] agent focused on [SPECIFIC TASK].
Your primary goal is to [OBJECTIVE].
```

**Define scope and boundaries:**
```
You should:
- [Action 1]
- [Action 2]

You must NOT:
- [Restriction 1]
- [Restriction 2]
```

**Include domain knowledge:**
```
Key concepts for this domain:
- [Concept 1]: [Description]
- [Concept 2]: [Description]

Standard workflow:
1. [Step 1]
2. [Step 2]
3. [Step 3]
```

**Specify output format:**
```
Always structure your output as:
## [Section 1]
[Content]

## [Section 2]
[Content]
```

### Step 3: Configure Tool Access

Determine which tools the sub-agent needs. Tool access can be:

**All tools** (`*`):
- Use for general-purpose agents
- Provides maximum flexibility
- Best for complex, unpredictable workflows

**Specific tools only**:
- Increases focus and reduces errors
- Prevents unintended operations
- Example: `Read, Grep, Glob, WebFetch, WebSearch` for research-only

**No tools** (text processing only):
- For pure reasoning/analysis tasks
- Fast, minimal context usage
- Example: code review from provided diff

Common tool configurations:
- **Read-only exploration**: `Glob, Grep, Read, Bash(git:*)`
- **Research**: `Read, Grep, Glob, WebFetch, WebSearch`
- **Code modification**: `Read, Edit, Write, Bash`
- **Full development**: All tools

### Step 4: Create the Subagent File

Create a Markdown file with YAML frontmatter in the appropriate location.

#### File Format

```markdown
---
name: your-subagent-name
description: Description of when this subagent should be invoked
tools: tool1, tool2, tool3  # Optional - omit to inherit all tools
model: sonnet               # Optional - sonnet, opus, haiku, or 'inherit'
permissionMode: default     # Optional - default, acceptEdits, bypassPermissions, plan, ignore
skills: skill1, skill2      # Optional - skills to auto-load
---

Your subagent's system prompt goes here. This can be multiple paragraphs
and should clearly define the subagent's role, capabilities, and approach
to solving problems.

Include specific instructions, best practices, and any constraints
the subagent should follow.
```

#### Configuration Fields

| Field | Required | Description |
|-------|----------|-------------|
| `name` | Yes | Unique identifier using lowercase letters and hyphens |
| `description` | Yes | Natural language description of when to invoke this subagent. Claude uses this to decide when to delegate tasks. Include "PROACTIVELY" or "MUST BE USED" to encourage automatic invocation. |
| `tools` | No | Comma-separated list of specific tools. If omitted, inherits all tools from main thread including MCP tools. |
| `model` | No | Model alias (`sonnet`, `opus`, `haiku`) or `'inherit'` to use main conversation's model. Defaults to configured subagent model. |
| `permissionMode` | No | Permission handling: `default`, `acceptEdits`, `bypassPermissions`, `plan`, `ignore` |
| `skills` | No | Comma-separated list of skill names to auto-load in the subagent's context |

#### Example File

Create `.claude/agents/code-reviewer.md`:

```markdown
---
name: code-reviewer
description: Expert code review specialist. Use PROACTIVELY after writing or modifying code to ensure quality and security.
tools: Read, Grep, Glob, Bash
model: inherit
---

You are a senior code reviewer ensuring high standards of code quality and security.

When invoked:
1. Run git diff to see recent changes
2. Focus on modified files
3. Begin review immediately

Review checklist:
- Code is simple and readable
- Functions and variables are well-named
- No duplicated code
- Proper error handling
- No exposed secrets or API keys
- Input validation implemented

Provide feedback organized by priority:
- Critical issues (must fix)
- Warnings (should fix)
- Suggestions (consider improving)
```

### Step 5: Using Your Subagent

Once created, your subagent is immediately available to Claude Code.

#### Automatic Invocation

Claude automatically delegates tasks based on the `description` field:

```
User: "Review my recent code changes for security issues"
Claude: [Automatically invokes code-reviewer subagent]
```

**Tips for automatic invocation:**
- Use action-oriented descriptions
- Include keywords like "PROACTIVELY" or "MUST BE USED"
- Be specific about when the agent should be used

#### Explicit Invocation

Users can explicitly request a specific subagent:

```
User: "Use the code-reviewer subagent to check this file"
User: "Have the security-analyzer subagent examine my auth code"
```

#### Managing Subagents

View and manage all subagents:
```bash
/agents
```

This shows:
- All available subagents (built-in, user, project, plugin)
- Which subagent is active when names conflict
- Options to create, edit, or delete custom subagents

### Step 6: Test and Iterate

Test the subagent with:
- **Typical use cases** - Does it handle expected scenarios?
- **Edge cases** - How does it handle unusual inputs?
- **Tool usage** - Does it use tools appropriately?
- **Output quality** - Are outputs useful and well-formatted?

Iterate on:
- System prompt clarity and specificity
- Tool access configuration
- Description wording for better automatic invocation
- Output format requirements
- Error handling instructions

## Sub-Agent Design Patterns

### Pattern 1: Focused Analyzer
**Use case**: Analyze specific aspects of code/docs
**Tools**: Read-only (Read, Grep, Glob)
**Prompt**: Specific criteria/checklist for analysis
**Example**: Security auditor, performance analyzer

### Pattern 2: Autonomous Implementer
**Use case**: Implement features following patterns
**Tools**: Full access (Read, Write, Edit, Bash)
**Prompt**: Architectural patterns, coding standards
**Example**: Feature developer, refactoring agent

### Pattern 3: Research Specialist
**Use case**: Gather and synthesize information
**Tools**: Read, Grep, WebFetch, WebSearch
**Prompt**: Research methodology, source evaluation
**Example**: Library documentation researcher, codebase explorer

### Pattern 4: Quality Enforcer
**Use case**: Validate against standards
**Tools**: Read, Grep (no write access)
**Prompt**: Specific rules, style guides, checklists
**Example**: Code reviewer, test coverage analyzer


## Common Pitfalls

**Avoid overly broad descriptions**
- Too vague → Claude won't know when to invoke the agent
- Solution: Be specific about triggers and use cases in the `description` field

**Don't over-restrict tools**
- Too few tools → agent can't complete its task
- Solution: Include all tools needed for the full workflow

**Avoid duplicate agents**
- Creating agents with overlapping purposes causes confusion
- Solution: Check existing agents with `/agents` before creating new ones

**Don't skip testing**
- Untested prompts often miss edge cases or don't invoke correctly
- Solution: Test with realistic examples and iterate on the description

**Forgetting to include "PROACTIVELY"**
- Without it, Claude may not automatically invoke your agent
- Solution: Add "PROACTIVELY" or "MUST BE USED" to the description for automatic invocation

## Examples

**For more comprehensive examples**, see [references/example-agents.md](references/example-agents.md) for production-ready sub-agents including:
- Security Auditor
- API Documentation Generator
- Test Generator
- Refactoring Specialist
- Performance Optimizer
- Dependency Upgrade Agent

### Example 1: Database Migration Reviewer

Create `.claude/agents/migration-reviewer.md`:

```markdown
---
name: migration-reviewer
description: Database migration safety expert. Use PROACTIVELY when reviewing migration files to identify safety issues before production deployment.
tools: Read, Grep, Glob
model: sonnet
---

You are a database migration safety reviewer. Your goal is to identify
potential issues in database migration files before they run in production.

Review checklist:
- Backward compatibility (can old code run during migration?)
- Rollback safety (can migration be reverted?)
- Performance impact (will migration lock tables?)
- Data integrity (are constraints properly handled?)

For each migration file:
1. Read the migration code
2. Check against the safety checklist
3. Identify risks (Critical, Warning, Info)
4. Suggest safer alternatives if issues found

Output format:
## Migration: [filename]
### Status: ✓ Safe | ⚠ Warnings | ✗ Critical Issues
### Findings:
[Detailed review]
```

**Usage:**
```
User: "Review the database migrations in db/migrations/"
Claude: [Automatically invokes migration-reviewer subagent]

# Or explicitly:
User: "Use the migration-reviewer subagent to check this migration"
```

### Example 2: Test Coverage Analyzer

Create `.claude/agents/test-coverage-analyzer.md`:

```markdown
---
name: test-coverage-analyzer
description: Test coverage specialist. Use PROACTIVELY after implementing features to identify test gaps and suggest missing tests.
tools: Read, Grep, Glob, Bash
model: sonnet
---

You are a test coverage analyst. Find gaps in test coverage and suggest
specific tests to add.

Process:
1. Read source code files
2. Read corresponding test files
3. Identify untested:
   - Functions/methods
   - Edge cases
   - Error paths
   - Integration points
4. Suggest specific tests with examples

Output format:
## Coverage Analysis: [module]
### Coverage: [X]%
### Tested: [list]
### Missing Coverage:
- [Untested item]: [Why it matters] [Test example]
```

**Usage:**
```
User: "Analyze test coverage for src/auth/"
Claude: [Automatically invokes test-coverage-analyzer subagent]

# Or explicitly:
User: "Use the test-coverage-analyzer to find gaps in my tests"
```

## Best Practices

### Start with Claude-Generated Agents

We highly recommend generating your initial subagent with Claude and then iterating:
1. Use `/agents` and select "Create New Agent"
2. Let Claude generate the initial version
3. Customize it to your specific needs
4. This gives you a solid foundation to build from

### Design Focused Subagents

- Create subagents with single, clear responsibilities
- Avoid trying to make one subagent do everything
- Focused agents are more predictable and perform better

### Write Detailed Prompts

- Include specific instructions, examples, and constraints
- The more guidance you provide, the better results
- Document the expected output format
- Specify what the agent should and shouldn't do

### Limit Tool Access Appropriately

- Only grant tools necessary for the subagent's purpose
- This improves security and helps the agent focus
- Use read-only tools for analysis agents
- Omit the `tools` field for full-featured agents

### Use Descriptive `description` Fields

- Make descriptions action-oriented and specific
- Include "PROACTIVELY" or "MUST BE USED" for automatic invocation
- Clearly state when Claude should delegate to this agent
- Examples:
  - Good: "Security expert. Use PROACTIVELY after code changes to identify vulnerabilities."
  - Bad: "Helps with security stuff"

### Version Control Project Agents

- Check `.claude/agents/` into git
- Your team can benefit from and improve them collaboratively
- Document any team-specific agents in your project README

## Advanced Features

### Resumable Subagents

Subagents can be resumed to continue previous work:

```
User: "Use the code-analyzer agent to review the auth module"
Claude: [Agent completes analysis, returns agentId: "abc123"]

User: "Resume agent abc123 and now check the authorization logic"
Claude: [Agent continues with full context from previous conversation]
```

Agent transcripts are stored in `agent-{agentId}.jsonl` files.

### Chaining Subagents

For complex workflows, chain multiple subagents:

```
User: "First use the code-explorer to find performance issues,
      then use the optimizer to fix them"
```

### Plugin Agents

Plugins can provide custom subagents that integrate seamlessly:
- Plugin agents appear in `/agents` interface
- Can be invoked automatically or explicitly
- Follow the same format as custom agents

### CLI-Based Configuration

Define subagents dynamically for testing or automation:

```bash
claude --agents '{
  "test-runner": {
    "description": "Test automation expert. Use proactively to run tests.",
    "prompt": "You are a test automation expert...",
    "tools": ["Read", "Bash"],
    "model": "sonnet"
  }
}'
```

## Quick Reference

### Subagent File Locations
```bash
.claude/agents/          # Project-level (this project only)
~/.claude/agents/        # User-level (all projects)
```

### File Format Template
```markdown
---
name: your-agent-name
description: When Claude should invoke this agent. Include PROACTIVELY for automatic use.
tools: Read, Grep, Glob  # Optional - omit for all tools
model: sonnet            # Optional - sonnet, opus, haiku, or 'inherit'
---

System prompt defining agent's role, behavior, and expertise.
```

### Common Tool Configurations
- **Read-only**: `Read, Grep, Glob, Bash`
- **Research**: `Read, Grep, Glob, WebFetch, WebSearch`
- **Code editing**: `Read, Write, Edit, Grep, Glob`
- **Full development**: Omit `tools` field (inherits all tools)
- **Analysis only**: `Read, Grep, Glob`

### Model Selection Guide
- Simple analysis, following templates → `haiku`
- Most tasks, balanced needs → `sonnet` (default)
- Complex reasoning, highest quality → `opus`
- Match main conversation → `'inherit'`

### Creation Commands
```bash
# Recommended: Interactive interface
/agents

# Manual creation
mkdir -p .claude/agents
cat > .claude/agents/my-agent.md <<'EOF'
---
name: my-agent
description: My specialized agent
---
System prompt here
EOF
```

### Priority Order
When subagent names conflict:
1. Project-level (`.claude/agents/`)
2. CLI-defined (`--agents` flag)
3. User-level (`~/.claude/agents/`)
4. Plugin agents
