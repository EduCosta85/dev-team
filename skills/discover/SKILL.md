---
name: discover
description: Full project discovery — analyzes the codebase and generates team config, project-specific agents, skills, and rules. Run once when setting up a new project, or to rebuild from scratch.
argument-hint: "[--force to overwrite existing config]"
allowed-tools: Read, Grep, Glob, Bash, Write, Edit
---

# Project Discovery

Run a full discovery of this project.

Git state: !`git log --oneline -1 2>/dev/null`
Project root: !`pwd`
Has team config: !`test -d .claude/team && echo "YES — .claude/team/ exists" || echo "NO — fresh project"`
Has graph: !`test -f .code-review-graph/graph.db && echo "YES — code-review-graph available" || echo "NO — graph not built"`

## Instructions

1. If `.claude/team/` already exists and `$ARGUMENTS` does not contain `--force`:
   - Read `.claude/team/.meta.json` to show when discovery was last run
   - Ask the user: "Team config already exists (discovered at [date], commit [hash]). Use `/dev-team:sync` to update incrementally, or run `/dev-team:discover --force` to rebuild from scratch."
   - Stop here.

2. If proceeding, delegate the full discovery to **@scout**:
   > Run a full project discovery. Analyze the codebase thoroughly and generate all team configuration, project-specific agents, skills, and rules.
   >
   > Key info:
   > - Project root: [pwd]
   > - Code-review-graph available: [yes/no]
   > - Existing CLAUDE.md: [yes/no]
   >
   > Remember: present the discovery report and wait for approval before writing files.
