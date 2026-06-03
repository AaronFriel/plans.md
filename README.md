# Plans.md

A Codex plugin for making Codex get work done with durable plan files.

Plans.md gives Codex one skill, `plans-md`, for creating and maintaining `plans.md`, `plan.md`, `records.md`, and `record.md` files. The goal is practical: keep the objective clear, define what "done" means, track progress in files, and make unfinished work hard to lose.

Plugin manifest:

- `.codex-plugin/plugin.json`
- `plugins/plans-md/.codex-plugin/plugin.json`

Marketplace manifest:

- `.agents/plugins/marketplace.json`

Add it in Codex:

- Source: `AaronFriel/plans.md`
- Git ref: `main`
- Sparse paths: leave empty

Skill:

- `skills/plans-md/SKILL.md`

References:

- `skills/plans-md/references/PLANS.md`
- `skills/plans-md/references/record-patterns.md`

The root plugin supports direct plugin installs. The copy under `plugins/plans-md` is used by the marketplace manifest so Codex can read plugin metadata before install.
