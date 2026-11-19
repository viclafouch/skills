# viclafouch/skills

The Claude Code plugin of Victor de la Fouchardière: the skills behind how he works, the same on every Mac he uses. The repository is both the plugin and the marketplace that serves it.

## Skills

| Skill | What it does |
|---|---|
| `create-issue` | Files one evergreen GitHub issue per run, shaped so a fresh session can take it with nothing else |
| `load-issue` | Briefs a GitHub issue from its live state: whether it can start, and where its description drifted from the code |
| `start-issue` | Takes an issue from a fresh base branch to a reviewed working tree, routed to test-driven development, a plain implement loop, or a diagnosis |
| `product-retro` | Looks back on a session or a subject and proposes grounded product changes, amendments to open issues, or challenges to the plan |

Each skill runs as `/<skill>`, or `/viclafouch:<skill>` when another command already holds the short name. `start-issue` and `product-retro` run only when you type them.

`create-issue` and `start-issue` call skills of the `mattpocock-skills` plugin, from the official marketplace: install it next to this one.

## Install on a Mac

```sh
claude plugin marketplace add viclafouch/skills
claude plugin install viclafouch@viclafouch
```

Then turn on auto-update for the `viclafouch` marketplace, under **Marketplaces** in `/plugin`. Each Mac then picks up every pushed commit a few minutes after a session starts, and loads it at the next launch.

## Change a skill

Edit the skill in a clone of this repository, then push to `main`. The plugin has no `version`, so every commit is a new release.

Before you push:

```sh
claude plugin validate .
```

To try a change before you push, start a session with `claude --plugin-dir .` from the clone.

## Add a skill

Add a folder under `skills/` with its `SKILL.md`. The folder name is the command name.
