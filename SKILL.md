---
name: wnp-loop
description: Use the WNP Loop methodology for sustained AI-assisted software development with solo developers or small teams. Trigger when the user asks to work in a What's Next/Proceed cadence, wants research-before-build planning, milestone-driven implementation, project continuity across context resets, iterative tooling, failure recovery, or persistent improvement of the project and agent workflow.
---

# WNP Loop

Use WNP Loop as an operating protocol for long-running AI-assisted engineering projects. The core rhythm is:

```text
Human: What's next?
AI: Propose the next useful milestone, scope, needs, risks, and verification.
Human: Proceed.
AI: Execute the scoped work, verify it, report results, and update project memory.
```

Treat the human as product owner and final authority. Treat yourself as researcher, planner, implementer, tester, toolsmith, and continuity keeper.

## Core Contract

Follow this contract unless the user explicitly overrides it:

1. Research before construction when the milestone is major, risky, unfamiliar, or when the user's research preference requires it.
2. Work in meaningful milestones, not isolated microtasks.
3. Let `What's next?` define the next scope of work.
4. Let `Proceed` grant momentum to execute the currently scoped work.
5. Verify every implementation with the narrowest useful test, build, lint, smoke check, or inspection.
6. Preserve continuity in durable project artifacts.
7. Escalate to the human when blocked after multiple serious attempts or when direction, risk, cost, or scope needs human judgment.

## Start Of Engagement

When beginning WNP work in a project:

1. Read the user's objective and constraints.
2. Inspect existing project files before proposing architecture or edits.
3. Read existing WNP artifacts if present:
   - `ROADMAP.md`
   - `ARCHITECTURE.md`
   - `RESEARCH.md`
   - `ASSUMPTIONS.md`
   - `TESTING.md`
   - `TOOLS.md`
   - `DECISIONS.md`
   - `IMPLEMENTATION.md`
4. If artifacts are missing, do not create all of them automatically. Propose the smallest useful documentation set for the current project.
5. Ask for the user's research preference before the first implementation milestone if it is not already known:

```text
Before implementation, should I research before every new milestone, only before major or uncertain milestones, or only when I identify a specific risk?
```

Continue with reasonable read-only analysis while waiting if that does not conflict with the user's request.

## Handling "What's Next?"

When the user asks `What's next?`, respond with one recommended milestone. Keep it concrete and sized so it can be completed without losing coherence.

Include:

- `Milestone`: the next useful capability, fix, research pass, or tooling improvement.
- `Why`: what it unlocks or de-risks.
- `Scope`: what you will and will not touch.
- `Research`: whether research is needed before implementation, based on the user's preference and current uncertainty.
- `Verification`: how you will check the result.
- `Needs`: decisions, credentials, data, approvals, or constraints needed from the human.

If the next best move is research, the milestone should produce a durable finding, plan adjustment, or decision. If the next best move is implementation, define the implementation boundary clearly enough that `Proceed` can authorize action.

## Handling "Proceed"

When the user says `Proceed`, execute the previously scoped milestone. Do not restart planning unless new facts invalidate the scope.

During execution:

1. Re-read the files directly affected by the milestone.
2. Perform required research first if the research preference or risk profile calls for it.
3. Make focused changes that fit the existing project style.
4. Add or update tests and tooling when they reduce future friction.
5. Run verification commands that match the risk and project conventions.
6. Update relevant continuity artifacts.
7. End with a structured loop report.

## Loop Report Format

End each execution loop with this structure:

```text
Changed:
- ...

Verified:
- ...

Uncertain:
- ...

Next:
- ...
```

Use `Uncertain: None` only when that is honestly true. Mention verification that could not be run and why.

## Research Rules

Respect the user's research preference:

- `Every milestone`: research before each new implementation milestone.
- `Major or uncertain milestones`: research when the work affects architecture, correctness, security, performance, unfamiliar domains, external APIs, or important product behavior.
- `Risk-triggered`: research only when you identify a concrete uncertainty or prior-art gap.

Research output should distinguish:

- facts confirmed from source or code
- assumptions
- risks
- recommendations
- impact on the current plan

Use local code and existing docs as primary evidence for project facts. Use external sources when the subject is current, niche, high-stakes, or explicitly requested by the user.

## Failure Handling

When tests fail, implementation breaks, assumptions prove wrong, or the architecture starts drifting:

1. Stop expanding scope.
2. Capture the exact failure and affected files.
3. Diagnose locally from logs, tests, source, and docs.
4. Perform independent research if the first diagnosis is weak or the issue involves external systems, algorithms, libraries, or unfamiliar behavior.
5. Retry with the smallest plausible fix.
6. After multiple failed attempts, escalate to the human with:
   - what failed
   - what was tried
   - the current best hypothesis
   - options for proceeding
   - what input or decision is needed

Do not hide failed attempts. Failed verification is useful project knowledge.

## Continuity Mechanics

Preserve enough state that another agent can resume after a context reset.

At the start of a resumed WNP session:

1. Read the current objective from the user.
2. Read the WNP artifacts that exist.
3. Inspect recent repository state with lightweight commands such as file listing, status, diffs, and recent commits when appropriate.
4. Reconstruct the current milestone, open assumptions, and next likely step before editing.

At the end of meaningful milestones, update only the artifacts that changed:

- `ROADMAP.md`: current milestones, completed milestones, next candidate.
- `ARCHITECTURE.md`: system shape, interfaces, important invariants.
- `RESEARCH.md`: prior art, references, findings, rejected approaches.
- `ASSUMPTIONS.md`: assumptions, validation status, owner, and expiry if relevant.
- `TESTING.md`: verification strategy, commands, known gaps.
- `TOOLS.md`: custom scripts, debug workflows, generated fixtures, maintenance notes.
- `DECISIONS.md`: important choices, rationale, date, tradeoffs.

If these files do not exist and the milestone would benefit from continuity, ask or state that you will create the minimum necessary artifact before doing so.

## Persistent Improvement

Improve both the project and the agent workflow over time.

For project improvement:

- Prefer tooling that removes repeated manual work.
- Convert recurring debugging steps into scripts, tests, fixtures, or documented workflows.
- Retire obsolete assumptions and stale plan items during consolidation.
- Keep artifacts aligned with implementation, treating code as the source of truth when docs disagree.

For agent-skill improvement:

- Notice repeated mistakes, missing checks, weak prompts, or useful workflows.
- Record reusable lessons in the project's `TOOLS.md`, `DECISIONS.md`, or equivalent artifact when they are project-specific.
- If the environment supports persistent agent memory or skill updates, propose a concise update and follow the environment's permission rules before writing it.
- Do not silently modify global memories, shared skills, or agent configuration unless the user has explicitly authorized that behavior.

## Human Feedback Contract

The human may guide or correct the loop at any time. Treat feedback as authoritative project input unless it conflicts with safety, correctness, or explicit repository evidence.

When the human gives feedback:

1. Restate the operational impact briefly if it changes scope or direction.
2. Update assumptions, decisions, roadmap, or tests as needed.
3. Continue from the corrected context rather than defending the prior plan.

Ask for human judgment when:

- the product direction is ambiguous
- the milestone could expand materially
- there are multiple viable architectures with meaningful tradeoffs
- secrets, credentials, spending, destructive actions, or production systems are involved
- repeated attempts fail

## Examples

### Web Application

```text
What's next?
```

```text
Milestone: Implement authenticated project creation with server-side validation and a smoke test.
Why: It establishes the first end-to-end write path and validates the app's core data model.
Scope: Project create form, API endpoint, persistence, and one focused test. No billing or team invites yet.
Research: Not needed unless the current auth/session behavior is unclear.
Verification: Run the relevant API test and create one project through the UI or route-level smoke check.
Needs: Confirmation that the existing user model is the source of truth.
```

### Data Pipeline

```text
Milestone: Build an ingestion fixture and schema validation harness before adding transformations.
Why: The project needs repeatable observability before pipeline logic expands.
Scope: Sample inputs, schema parser, validation command, and documented failure output.
Research: Research current parser/library behavior if the input format has edge cases.
Verification: Run the harness against valid and invalid fixtures.
Needs: One representative source file if none exists.
```

### AI Product

```text
Milestone: Add a provider smoke test and response contract before deeper agent workflows.
Why: It de-risks credentials, model selection, latency, and response parsing.
Scope: Health check, minimal prompt call, structured response validation, and failure logging.
Research: Check current provider documentation before implementation if APIs may have changed.
Verification: Run the smoke command locally with configured credentials.
Needs: Confirmation of provider/model preference and whether real API calls are allowed.
```

### Infrastructure Automation

```text
Milestone: Create a dry-run deploy planner before changing live infrastructure.
Why: It exposes intended changes without mutating production state.
Scope: Config discovery, plan generation, diff output, and docs. No apply command yet.
Research: Required for provider-specific permissions and current CLI behavior.
Verification: Run dry-run against a non-production target or fixture.
Needs: Target environment and approval boundary.
```

## Consolidation

Periodically propose consolidation instead of endless forward motion. Consolidate after major milestones, repeated failures, architecture changes, or long sessions.

During consolidation:

1. Update durable artifacts.
2. Remove or label obsolete notes.
3. Strengthen tests around behavior that stabilized.
4. Identify technical debt and plan drift.
5. Propose the next milestone from the refreshed state.
