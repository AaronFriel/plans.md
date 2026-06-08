# Plans.md

A Codex plugin for making Codex get work done with plan files.

Plans.md gives Codex one skill, `plans-md`, for creating and maintaining `plans.md`, `plan.md`, `records.md`, and `record.md` files. The goal is practical: keep the objective clear, define what "done" means, track progress in files, and make unfinished work hard to lose.

## Install With Codex CLI

Install the `AaronFriel/codex-plugins` marketplace, then install `plans-md` from that marketplace:

```sh
codex plugin marketplace add AaronFriel/codex-plugins --ref main
codex plugin add plans-md@codex-plugins
```

## Install With Codex App

In Codex App, add a marketplace:

- Source: `AaronFriel/codex-plugins`
- Git ref: `main`
- Sparse paths: leave empty

Then install `PLANS.md` from the marketplace.

## Repository Layout

Plugin manifest:

- `.codex-plugin/plugin.json`

Skill:

- `skills/plans-md/SKILL.md`

References:

- `skills/plans-md/references/PLANS.md`
- `skills/plans-md/references/record-patterns.md`
