# dev-team

A Claude Code plugin that provides a full development team of specialized AI agents and skills for orchestrating software development workflows. Agents cover the entire dev lifecycle — from requirements to deployment — and skills wire them together into reusable commands.

## Features

- **8 specialized agents**: lead, architect, developer, reviewer, tester, devops, product-owner, scout
- **5 workflow skills**: kickoff, discover, init, review, sync
- Pure markdown — no build step, no dependencies
- Works with any project and tech stack

## Installation

**From marketplace:**
```bash
/plugin install dev-team@claude-code-marketplace
```

**From GitHub:**

Add to `~/.claude/settings.json`:
```json
{
  "plugins": {
    "dev-team": {
      "source": {
        "source": "npm",
        "url": "https://github.com/EduCosta85/dev-team"
      }
    }
  }
}
```

## Usage

```
/dev-team:kickoff <feature description>   # Start a full dev cycle
/dev-team:discover                        # Analyze codebase and generate team config
/dev-team:init                            # Bootstrap .claude/team/ config files
/dev-team:review [files or commit range]  # Run a code review
/dev-team:sync                            # Incrementally update team config
```

Start a session with the full team lead:
```
claude --agent lead
```

## Agents

| Name | Role | Model |
|------|------|-------|
| lead | Orchestrates the full dev lifecycle, delegates to all agents | opus |
| product-owner | Decomposes features into user stories and acceptance criteria | opus |
| architect | Designs technical approach and creates implementation plans | opus |
| developer | Implements code following project standards and the plan | sonnet |
| reviewer | Reviews code for correctness, style, and security | opus |
| tester | Writes and runs tests, validates acceptance criteria | sonnet |
| devops | Handles deployments, CI/CD, and infrastructure | sonnet |
| scout | Performs deep codebase analysis and generates team config | opus |

## Skills

| Name | Description |
|------|-------------|
| kickoff | Start a full development cycle from feature description to implementation |
| discover | Full codebase discovery — generates agents, skills, and team config |
| init | Bootstrap `.claude/team/` directory with project configuration templates |
| review | Code review on recent changes, specific files, or a commit range |
| sync | Incremental update of team config based on changes since last discovery |

## License

MIT
