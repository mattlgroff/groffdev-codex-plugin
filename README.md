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

## Install From GitHub

Run this on the computer where you use Codex:

```bash
codex plugin marketplace add mattlgroff/groffdev-codex-plugin
```

Then restart Codex, open the plugin directory, choose "Groffdev Codex Plugins", and install `groffdev-codex-plugin`.

### What This Command Does

`codex plugin marketplace add mattlgroff/groffdev-codex-plugin` registers this GitHub repo as a plugin marketplace source for your local Codex installation.

It affects your computer's Codex config/cache. It does not modify this GitHub repo, and it does not add files to the repository you are working in.

Conceptually, Codex:

1. Fetches or records `github.com/mattlgroff/groffdev-codex-plugin` as a marketplace source.
2. Reads `.agents/plugins/marketplace.json`.
3. Finds the `groffdev-codex-plugin` entry.
4. Lets you install and enable that plugin in your local Codex environment.

Other people install it the same way on their own computers:

```bash
codex plugin marketplace add mattlgroff/groffdev-codex-plugin
```

## Install From A Local Checkout

From this directory:

```bash
codex plugin marketplace add ./.
```

This also registers a marketplace source for your local Codex installation, but it points at the folder on disk instead of GitHub. It is useful while developing the plugin.

## Repo-Scoped Sharing

If you want a project repository to advertise this plugin to everyone working in that repo, add a marketplace file to that project at:

```text
.agents/plugins/marketplace.json
```

That file can point to this GitHub-backed plugin marketplace, or the project can vendor a copy of the plugin under its own `plugins/` directory. Repo-scoped marketplace files live in the project repo, so they are shared with collaborators through git.
