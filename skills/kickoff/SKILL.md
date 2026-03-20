---
name: kickoff
description: Start a full development cycle. Delegates to Product Owner for requirements, then Architect for technical plan. Use when starting a new feature or significant change.
argument-hint: "<feature description>"
---

# Dev Team Kickoff

Start a development cycle for: **$ARGUMENTS**

## Process

1. First, check if `.claude/team/rules.md` exists. If not, suggest running `/dev-team:init` first.

2. Delegate to **@product-owner** with this prompt:
   > Analyze this codebase and decompose the following feature into user stories with acceptance criteria:
   > $ARGUMENTS
   > Read CLAUDE.md and .claude/team/ files for project context.

3. Present the Product Owner's output to the user. Ask: "Does this look right? Any changes?"

4. After approval, delegate to **@architect** with this prompt:
   > Based on these user stories and acceptance criteria, design the technical solution and create an implementation plan:
   > [Include PO's output]
   > Read CLAUDE.md and .claude/team/ files for project conventions.

5. Present the Architect's plan. Ask: "Shall I proceed with implementation?"

6. If approved, delegate to **@developer** with the implementation plan, task by task.

7. After implementation, delegate to **@reviewer** for code review.

8. After review passes, delegate to **@tester** for test writing and execution.

9. Summarize the full cycle and ask if deploy is needed.
