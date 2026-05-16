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

## Recommended Workflow

Use the skills in this order for normal feature work:

```text
research-codebase -> create-plan -> grill-me -> implement-plan -> review-work
```

Then use `address-pr-comments` after a pull request has review feedback.

Use `handoff` whenever a session is ending, the context is getting long, or another Codex session should continue the work. It is not a replacement for research, plans, packets, or reviews; it should reference those artifacts instead of duplicating them.

### How The Skills Connect

1. `research-codebase` documents how the repository works today and saves findings in `thoughts/research/`.
2. `create-plan` reads relevant research and code, optionally runs the `grill-me` decision loop, and writes an implementation plan in `thoughts/plans/`.
3. `grill-me` stress-tests unclear plan or design decisions one question at a time. It can be used standalone or during `create-plan`.
4. `implement-plan` reads a plan, writes execution packets to `thoughts/packets/`, and runs fresh Codex CLI instances for each implementation slice.
5. `review-work` sends completed work to a fresh Codex reviewer and delegates accepted fixes.
6. `address-pr-comments` handles GitHub PR review comments after a PR exists.
7. `handoff` captures the current state for the next session and should point to the relevant `thoughts/` artifacts.

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

## Updating The Plugin

For users who installed the GitHub marketplace, update marketplace sources with:

```bash
codex plugin marketplace upgrade groffdev-codex-plugin-marketplace
```

You can also refresh all configured marketplaces:

```bash
codex plugin marketplace upgrade
```

Then restart Codex. If the plugin directory shows an available update for `groffdev-codex-plugin`, install or update it there.

For local checkout development:

```bash
cd /path/to/groffdev-codex-plugin
git pull
codex plugin marketplace upgrade groffdev-codex-plugin-marketplace
```

Then restart Codex so it reloads the installed plugin copy.

### Versioning

Increment `.codex-plugin/plugin.json` version when plugin behavior changes, including skill instructions, hooks, bundled apps, or MCP config.

Suggested versioning:

- Patch, such as `0.1.1`: wording fixes, skill behavior refinements, small hook fixes.
- Minor, such as `0.2.0`: new skills, renamed workflows, meaningful behavior changes.
- Major, such as `1.0.0` to `2.0.0`: breaking changes to skill names, artifact paths, or expected workflow.

README-only changes do not require a version bump unless the documented behavior depends on changed plugin files.

## Codex CLI Packet Defaults

Implementation and review packets should run through fresh Codex CLI instances using GPT-5.5, low reasoning effort, and the fast service tier:

```bash
codex exec -m gpt-5.5 \
  -c model_reasoning_effort="low" \
  -c service_tier="fast" \
  < "$PACKET_PATH"
```

The installed Codex CLI exposes `-m, --model <MODEL>` directly. Reasoning effort and fast mode are config overrides, so this plugin passes them with `-c`.

## Repo-Scoped Sharing

If you want a project repository to advertise this plugin to everyone working in that repo, add a marketplace file to that project at:

```text
.agents/plugins/marketplace.json
```

That file can point to this GitHub-backed plugin marketplace, or the project can vendor a copy of the plugin under its own `plugins/` directory. Repo-scoped marketplace files live in the project repo, so they are shared with collaborators through git.
