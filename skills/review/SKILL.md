---
name: review
description: Run a code review on recent changes. Can specify files, a commit range, or review the current diff. For comprehensive reviews, spawns parallel reviewers via Agent Teams.
argument-hint: "[files or commit range]"
---

# Dev Team Code Review

Review target: **$ARGUMENTS**

Current diff: !`git diff --stat HEAD~1 2>/dev/null || git diff --stat`

## Process

1. Determine what to review:
   - If $ARGUMENTS specifies files → review those files
   - If $ARGUMENTS specifies a commit range → review that range
   - If $ARGUMENTS is empty → review uncommitted changes or last commit

2. Read CLAUDE.md and `.claude/team/` files for project standards.

3. Delegate to **@reviewer** with the files/changes to review.

4. Present the review results with clear verdict (Approved / Changes Requested).

5. If changes are requested, ask the user if they want to delegate fixes to **@developer**.
