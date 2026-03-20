---
name: sync
description: Incremental update of project team config. Compares current state with last discovery and updates only what changed. Much faster and cheaper than full discovery.
argument-hint: "[--force to trigger full re-sync]"
allowed-tools: Read, Grep, Glob, Bash, Write, Edit
---

# Project Sync

Incrementally update team config based on changes since last discovery.

Git state: !`git log --oneline -1 2>/dev/null`
Last discovery meta: !`cat .claude/team/.meta.json 2>/dev/null || echo "NO META — run /dev-team:discover first"`
Commits since discovery: !`HASH=$(cat .claude/team/.meta.json 2>/dev/null | grep -o '"commit_hash"[[:space:]]*:[[:space:]]*"[^"]*"' | grep -o '[^"]*$' | head -1); test -n "$HASH" && git log --oneline "$HASH"..HEAD 2>/dev/null | head -20 || echo "Cannot determine — no meta found"`
Changed files since discovery: !`HASH=$(cat .claude/team/.meta.json 2>/dev/null | grep -o '"commit_hash"[[:space:]]*:[[:space:]]*"[^"]*"' | grep -o '[^"]*$' | head -1); test -n "$HASH" && git diff --stat "$HASH"..HEAD 2>/dev/null | tail -5 || echo "Cannot determine"`

## Instructions

1. If `.claude/team/.meta.json` does not exist:
   - Tell the user: "No previous discovery found. Run `/dev-team:discover` first."
   - Stop.

2. Analyze what changed since last discovery:
   - Check commits since `commit_hash` in meta
   - If 0 commits → "Everything is up to date. No sync needed."
   - Check which areas changed (use `git diff --stat` output):
     - `package.json` changed → update `stack.md`, check for new deps
     - `src/` structure changed significantly → update `conventions.md`, check if new agents needed
     - `.github/workflows/` changed → update `devops.md`
     - New directories/modules appeared → consider new path-scoped rules or agents

3. For each affected area:
   - Read the changed files
   - Update the corresponding team config file
   - If a project agent's domain changed, update the agent

4. Update `.meta.json` with new commit hash and timestamp.

5. Present a summary:
   ```
   ## Sync Report

   ### Changes detected: X commits since [old_hash]

   ### Updated:
   - .claude/team/stack.md — added new dependency: [name]
   - .claude/agents/firebase-expert.md — updated collection list

   ### No changes needed:
   - .claude/team/rules.md — still accurate
   - .claude/team/devops.md — no CI/CD changes
   ```

6. Write updated files (no approval needed for sync — it's incremental).
