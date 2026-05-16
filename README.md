# groffdev-codex-plugin

A Codex plugin for a research, planning, implementation, review, PR-comment, grill, and handoff workflow.

## Skills

| Skill | What it does |
|-------|-------------|
| `research-codebase` | Documents the codebase as-is and saves research to `thoughts/research/` |
| `create-plan` | Builds an implementation plan in `thoughts/plans/` from researched context |
| `grill-me` | Stress-tests a plan one decision at a time, with recommended answers |
| `implement-plan` | Creates execution packets in `thoughts/packets/` and runs fresh Codex CLI instances |
| `review-work` | Runs independent Codex review loops and delegates accepted fixes |
| `address-pr-comments` | Triages PR comments and fixes approved items one packet per comment |
| `handoff` | Writes continuation notes to `thoughts/handoffs/` |

## Local Install

From this directory:

```bash
codex plugin marketplace add ./.
```

Restart Codex, open the plugin directory, choose "Groffdev Codex Plugins", and install `groffdev-codex-plugin`.
