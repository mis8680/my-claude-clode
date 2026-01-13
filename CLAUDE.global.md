# Claude Code - Global Instructions

This file contains global instructions that apply to all projects. These instructions OVERRIDE default behaviors.

---

## Code Quality

### Variable Naming
- **Always use descriptive variable names**
  - Prefer `userEmail` over `e` or `email`
  - Prefer `totalRevenue` over `total` or `rev`
  - Prefer `isAuthenticated` over `auth` or `flag`
  - Use clear, self-documenting names that explain purpose

### Code Style
- Follow existing project conventions and patterns
- Maintain consistency with the codebase
- Write clean, readable code over clever solutions

---

## Git Conventions

### Branch Naming
- **Always create a branch per Jira ticket/task**
- **Format:** `{type}/{TICKET-NUMBER}_{descriptive-name}`
  - Type: `feature/`, `fix/`, `refactor/`, etc.
  - Ticket: Jira ticket number (e.g., `ODP-5926`)
  - Description: Kebab-case descriptive name
- **Example:** `feature/ODP-5926_move-od-lambdas-to-node-js-20`
- **No version suffixes** (e.g., `--v2`) unless explicitly required

### Commits
- **Format:** Title only, no body details
- **No Claude attribution:** Do not add "Co-Authored-By: Claude" or similar
- **Jira ticket reference:**
  - Optionally prefix with ticket number: `ODP-5926: migrate to Node.js 20`
  - Or use conventional commit: `feat: migrate to Node.js 20`
  - Choose format based on project conventions
- **Title guidelines:**
  - Use conventional commit format when project uses it (e.g., `feat:`, `fix:`, `refactor:`)
  - Keep titles concise and descriptive
  - Use imperative mood (e.g., "Add feature" not "Added feature")

### Pull Requests
- **Title format:** `[TICKET-NUMBER] Description`
- **Example:** `[ODP-5926] Migrate to Node.js 20`
- **Description should link to Jira ticket** if project uses automatic linking

### Examples
```
Good: feat: add user authentication middleware
Good: fix: resolve null pointer in payment handler
Good: refactor: simplify database query logic

Bad: Updated some files
Bad: WIP
Bad: Fixed bug (with Claude attribution)
```

---

## Documentation

### Documentation Location
- Project-specific documentation MUST live in the `docs/` folder of the repository.
- The `docs/` folder is the single source of truth for the project.

### Documentation Structure (Default)
Use **meaning-based folders** to improve clarity and AI collaboration:

- `docs/prd/` — product requirements
- `docs/decisions/` — architecture & technical decisions (ADR)
- `docs/research/` — investigations and spikes
- `docs/tasks/` — planning and progress logs

> Prefer clarity and intent over numeric classification for project docs.

### Johnny Decimal System (Optional / Personal Knowledge)

- The Johnny Decimal System (JDS) MAY be used for:
  - Personal knowledge bases
  - Long-term research archives
  - Central (non-repo) vaults

- JDS SHOULD NOT be enforced for active project documentation unless explicitly required by the project.

> Use JDS where information is stable.
> Use meaning-based folders where work is ongoing.

**JDS Structure (if used):** `Area/Category/ID.document-name.md`
- **Area:** 00-99 (e.g., 10-migrations, 20-architecture)
- **Category:** Two digits (e.g., 11-node-upgrades, 21-system-design)
- **ID:** Unique document number (e.g., 11.01, 11.02)

### Documentation Types
Common documentation that belongs in `docs/`:
- Product requirements and specifications
- Architecture and technical decision records (ADRs)
- Research notes and investigation findings
- Task planning and progress logs
- Migration guides and checklists
- Troubleshooting guides
- Session summaries and debugging notes
- Any other markdown/documentation files

### When to Document
- Create session summaries for complex changes
- Document non-obvious decisions
- Keep debugging notes for troubleshooting sessions
- Maintain checklists for multi-step processes

### Document References (@ Import Pattern)

When creating new documentation that needs to reference other long documents, use the `@` import pattern instead of duplicating content:

**Format:** `@./path/to/document.md`

**Example:**
```markdown
## Task Master AI Instructions

**Import Task Master's development workflow commands and guidelines, treat as if import is in the main CLAUDE.md file.**
@./.taskmaster/CLAUDE.md
```

**When to use:**
- Referencing lengthy documentation from other files
- Avoiding duplication of content across documents
- Creating modular documentation that can be updated independently
- Keeping main documents concise while providing access to detailed information

**Benefits:**
- Single source of truth for documentation
- Easier maintenance (update once, referenced everywhere)
- Keeps documents focused and readable
- Clear indication that content is imported from elsewhere

---

## Testing

### Test Requirements
**Always write tests for new functionality and changes**

### What to Test
- **New features:** Write tests that cover the main use cases
- **Bug fixes:** Add tests that would have caught the bug
- **Refactoring:** Ensure existing tests pass, add missing coverage
- **Edge cases:** Test boundary conditions and error scenarios

### Coverage Goals
- Aim for meaningful coverage, not just high percentages
- **Critical paths:** 100% coverage for authentication, payments, data integrity
- **Business logic:** 80-90% coverage minimum
- **Utilities:** 70-80% coverage minimum
- **UI components:** Test user interactions and state changes

### Test Structure
```
describe('what we are testing', () => {
  it('should handle expected behavior', () => {
    // Arrange: Set up test data
    // Act: Execute the code
    // Assert: Verify results
  });

  it('should handle error cases', () => {
    // Test failure scenarios
  });

  it('should handle edge cases', () => {
    // Test boundaries and unusual inputs
  });
});
```

### Before Committing
- Run all tests and ensure they pass
- Check coverage reports for new code
- Verify no regressions in existing tests
- Run linting and type checking

---

## Best Practices

### Before Starting Work
1. Understand the existing codebase structure
2. Check for similar patterns in the project
3. Review related tests to understand expectations

### During Development
1. Write tests alongside implementation
2. Keep changes focused and atomic
3. Follow project conventions strictly

### Before Completing
1. Run full test suite
2. Review coverage for new code
3. Clean up debug code and console logs
4. Verify no unintended changes

---

## Serena Usage (MANDATORY)

### Always Use Serena MCP Tools

**Serena provides semantic code exploration and must be used for all code navigation tasks.**

### Core Serena Tools

1. **`find_symbol`** - Locate classes, functions, variables by name
   - Use substring matching for fuzzy search
   - More efficient than grep for finding definitions
   - Returns exact symbol locations with context

2. **`get_symbols_overview`** - Understand file structure
   - Get high-level view of all symbols in a file
   - See class hierarchies, methods, functions
   - Avoid reading entire files unnecessarily

3. **`find_referencing_symbols`** - Check dependencies before changes
   - Find all references to a symbol
   - Understand impact of changes
   - Ensure backward compatibility when refactoring

4. **`insert_after_symbol` / `insert_before_symbol`** - For code insertion
   - Insert code relative to existing symbols
   - More precise than line-based editing
   - Maintains code structure

5. **`replace_symbol_body`** - For refactoring entire symbols
   - Replace complete function/method/class definitions
   - Use when modifying entire symbol bodies
   - Not for small line edits within symbols

### Serena Rules

**NEVER:**
- ❌ Use `grep` or `ripgrep` when Serena can do semantic search
- ❌ Read entire files - use Serena to get relevant symbols only
- ❌ Use line-based search when you need symbol definitions
- ❌ Edit code without checking references first

**ALWAYS:**
- ✅ Use `find_symbol` to locate code by name
- ✅ Use `get_symbols_overview` before reading files
- ✅ Use `find_referencing_symbols` before refactoring
- ✅ Use symbol-based editing tools for precise changes

### When to Use Serena vs Other Tools

| Task | Use Serena | Use Other Tools |
|------|------------|-----------------|
| Find function/class definition | ✅ `find_symbol` | ❌ Not grep |
| Understand file structure | ✅ `get_symbols_overview` | ❌ Not Read entire file |
| Find all usages of function | ✅ `find_referencing_symbols` | ❌ Not grep |
| Search for text pattern | ❌ | ✅ Grep (for non-code) |
| Read non-code files | ❌ | ✅ Read tool |
| Edit few lines within symbol | ❌ | ✅ Edit tool |
| Replace entire function | ✅ `replace_symbol_body` | ❌ Not Edit tool |

### Example Workflow

**❌ Wrong - Reading entire files:**
```
Read src/components/UserProfile.tsx (entire file)
Read src/hooks/useUser.ts (entire file)
Find the function I need manually
```

**✅ Correct - Using Serena:**
```
get_symbols_overview("src/components/UserProfile.tsx")
find_symbol(name_path="UserProfile", include_body=true)
find_referencing_symbols(symbol_name="UserProfile")
```

### Benefits

- **Token efficient**: Only load relevant code sections
- **Semantic understanding**: Navigate by code structure, not text
- **Impact analysis**: See all references before making changes
- **Precise editing**: Symbol-based operations maintain code integrity

---

## Library Documentation (Context7 MCP)

### When to Use Context7
**Always use context7 MCP for up-to-date library documentation**

Use context7 when:
- Working with external libraries or frameworks (React, Vue, Express, etc.)
- Need current API references or method signatures
- Looking for official code examples and patterns
- Checking latest features or changes in a library version
- Implementing integrations with third-party services

### How to Use Context7
1. **First:** Call `resolve-library-id` with the library name to get the Context7 ID
2. **Then:** Call `get-library-docs` with that ID and optional topic

Example workflow:
```
User asks: "How do I use React hooks?"
1. resolve-library-id("react") → get library ID
2. get-library-docs(libraryId, topic: "hooks") → get documentation
3. Use the docs to answer or implement
```

### When NOT to Use Context7
- Built-in language features (JavaScript, Python, etc.)
- Reading existing project code (use Read/Grep instead)
- Internal project documentation
- Standard library features

### Benefits
- Always current documentation (no knowledge cutoff issues)
- Official examples and best practices
- Version-specific information when needed
- Reduces hallucination risk for library APIs

---

## Notes
- These instructions apply to all projects globally
- Project-specific CLAUDE.md files can add additional rules
- When in doubt, ask for clarification rather than assuming
- just title. no details, no CLAUDE author, for git commit message
