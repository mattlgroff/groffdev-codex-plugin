---
name: handoff
description: Compact the current conversation into a handoff document for another Codex agent to pick up, saved under thoughts/handoffs.
---

# Handoff

Write a concise handoff document so a fresh Codex agent can continue the work.

Argument hint: what the next session will be used for.

Save the document under `thoughts/handoffs/`. Create the directory if needed. Use a filename in this shape:

```text
thoughts/handoffs/YYYY-MM-DD-description.md
```

If a temporary path is useful while drafting, produce it with `mktemp -t handoff-XXXXXX.md` and read the file before writing to it. The final artifact must live in `thoughts/handoffs/`.

## Content Rules

- Do not duplicate content already captured in PRDs, plans, ADRs, issues, commits, diffs, research, packets, or reviews. Reference those artifacts by path or URL.
- If the user passed arguments, treat them as the next session's focus and tailor the handoff to that work.
- Include suggested skills for the next session, if any.
- Include the exact current branch, git commit, and dirty worktree summary.
- Include blockers, assumptions, and next commands only when they are actionable.

## Suggested Structure

```markdown
# Handoff: [short title]

## Next Session Focus
[What the next Codex session should accomplish.]

## Current State
- Branch: `[branch]`
- Commit: `[sha]`
- Worktree: [clean/dirty summary]
- Key artifacts: [paths]

## Decisions Already Made
- [Decision and artifact path]

## Remaining Work
- [Concrete next action]

## Verification Context
- [Commands run and results, or "Not run yet"]

## Suggested Skills
- [skill name] - [why]
```
