---
description: Create a new git branch following naming conventions
argument-hint: [ticket-number] [description]
allowed-tools: Bash(git checkout:*), Bash(git branch:*), Bash(git status:*)
---

## Current branch
!`git branch --show-current`

## Create new branch

Branch naming format: `{type}/{TICKET-NUMBER}_{descriptive-name}`

Types: feature/, fix/, refactor/, docs/, test/

Based on arguments: $ARGUMENTS

1. Parse the ticket number and description
2. Determine appropriate type based on description
3. Create branch using: `git checkout -b {type}/{ticket}_{description}`
4. Show new branch status

If no ticket number provided, ask user for:
- Ticket number (or use "no-ticket")
- Description in kebab-case
- Type (feature/fix/refactor/docs/test)
