---
name: init
description: Initialize project-specific dev-team configuration. Creates .claude/team/ directory with templates for rules, stack, conventions, and devops config.
argument-hint: "[--force to overwrite existing config]"
disable-model-invocation: true
---

# Initialize Dev Team for This Project

Create the `.claude/team/` directory with project-specific configuration templates.

## Steps

1. Check if `.claude/team/` already exists. If so, ask the user if they want to overwrite.

2. Read the project's CLAUDE.md, package.json (or equivalent), and explore the codebase briefly to understand:
   - Tech stack (framework, language, key dependencies)
   - Testing framework
   - Linting/formatting tools
   - Build/dev commands
   - Deploy setup (if detectable)

3. Create these files:

### `.claude/team/rules.md`
General development rules for this project. Pre-fill with detected info:
```markdown
# Dev Team Rules — [Project Name]

## Stack
- [Detected framework, language, etc.]

## Development
- [Dev command]
- [Build command]
- [Detected conventions]

## Quality
- Linter: [detected]
- Tests: [detected test framework]
- Type checking: [if TypeScript]

## Git Workflow
- Branch naming: feature/, fix/, chore/
- Commit style: conventional commits
- PR required: yes/no
```

### `.claude/team/conventions.md`
Coding conventions specific to this project:
```markdown
# Coding Conventions

## File Organization
- [Detected patterns]

## Naming
- [Components, functions, files]

## Imports
- [Import style/order]

## Error Handling
- [Patterns used]
```

### `.claude/team/devops.md`
Deployment configuration:
```markdown
# DevOps Configuration

## Environments
- Staging: [URL if detected]
- Production: [URL if detected]

## Deploy Commands
- Staging: [command]
- Production: [command]

## Health Checks
- [endpoints]

## Rollback
- [procedure]
```

4. Tell the user what was created and suggest they review and customize each file.
