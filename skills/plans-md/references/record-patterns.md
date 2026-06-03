# Record Patterns

A `record.md` is plan-defined support material. It is not always a ledger, journal, or experiment log. Choose the format that makes the plan easier to audit.

The plan should say what belongs in the record. If the record grows large, split out associated files and link them from both `plan.md` and `record.md`. A reader should be able to understand the state and progress of the plan from the plan file plus the associated files named by the plan.

## General Record

Use for implementation, debugging, cleanup, migrations, and review-heavy work.

Recommended entries:

- Timestamp and authoring agent.
- Starting commit or branch.
- Commands run and why they were selected.
- Test output summaries with paths to full logs when needed.
- Commits, patches, screenshots, generated files, or other artifacts.
- Reviewer findings and the disposition of each finding.
- Decisions made and alternatives rejected.
- Recovery notes for reverting or resuming.

## Experiment Record

Use when trying to prove a performance, reliability, behavior, or product claim.

Before running the experiment, preregister enough information to make the result auditable. Useful entries include:

- Question being tested.
- Hypothesis.
- Starting commit and environment.
- Baseline command and baseline result.
- Planned change or intervention.
- Metric and measurement method.
- Stop condition.
- Decision rule.
- Artifact path for logs, traces, screenshots, or generated data.

After the experiment, record enough information for a reader to understand what happened without chat history. The exact fields depend on the work, but the record should make clear what changed, what evidence was gathered, what conclusion was drawn, and what the next concrete action is.

## Design Record

Use for UI, product, brand, docs presentation, diagrams, and visual assets.

Record:

- Audience and use case.
- Reference images, screenshots, sketches, or generated images.
- The chosen visual target.
- Constraints such as responsive behavior, accessibility, brand rules, and required content.
- Rejected directions and why they were rejected.
- Final screenshots or artifact paths.

## Security Record

Use for security review, threat modeling, incident analysis, and hardening.

Record:

- Assets and trust boundaries.
- Potential attack paths considered.
- Relevant files, endpoints, keys, permissions, and external services.
- Evidence for each finding.
- Mitigations implemented or proposed.
- Tests, repro steps, or commands.
- What remains untested and why.

## Research Record

Use for literature review, vendor comparison, API research, architecture options, and policy questions.

Record:

- Sources with dates and links when applicable.
- Claims extracted from each source.
- Confidence and contradictions.
- Open questions.
- Recommendation and the evidence behind it.
