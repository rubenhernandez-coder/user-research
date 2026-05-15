# User Research

A Codespace-ready starter for running structured user research with Claude
Code. Open the repo in GitHub Codespaces (or any Dev Containers–compatible
editor) and you get a fresh environment with Claude Code installed and the
[ua-framework] plugin enabled — the same three-stage process used in League
classes for taking a product from a vague idea to a specification and
wireframes.

[ua-framework]: https://github.com/league-infrastructure/claude-plugin-marketplace/tree/master/plugins/ua-framework

## What you get in the Codespace

- **Claude Code** installed via the official dev-container feature.
- **ua-framework plugin** auto-enabled at the project level. The first time
  you run `claude` and trust this folder, the plugin is installed from the
  League marketplace without any setup on your part.
- A **persistent volume** mounted at `~/.claude` so your login and history
  survive Codespace rebuilds.

## Quick start

1. Click **Code → Create codespace on master**, or open this repo in VS Code
   and choose **Reopen in Container**.
2. Wait for the container to finish building.
3. In the integrated terminal, run:

   ```bash
   claude
   ```

4. Sign in when prompted (a browser window opens for Claude.ai auth).
5. When Claude Code asks whether to trust this folder, answer **yes**. The
   ua-framework plugin installs automatically from
   `league-infrastructure/claude-plugin-marketplace`.
6. Start your research project:

   ```text
   /ua-framework:start
   ```

   The orchestrator will check `UA0-PROJECT-STATUS.md`, ask whether you have
   an idea yet, and route you to the right activity.

## How you work in this repo

Use it like a Claude project: the conversation is in the terminal, the
artifacts live in this directory as markdown files. The plugin writes its
output in reading order:

| File | What it is |
|---|---|
| `UA0-PROJECT-STATUS.md` | Where the project is in the process (maintained by Claude) |
| `ua1-opportunity-notes.md` | Friction observed, conversations, candidate opportunity |
| `ua2-positioning-statement.md` | Geoffrey Moore positioning paragraph + evidence |
| `ua3-research-plan.md` | Desk research plan, sources, log |
| `ua4-interview-plan.md` | Recruiting, question areas, falsification commitments |
| `ua5-stage-2-analysis.md` | Landscape, stakeholders, JTBD and scenarios |
| `ua6-specification.md` | Screen inventory and requirements |
| `wireframes/` | Astro + wired-elements wireframes |

Commit as you go — the git history of these files is part of the learning
record.

## Useful commands

| Command | What it does |
|---|---|
| `/ua-framework:start` | Initialize a project and route to the right activity |
| `/ua-framework:status` | Show where the project is and the next step |
| `/ua-framework:advance` | Mark the current pass complete and move on |

## How the auto-install works

Two files do the work:

- [.devcontainer/devcontainer.json](.devcontainer/devcontainer.json) installs
  Claude Code in the container via the official Anthropic dev-container
  feature and mounts a persistent volume for `~/.claude`.
- [.claude/settings.json](.claude/settings.json) registers the League
  marketplace under `extraKnownMarketplaces` and force-enables the
  `ua-framework` plugin via `enabledPlugins`. When you trust the folder,
  Claude Code installs the plugin from the marketplace on first run.

[.devcontainer/post-create.sh](.devcontainer/post-create.sh) pre-clones the
marketplace into the plugin cache so the first `claude` start is fast, but
it is best-effort — Claude Code will fetch on demand if the pre-fetch fails.

## Running it outside a Codespace

You can also clone this repo locally:

```bash
git clone https://github.com/League-Examples/user-research.git
cd user-research
claude
```

Trust the folder on first launch and the same auto-install path runs. You
need a working Claude Code install on your machine (`brew install claude-code`
or see the [setup docs](https://code.claude.com/docs/en/setup)).
