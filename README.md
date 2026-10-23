# qa-kit

A small Claude Code plugin for wrapping up a piece of work: summarise what changed on your branch, then get a quick review of it before you open a pull request.

## What's included

| Component | Type | What it does |
|---|---|---|
| `summarize-changes` | Slash command | Lists each file touched on the current branch with a one-line description of the change, short enough to paste into a PR description. |
| `code-reviewer` | Subagent | Reviews recent changes for bugs, missing error handling and unclear names, and returns findings grouped by severity (high, medium, low). It is read-only: it uses `Read`, `Grep` and `Glob`. |

## Structure

```
.
├── .claude-plugin/
│   └── plugin.json
├── commands/
│   └── summarize-changes.md
├── agents/
│   └── code-reviewer.md
└── README.md
```

## Usage

Load the plugin locally from the repo root:

```bash
claude --plugin-dir .
```

Then:

- **Summarise your branch:** run `/qa-kit:summarize-changes`.
- **Review your changes:** ask Claude something like "review my recent changes". It should hand the work to the `code-reviewer` subagent.

After editing any plugin file, run `/reload-plugins` to pick up the changes.

## Validation

The **Validate plugin** GitHub Action checks the plugin structure on every push. To run the same check locally:

```bash
node .github/scripts/validate-plugin.js
```
