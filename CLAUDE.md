# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Purpose

This is a personal repository for custom Claude Code configurations including:
- Custom slash commands for common development workflows
- Custom skills for specialized tasks
- Documentation templates and examples
- Personal development tools and utilities

## Directory Structure

```
.claude/
├── commands/           # Custom slash commands
│   ├── docs/          # Documentation-related commands
│   ├── git/           # Git workflow commands
│   └── dev/           # Development workflow commands
├── skills/            # Custom agent skills
│   ├── code-review/   # Code review skill
│   └── docs-gen/      # Documentation generation skill
└── CLAUDE.md          # This file

docs/                  # Documentation and notes
├── prd/              # Product requirements
├── decisions/        # Technical decisions (ADR)
├── research/         # Investigations and spikes
└── tasks/            # Planning and progress logs
```

## Custom Slash Commands

This repository includes custom slash commands organized by category. Use `/help` to see all available commands.

### Documentation Commands (`/docs/*`)
- Commands for generating, updating, and organizing documentation
- Follow the documentation structure defined in global CLAUDE.md

### Git Commands (`/git/*`)
- Workflow commands for branching, commits, and PRs
- Follow the git conventions from global CLAUDE.md

### Development Commands (`/dev/*`)
- Common development workflows
- Testing, linting, and code analysis shortcuts

## Custom Skills

Skills are automatically invoked by Claude when relevant to the task.

### Code Review Skill
Comprehensive code review focusing on:
- Code quality and style
- Security vulnerabilities
- Performance issues
- Test coverage

### Documentation Generation Skill
Automated documentation creation following project standards:
- ADR (Architecture Decision Records)
- Task planning documents
- Research notes
- Session summaries

## Documentation Standards

All documentation in this repository follows the structure defined in the global CLAUDE.md:

- Use meaning-based folders (`docs/prd/`, `docs/decisions/`, etc.)
- Use the `@import` pattern to reference other documents
- Keep documentation in the `docs/` folder as single source of truth

## Development Workflow

Since this is a configuration repository:

1. **Adding Commands**: Create new `.md` files in `.claude/commands/`
2. **Adding Skills**: Create new directory with `SKILL.md` in `.claude/skills/`
3. **Testing**: Use commands/skills in real projects to validate
4. **Documentation**: Document new commands and skills in this file

## Version Control

- Follow global git conventions (no Claude attribution, descriptive commits)
- Use meaningful commit messages describing what was added/changed
- Branch naming: `feature/add-{command-or-skill-name}`

## Extending This Repository

When adding new commands or skills:

1. Read existing examples first
2. Follow naming conventions (kebab-case)
3. Add frontmatter with descriptions
4. Test thoroughly before committing
5. Update this CLAUDE.md if adding new categories

## Reference

For detailed information on creating commands and skills, see:
- Official Claude Code docs: https://code.claude.com/docs
- Global CLAUDE.md for general coding standards
