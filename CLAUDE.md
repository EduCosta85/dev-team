# dev-team — Claude Code Plugin

A pure-markdown Claude Code plugin. No build step, no dependencies.

## File Structure

```
.claude-plugin/     # Plugin metadata (plugin.json, marketplace.json)
agents/             # Agent definition files (*.md)
skills/             # Skill directories, each with a SKILL.md
  discover/
  init/
  kickoff/
  review/
  sync/
```

## Agent Frontmatter

```yaml
---
name: agent-name
description: What this agent does
tools: Read, Grep, Glob, Bash, Edit, Write, Agent
disallowedTools: Agent        # optional
model: opus | sonnet | haiku
maxTurns: 50                  # optional, default varies
memory: user                  # optional
---
```

## Skill Frontmatter

```yaml
---
name: skill-name
description: What this skill does
argument-hint: "<required-arg>"          # shown in autocomplete
disable-model-invocation: true           # optional — for pure-script skills
allowed-tools: Read, Grep, Glob, Bash, Write, Edit  # optional override
---
```

## Conventions

- Agent files live in `agents/` as `<name>.md`
- Skill files live in `skills/<name>/SKILL.md`
- Use `$ARGUMENTS` in skill bodies to reference user-provided arguments
- Use `!` prefix for inline shell commands in skill bodies (e.g., `!`git log --oneline -1``)
- Delegate to agents using `@agent-name` syntax in skill instructions
- Keep agent prompts role-focused; keep skills workflow-focused
