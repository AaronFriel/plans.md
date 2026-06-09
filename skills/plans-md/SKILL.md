---
name: plans-md
description: Create and maintain concrete plans.md, plan.md, record.md, and records.md files for substantial Codex work. Use when the user asks to plan work, organize several related tasks, continue until done, delegate to subagents, run experiments, design an app, perform security review, or avoid vague planning language.
---

# Plans.md

Plans.md keeps substantial work understandable while it is happening.

Use this skill when a task is large enough that chat history alone will not keep the work clear: multi-step coding, research, design, debugging, benchmarking, security review, migrations, long cleanup, or any task where subagents may help.

The purpose of Plans.md is to finish work, not to create attractive planning files. Plans should make unfinished work obvious, preserve the user's intent, and help the agent keep moving until the work is complete, deliberately paused, or blocked on information the user must provide.

This skill works best when each plan has a clear scope, explicit boundaries, and a visible timeline. If a plan is canceled, superseded, split, merged, or moved, the affected plan should say so plainly and point to the plan that now owns the work. The new plan should point back to the older plan when that history matters.

## Core Terms

- A `plan.md` explains one meaningful piece of work: what is being done, why it matters, what has happened, and what still needs to happen.
- A root `plans.md` coordinates several child plan folders when the work has genuinely independent parts.
- A `record.md` stores dense supporting material for its plan: commands, commits, measurements, sources, sketches, screenshots, hypotheses, failed attempts, reviewer notes, and links to artifacts.
- A root `records.md` stores coordination notes, decisions, launches, merges, and cross-plan evidence when the root `plans.md` would otherwise become hard to skim.
- A child plan folder is a named directory such as `parser-rewrite/` or `billing-ui/` that contains its own `plan.md`, usually with a `record.md`.
- An associated file is any extra file named by the plan, such as `mockup.png`, `threat-model.md`, `benchmark-results.md`, or `review-notes.md`.
- For implementation-heavy work, use the structure in `references/PLANS.md`.

Do not create a separate record file just because the skill says so. Create it when the plan needs durable evidence or when the work has enough detail that the plan would become hard to skim.

## Start

1. Look for an existing convention: `PLANS.md`, `plans/`, `docs/plans/`, or nearby `plan.md` files.
2. If the repo has its own `PLANS.md`, follow it. Otherwise use `references/PLANS.md`.
3. Search for existing related plans before creating a new one. Extend an existing plan when it covers the same work. If several plans could apply, choose one and record why in that plan's `Decision Log`.
4. For work likely to span many turns, delegated work, or more than an hour, use the current Codex goal supervisor according to platform instructions. Create or update the plan files first, then make the goal instruction point at those files. The goal should say something like "complete `<plan path>`" and name any relevant `plans.md`, `plan.md`, `records.md`, or `record.md` paths so future supervision checks the files, not just chat.
5. For higher-level harness features such as `/loop`, goals, monitors, or other supervision instructions, keep the mutable plan in files and keep the harness instruction short. Do not paste the whole plan into the goal or loop instruction. Those instructions are often less mutable than files, and duplicating the plan there can create split-brain instructions when the agent later updates `plan.md` but the old goal text still says something else.
6. When a harness goal, loop, issue, or tracker item names a plan, do not mark that harness item complete until the associated plan is also in its completed state. If the work is finished but the plan still lives under `active/`, or an external tracker still says active, the remaining task is to update the plan state, summarize the outcome, and then complete the harness item.
7. Choose the smallest durable structure that fits the task:
   - One task: `plan.md`.
   - One substantial task: `plan.md` and `record.md`.
   - Several independent tasks: root `plans.md`, root `records.md` if useful, and one child folder per named part.
8. Write plans for a casual observer who is skimming. The reader should understand the current state from headings and first sentences.
9. Let the root `plans.md` choose the naming convention for child plan folders. Dates, priority labels, and short descriptive names are often useful because they make order and lineage visible, but the skill must not enforce one global convention.
10. For several child plans, prefer `backlog/`, `active/`, and `completed/` folders unless the repository already has a clearer convention. The layout should make state changes cheap: usually one `mv`, one tracker status update, or one clearly named status edit. Avoid layouts where completing a plan requires updating several independent sources of truth.
11. Choose names that sort in the order the user cares about. For active and backlog plans, priority then date is often useful, such as `P0-2026-06-01-parser-rewrite`. For completed plans, date then priority is often useful, such as `2026-06-01-P0-parser-rewrite`.
12. Add a `## Plan Layout` section to the root `plans.md` when the plan is split across files. It should name the files or filename patterns, including any `records.md`, child `plan.md`, child `record.md`, and associated files.
13. Define the `record.md` or `records.md` format inside the plan. The record format should fit the work, not a generic template.
14. When setting up Plans.md in a repository, ask where planning information should live. Some projects want plans and records committed in the repository. Others use issues, project trackers, docs, wikis, lab notebooks, or experiment systems. Prefer one source of truth. If more than one system is used, the root `plans.md` should say what belongs in each place and how entries link to commits, pull requests, issues, or external documents.

## Record Formats

Use `record.md` as a plan-defined scratchpad, not as a mandatory ledger.

- For experiments or optimization, preregister the question, method, baseline, metric, stop condition, starting commit, expected artifact, and decision rule before running the work.
- For app design, record sketches, mockups, generated images, screenshots, visual constraints, and the chosen target before implementation.
- For security work, record assets, potential attack paths, assumptions, evidence, mitigations, and what remains untested.
- For implementation, record commits, commands, test output, reviewer findings, rejected alternatives, and recovery notes.
- For research, record sources, claims, confidence, contradictions, and unresolved questions.

If substantial work starts before a record entry exists, pause and write the intent down first. The record is the write-ahead note that makes later claims auditable.

## Migration From ExecPlan Or AutoPlan

When upgrading older `execplan` or `autoplan` files into Plans.md, preserve the useful intent and evidence while adopting the simpler names used here.

- Convert an old root AutoPlan into a root `plans.md` when it coordinates several child plan folders.
- Convert old workstreams into child plan folders with `plan.md` and, when useful, `record.md`.
- Convert "loop ledgers", "ledgers", and similar history files into `record.md` or `records.md`.
- Keep the implementation-heavy structure from `PLANS.md` when a child plan needs step-by-step implementation detail, but do not preserve `execplan` as a separate naming system unless the repository already depends on it.
- Let the new root `plans.md` define the folder naming convention. Prefer readable names that make priority, date, and lineage clear, rather than carrying forward old labels that no longer explain the work.
- If an old plan is superseded by the new layout, edit the old file or its replacement note so a reader can find the new `plan.md` without reading chat.

## Subagents

Use subagents when they reduce wall-clock time, add independent judgment, or let several child plans advance at once.

- Assign a persistent worker to a child plan when the task is large enough for another capable agent to own end-to-end for several minutes or longer.
- Give a worker the relevant plan path, expected result, validation commands, artifact paths, and any constraints about shared files or worktrees.
- Expect a forked worker to drive its own internal loop inside the assigned task: inspect what it needs, advance the work, validate the result, and return either a meaningful result or a precise blocker.
- Keep useful workers alive. Send follow-up instructions to the same agent when new work continues its existing assignment instead of spawning a near-duplicate.
- Use a separate reviewer for concrete results such as a commit, patch, benchmark result, design artifact, or research conclusion.
- Treat reviewers as usually single-shot. If worker and reviewer disagree, close the reviewer, give the worker the specific feedback, wait for a revision, then review the new result.
- The root agent integrates the result, resolves disagreements, updates the root plan, and decides whether the child plan is complete.

A forked subagent should receive meaningful work. Do not fork an equally capable agent merely to answer a tiny question that the root can answer faster.

When a new repo has no commits yet and Git worktrees would help parallel work, create the plan files and make a small baseline commit before trying to split work across worktrees.

When a repository adopts Plans.md as an ongoing operating model, consider adding or updating repo-local `AGENTS.md`. That file should point to the plan files, explain the local file layout, and say how unfinished active plans should be handled. It should not duplicate live status that belongs in the plan files.

## Language Rules

Plans.md must actively prevent semantic collapse: one vague term being reused for the goal, plan, files, agent, task, progress, and evidence until the text sounds organized but stops saying anything.

Write specific prose:

- Name the file, command, module, test, artifact, user-visible behavior, commit, source, or decision.
- Use ordinary language a casual observer can skim.
- Prefer short paragraphs with concrete nouns and verbs.
- Use fragments only when the named reference is clear, for example "`parser-rewrite/plan.md`: ready for review after `cargo test parser` passes."
- Replace vague nouns with the thing meant. Instead of "make progress", write "finish `parser-rewrite/plan.md` through the review step."
- Avoid empty signifiers and planning jargon. If a word does not identify a concrete file, command, artifact, agent, result, or decision, replace it.
- Avoid baroque noun phrases such as "primary objective set", "coordination surface", or "validation model". They are harder to audit than named files and actions.
- Do not invent labels that sound formal unless the plan defines exactly what file, command, agent, artifact, or decision the label names.

If a term appears repeatedly in several meanings, rename the references. Use `plan.md`, `record.md`, child folder names, agent names, commit hashes, command names, and artifact paths.

## Before Work Reaches The Trunk Branch

Before work is merged, rebased, squashed, or pushed directly to the repository's main line, review the final diff.

Plans and records that remain in the repository should help a future reader understand what changed, why it changed, what evidence supports it, and what remains to do. Avoid leaving frequently edited notes, scratch files, large command transcripts, temporary experiment data, or generated comparison files in the trunk branch unless the project intentionally keeps that information in source control.

The right cleanup point depends on the project's workflow. If the project uses squash merges, it may be reasonable to keep detailed records during the branch and then add a cleanup commit before opening or finalizing the pull request. That cleanup should summarize records, move completed plans to the completed location, and remove scratch data that should not become part of the final diff.

If the project uses merge commits, rebases, or direct pushes to the trunk branch, the plan should say upfront how record files and scratch data are handled. Options include committing compact records only, adding scratch paths to `.gitignore`, storing records outside the repository, linking to issues or external documents, or keeping detailed files only when the project explicitly wants them.

When setting up Plans.md in a repository, ask the user which workflow applies and record the answer in the root plan.

## Continue

While executing a plan:

1. Keep the plan current enough that a new agent can continue from it.
2. Move detailed observations into `record.md` or associated files.
3. Keep each child plan narrow enough to finish, but substantial enough to justify its own plan.
4. Update the root `plans.md` when sequencing changes, one child plan blocks another, or a result changes the next useful action.
5. Run the fastest relevant verification loop first, then broader validation when the work is ready.
6. Preserve parallel child-plan structure when it exists. Do not collapse several active child plans into one serial root-only task unless the plan records why.
7. If a new user request would change focus while active plans are unfinished, ask how to handle them unless the user's instruction already makes that clear. Useful options include pausing a plan, moving it to `backlog/`, marking it complete, assigning it to another agent or thread, using a worktree, or using a remote host.
8. When a plan is superseded, canceled, split, merged, or moved, update the old and new plan files so a reader can follow the chain without searching chat.
9. Before ending a turn, check whether each associated plan is in the correct state: backlog for work not started or intentionally deferred, active for work still being advanced, and completed for work that satisfies its definition of done. If the repository uses an external issue tracker or document store instead of folders, update that system according to the root plan.
10. Do not complete a goal, loop, or similar harness-level item while its named plan still appears active. First update `Progress`, `Outcomes and Retrospective`, and any record summary needed for a reader to understand the result. Then move or mark the plan completed.
11. Stop only when the plan reaches its acceptance criteria, the user changes direction, or a real blocker needs user input.

## References

- `references/PLANS.md`: the implementation-oriented plan skeleton.
- `references/record-patterns.md`: examples for choosing a record format.
