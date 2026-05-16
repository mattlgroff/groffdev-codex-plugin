---
name: review-work
description: Send completed work to a fresh Codex CLI instance for independent review, triage feedback, and delegate accepted fixes.
---

# Review Work

Run an independent review loop for the current work.

Argument hint: `[description-of-work]`.

## Workflow

1. Determine scope from the user description or from:
   - `git diff --stat HEAD~1`
   - `git diff --name-only HEAD~1`
   - recent `thoughts/plans/` and `thoughts/packets/`
2. Write a review prompt to `thoughts/reviews/YYYY-MM-DD-description.md`.
3. Run a fresh Codex reviewer:

```bash
codex exec < "$REVIEW_PROMPT_PATH"
```

4. Triage findings:
   - Agree -> Fix
   - Agree -> Defer
   - Disagree -> Skip
5. Present triage to the user before applying fixes unless the user explicitly asked for fully automated review/fix.
6. For accepted fixes, write a fix packet to `thoughts/reviews/YYYY-MM-DD-description-fix-roundN.md` and run `codex exec < "$FIX_PACKET_PATH"`.
7. Re-review until clean, only nits remain, a blocker appears, or three rounds have run.

Never inline review or fix prompts with heredocs.

## Reviewer Prompt Requirements

Ask the reviewer to inspect the git diff, run relevant tests, check for bugs, regressions, missing tests, security issues, and unnecessary scope. Require findings with file:line references and a final risk level.

## Final Summary

Report review rounds, changes applied, verification results, deferred items, remaining nits, and artifact paths.
