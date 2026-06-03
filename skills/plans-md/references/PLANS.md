# Plans.md Requirements

This document describes the requirements for plan files that a coding agent or human novice can follow to deliver working behavior. Treat the reader as a complete beginner to this repository: they have only the current working tree and the plan files you provide. They have no memory of prior plans and no external context unless a plan file names that context explicitly.

Use `plan.md` for one meaningful piece of work. Use a root `plans.md` when several child plan folders need coordination. Use `record.md` for dense supporting material for one plan. Use root `records.md` only when root-level notes would make `plans.md` hard to skim.

## How To Use Plans.md

When authoring a plan, follow this document to the letter. If it is not in your context, read the entire file again before drafting. Be thorough in reading and rereading source material so the plan is accurate. Start from the skeleton below and flesh it out as you learn the repository.

Before creating a new plan, search for existing related plans. Extend an existing plan when it covers the same work. If several existing plans could apply, choose the best match and record the reason in `Decision Log` so a later reader understands why the plan set did not split into overlapping promises.

When implementing a plan, do not prompt the user for "next steps" unless the user asked for planning only or a real blocker requires user input. Proceed to the next milestone. Keep all living sections up to date. Add or split entries in `Progress` at every stopping point so the file affirmatively states what changed and what remains. Resolve ordinary ambiguity inside the plan and record why.

When discussing a plan, record decisions in the plan for posterity. It should be unambiguously clear why any change to the plan was made. Plans are living documents, and it should always be possible to restart from the plan files and no chat transcript.

When researching a design with challenging requirements or significant unknowns, use milestones to implement proof-of-concept work that validates whether the proposal is feasible. Read source code of libraries by finding or acquiring them, research deeply, and include prototypes only when they will guide the full implementation.

## Requirements

Non-negotiable requirements:

- Every plan must be fully self-contained. In its current form it must contain all knowledge and instructions needed for a novice to succeed.
- Every plan is a living document. Contributors are required to revise it as progress is made, discoveries occur, and decisions are finalized. Each revision must remain fully self-contained.
- Every plan must enable a complete novice to implement the work end-to-end without prior knowledge of this repo.
- Every plan must produce demonstrably working behavior, not merely code changes that "meet a definition."
- Every plan must define every term of art in plain language or avoid the term.
- Every split plan must include a `## Plan Layout` section that names the files or filename patterns that make up the plan.
- Every plan must define what "done" means. "Done" may be an empirical test, an observable behavior, a written rubric, or a combination of those. Qualitative work still needs an explicit rubric.

Purpose and intent come first. Begin by explaining, in a few sentences, why the work matters from a user's perspective: what someone can do after this change that they could not do before, and how to see it working. Then guide the reader through the exact steps to achieve that outcome, including what to edit, what to run, and what they should observe.

The agent executing your plan can list files, read files, search, run the project, and run tests. It does not know any prior context and cannot infer what you meant from earlier notes. Repeat every assumption you rely on. Do not point to external blogs or docs as required reading; if knowledge is required, embed it in the plan in your own words. If a plan builds upon a prior checked-in plan, incorporate that file by reference and summarize the facts needed by a new reader. If the prior plan is not checked in, include all relevant context from it.

## Formatting

Format and envelope are simple and strict. When writing a plan inside another Markdown document, put the entire plan in one fenced code block labeled `md`. Do not nest additional triple-backtick fences inside that block. When you need to show commands, transcripts, diffs, or code, present them as indented blocks within the plan. When writing a Markdown file whose content is only the plan, omit the outer triple backticks.

Use two newlines after every heading. Use `#`, `##`, and lower headings normally. Write in plain prose. Prefer sentences over lists. Avoid checklists, tables, and long enumerations unless prose would obscure the information. Checklists are permitted in `Progress`, where they are mandatory. Narrative sections must remain prose-first.

## Guidelines

Self-containment and plain language are paramount. If you introduce a phrase that is not ordinary English, define it immediately and explain how it appears in this repository by naming the files, commands, or behavior. Do not say "as defined previously" or "according to the architecture doc." Include the needed explanation here, even if that repeats information from elsewhere.

Avoid common failure modes. Do not rely on undefined jargon. Do not describe a feature so narrowly that the resulting code compiles but does nothing meaningful. Do not outsource key decisions to the reader. When ambiguity exists, resolve it in the plan itself and explain why you chose that path. Err on the side of over-explaining user-visible effects and under-specifying incidental implementation details.

Anchor the plan with observable outcomes. State what the user can do after implementation, the commands to run, and the outputs they should see. Acceptance should be phrased as behavior a human can verify, such as "after starting the server, navigating to http://localhost:8080/health returns HTTP 200 with body OK," rather than internal attributes such as "added a HealthCheck struct." If a change is internal, explain how its impact can still be demonstrated, for example by running tests that fail before and pass after, and by showing a scenario that uses the new behavior.

Specify repository context explicitly. Name files with repository-relative paths, name functions and modules precisely, and describe where new files should be created. If touching multiple areas, include a short orientation paragraph that explains how those parts fit together so a novice can navigate confidently. When running commands, show the working directory and exact command line. When outcomes depend on environment, state the assumptions and provide alternatives when reasonable.

Be idempotent and safe. Write steps so they can be run multiple times without causing damage or drift. If a step can fail halfway, include how to retry or adapt. If a migration or destructive operation is necessary, spell out backups or safe fallbacks. Prefer additive, testable changes that can be validated as you go.

Validation is not optional. Include instructions to run tests, to start the system if applicable, and to observe it doing something useful. Describe comprehensive testing for new features or capabilities. Include expected outputs and error messages so a novice can tell success from failure. Where possible, show how to prove the change is effective beyond compilation, such as through a small end-to-end scenario, a CLI invocation, or an HTTP request and response. State the exact test commands appropriate to the project's toolchain and how to interpret their results.

Capture evidence. When your steps produce terminal output, short diffs, logs, screenshots, or generated files, include concise references in `record.md`, `records.md`, or `Artifacts and Notes`. Keep evidence focused on what proves success. If you need to include a patch, prefer file-specific diffs or small excerpts that a reader can recreate by following your instructions rather than pasting large blobs.

Distinguish observable facts from inferred judgments. "Command X passed with output Y" is an observable fact. "This is probably enough" is a judgment. Plans may include both, but they must be labeled clearly enough that another reader can tell what was seen and what was concluded.

## Stable Sections And Mutable Sections

Plans prevent drift by separating information that should remain mostly stable from information that should change frequently.

Stable sections include purpose, desired state, definition of done, plan layout, work boundaries, milestones, and validation strategy. Revise these when the work genuinely changes, but record the reason in `Decision Log`.

Mutable sections include progress, surprises and discoveries, decision log entries, records, current blockers, current evidence, and outcomes. Update these as work proceeds. Do not rewrite stable sections merely because implementation was messy; put the mess in mutable sections and change stable sections only when the plan itself needs to change.

## Plan Layout

Use this section whenever a plan is split across multiple files. The `## Plan Layout` section belongs in the root `plans.md` for a multi-plan directory. It must name the exact files or the filename patterns. A reader should know where to find the root plan, root record, child plans, child records, and associated files without searching the repository.

For a single-file plan, this section can be one sentence naming the file. For several child plans, it should describe the directory grouping, naming convention, and how child folders move between groups.

Choose the simplest layout that keeps files readable. Start with fewer files when the work is small. Split into `records.md` or child plan folders when the current file is becoming hard to skim or when locality of information would prevent mistakes. Do not create multiple sources of truth; the root `plans.md` should say which file owns which information.

The root plan chooses the naming convention. Dates, priority labels, and short descriptive names are often useful, but this document does not enforce one global convention. Names should sort naturally in the order the user cares about. For active and backlog plans, priority then date is often useful, such as `P0-2026-06-01-parser-rewrite`. For completed plans, date then priority is often useful, such as `2026-06-01-P0-parser-rewrite`.

Prefer `backlog/`, `active/`, and `completed/` folders when there are enough child plans to need grouping. The root plan should define what each folder means for the repository and how plans move between them.

Example:

    docs/plans/
      plans.md
      records.md
      backlog/
        P1-2026-06-02-billing-ui/
          plan.md
          record.md
          mockup.png
      active/
        P0-2026-06-02-parser-rewrite/
          plan.md
          record.md
      completed/
        2026-06-01-P0-remove-deprecated-api/
          plan.md
          record.md

### `plans.md`

The root `plans.md` explains the overall goal, folder naming convention, active child plans, blocked child plans, child plans that can proceed in parallel, and validation for the combined result. It coordinates child plans. It should not duplicate their detailed history.

### `records.md`

The root `records.md` stores cross-plan notes: launches, merges, reviewer summaries, major decisions, and evidence that affects more than one child plan. Use `records.md` when those notes would otherwise make `plans.md` hard to skim. If root-level history is short, keep it inside `plans.md` instead.

Do not let root `records.md` become a diary of every experiment or every command. Detailed evidence belongs near the plan it supports. The root record is for information that affects more than one child plan or explains coordination decisions a future reader must understand.

Child folders usually use singular `record.md` because each file supports one `plan.md`. The child `record.md` should contain the evidence and scratchpad material for that child plan: commands, commits, measurements, screenshots, sources, hypotheses, rejected alternatives, reviewer notes, and artifact links.

## Work Boundaries

Every child plan should state the files, modules, commands, systems, or questions it is expected to touch. If there are important out-of-bounds areas, name them too. These boundaries help parallel work avoid collisions and make review easier.

When work is delegated to several agents, people, devboxes, branches, worktrees, remote hosts, or issue-tracker owners, make ownership explicit in the relevant plan or record. Prefer durable identifiers such as names, usernames, branches, issue links, hostnames, or worktree paths. Ephemeral subagent handles usually do not belong in long-lived plan files unless they are needed to understand current coordination.

Preserve parallel child-plan structure when it exists. If several active child plans can move independently, the root `plans.md` should keep that fact visible. If one child plan blocks another, record the dependency in the affected plans.

If a new user request would change focus while active child plans are unfinished, the plan files should record how those plans were handled: continued, paused, moved to backlog, completed, delegated elsewhere, or intentionally abandoned. The goal is to avoid silent unfinished work.

## Records And Preregistration

Records are support material for plans. They should be dense, local to the plan they support, and organized in whatever format the plan declares.

Before running a substantial experiment, optimization attempt, security probe, design exploration, or research comparison, preregister the intent in the relevant `record.md` or associated file. The entry should explain what question is being tested, how it will be tested, what evidence would count, and how the result will change the next step. This is a write-ahead note, not an after-the-fact summary.

After substantial work, update the plan and record enough information that a reader can understand the current state from the files alone. The exact fields depend on the work, but the reader should be able to find what changed, what evidence was gathered, what conclusion was drawn, and the next concrete action.

Each substantial attempt should end with an explicit next action. The wording may vary, but it must be concrete enough to act on: continue with a named step, retry with a named correction, change approach for a stated reason, pause for a blocker, or mark the plan complete.

## Milestones

Milestones are narrative, not bureaucracy. If you break the work into milestones, introduce each with a brief paragraph that describes what will exist at the end of the milestone that did not exist before, the commands to run, and the acceptance you expect to observe. Keep it readable as a story: goal, work, result, proof.

Progress and milestones are distinct. Milestones tell the story. Progress tracks granular work. Both must exist. Never abbreviate a milestone merely for brevity, and do not leave out details that could be crucial to a future implementation.

Each milestone must be independently verifiable and must incrementally implement the overall goal of the plan.

## Living Plans And Design Decisions

Plans are living documents. As you make key design decisions, update the plan to record both the decision and the thinking behind it. Record all decisions in `Decision Log`.

Plans must contain and maintain `Progress`, `Surprises and Discoveries`, `Decision Log`, and `Outcomes and Retrospective`. These are not optional.

When you discover optimizer behavior, performance tradeoffs, unexpected bugs, dependency behavior, or recovery semantics that shaped your approach, capture those observations in `Surprises and Discoveries` with short evidence snippets. Test output is ideal.

If you change course mid-implementation, document why in `Decision Log` and reflect the implications in `Progress`. Plans are guides for the next contributor as much as checklists for the current agent.

At completion of a major task or the full plan, write an `Outcomes and Retrospective` entry summarizing what was achieved, what remains, and lessons learned.

## Definition Of Done And Validation

Every plan needs a definition of done. For deterministic work, this should be grounded in empirical tests: commands, expected outputs, file contents, benchmark thresholds, screenshots, API responses, or observable user behavior.

For qualitative work, write a rubric. The rubric should say what a good result must satisfy and how a reviewer should judge it. Examples include research completeness, proposal clarity, architecture coherence, design quality, security coverage, or user experience. Do not leave the rubric implicit in chat.

Name the fastest current check separately from broader final validation. The fastest check is the command, review, screenshot, local run, or focused probe that gives useful feedback during iteration. Final validation is the stronger evidence needed before calling the plan done.

Child plans should include their own definition of done, main validator, and fastest current check. These can be short, but they must be concrete enough that another agent or person can judge progress without asking the original author.

## Prototyping And Parallel Implementations

It is acceptable and often encouraged to include explicit prototyping milestones when they reduce risk in a larger change. Examples include adding a low-level operator to a dependency to validate feasibility, or exploring two composition orders while measuring optimizer behavior. Keep prototypes additive and testable. Clearly label the work as prototyping, describe how to run and observe results, and state the criteria for promoting or discarding the prototype.

Prefer additive code changes followed by removals that keep tests passing. Parallel implementations, such as keeping an adapter alongside an older path during migration, are fine when they reduce risk or enable tests to continue passing during a large migration. Describe how to validate both paths and how to retire one safely with tests. When working with multiple new libraries or feature areas, consider independent probes that prove external libraries perform as expected and implement the features needed in isolation.

## Skeleton Of A Good Plan

    # <Short, action-oriented description>

    This plan is a living document. The sections `Progress`, `Surprises and Discoveries`, `Decision Log`, and `Outcomes and Retrospective` must be kept up to date as work proceeds.

    If a PLANS.md file is checked into the repo, reference the path to that file here from the repository root and note that this document must be maintained in accordance with PLANS.md.

    ## Purpose / Big Picture

    Explain in a few sentences what someone gains after this change and how they can see it working. State the user-visible behavior you will enable.

    ## Plan Layout

    If this is a single-file plan, name the file. If this plan is split across files, name the root plan, root record, child folder pattern, child plan files, child record files, and associated files.

    Example for split plans:

        Root plan: `docs/plans/plans.md`
        Root record: `docs/plans/records.md`
        Active child plans: `docs/plans/active/P#-YYYY-MM-DD-<topic>/plan.md`
        Active child records: `docs/plans/active/P#-YYYY-MM-DD-<topic>/record.md`
        Backlog child plans: `docs/plans/backlog/P#-YYYY-MM-DD-<topic>/plan.md`
        Completed child plans: `docs/plans/completed/YYYY-MM-DD-P#-<topic>/plan.md`

    ## Work Boundaries

    Name the files, modules, commands, systems, or questions this plan is expected to touch. Name important out-of-bounds areas.

    ## Definition Of Done

    Define done by empirical tests, observable behavior, a rubric, or a combination. Name the main validator and the fastest current check.

    ## Progress

    Use a list with checkboxes to summarize granular steps. Every stopping point must be documented here, even if it requires splitting a partially completed task into two entries, one for what is done and one for what remains. This section must always reflect the actual current state of the work.

    - [x] (2026-06-01 13:00Z) Example completed step.
    - [ ] Example incomplete step.
    - [ ] Example partially completed step (completed: X; remaining: Y).

    Use timestamps to measure rates of progress.

    ## Surprises and Discoveries

    Document unexpected behaviors, bugs, optimizations, or insights discovered during implementation. Provide concise evidence.

    - Observation: ...
      Evidence: ...

    ## Decision Log

    Record every decision made while working on the plan in the format:

    - Decision: ...
      Rationale: ...
      Date/Author: ...

    ## Outcomes and Retrospective

    Summarize outcomes, gaps, and lessons learned at major milestones or at completion. Compare the result against the original purpose.

    ## Context and Orientation

    Describe the current repository state relevant to this task as if the reader knows nothing. Name key files and modules by repository-relative path. Define any non-obvious term you will use. Do not refer to prior chat.

    ## Plan of Work

    Describe, in prose, the sequence of edits and additions. For each edit, name the file and location, such as function or module, and what to insert or change. Keep it concrete and minimal.

    ## Concrete Steps

    State the exact commands to run and where to run them. When a command generates output, show a short expected transcript so the reader can compare. This section must be updated as work proceeds.

    ## Validation and Acceptance

    Describe how to start or exercise the system and what to observe. Phrase acceptance as behavior, with specific inputs and outputs. If tests are involved, say which command to run and what must pass.

    ## Idempotence and Recovery

    If steps can be repeated safely, say so. If a step is risky, provide a safe retry or rollback path. Keep the environment clean after completion.

    ## Artifacts and Notes

    Include the most important transcripts, diffs, screenshots, generated files, or snippets. Keep them concise and focused on what proves success. If this plan has a `record.md` or `records.md`, name it here and say what evidence belongs there.

    ## Next Action

    State the next concrete action after each substantial attempt. The next action should be specific enough for another reader to continue without asking what "keep going" means.

    ## Interfaces and Dependencies

    Be prescriptive. Name the libraries, modules, and services to use and why. Specify the types, traits, interfaces, and function signatures that must exist at the end of the milestone. Prefer stable names and paths such as `crate::module::function` or `package.submodule.Interface`.

    For example, in `crates/foo/planner.rs`, define:

        pub trait Planner {
            fn plan(&self, observed: &Observed) -> Vec<Action>;
        }

If you follow the guidance above, a single stateless agent or a human novice can read your plan from top to bottom and produce a working, observable result. That is the bar: self-contained, self-sufficient, novice-guiding, and outcome-focused.

When you revise a plan, ensure your changes are reflected across all relevant sections, including the living document sections. Write a note at the bottom of the plan describing the change and the reason why. Plans must describe not just what changed but why for almost everything.
