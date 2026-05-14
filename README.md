# WNP Loop: A Proposal for Iterative AI-Assisted Development

## Abstract

The WNP Loop, short for "What's Next, Proceed," is an AI-assisted development methodology built around a simple operating rhythm:

1. Define a meaningful technical objective.
2. Ask the AI to research existing solutions and relevant prior art.
3. Form an implementation plan.
4. Execute in repeated cycles of "what's next" and "proceed."

The method is designed for complex, exploratory engineering work where the final shape of the system cannot be fully known at the beginning. It has been especially useful for projects such as emulator design, kernel development, systems tooling, and other domains where progress depends on incremental discovery, disciplined implementation, and frequent reassessment.

WNP treats the AI not as a one-shot code generator, but as a continuously engaged engineering collaborator. The human remains the product owner, taste-maker, constraint-setter, and final authority. The AI acts as researcher, planner, implementer, tester, toolsmith, and continuity engine.

## Core Idea

Most AI development workflows overemphasize the initial prompt. WNP instead emphasizes the loop.

The initial prompt establishes direction:

> We need to build X. Research existing solutions and research, then form a plan for implementing X.

After that, work advances through a repeating sequence:

> What's next?

> Proceed.

The simplicity is intentional. The human does not need to micromanage every implementation step. The AI is expected to maintain context, identify the next useful milestone, execute it, report results, and surface blockers.

## Why WNP Exists

Complex software rarely unfolds according to a perfect up-front plan. This is especially true in low-level, research-heavy, or architecture-heavy domains. Emulator development, kernel work, compiler work, protocol design, robotics, and tooling often involve:

- incomplete requirements
- hidden technical constraints
- evolving architecture
- unknown unknowns
- long chains of dependent milestones
- frequent need for custom debugging and inspection tools

WNP provides a disciplined way to work with AI in these conditions. It lets the AI use its strengths in research, synthesis, implementation, and tireless iteration while preserving human oversight at the decision points that matter.

## Principles

### 1. Research Before Construction

WNP begins by asking the AI to investigate prior art, existing implementations, papers, tools, libraries, protocols, and known pitfalls before committing to a design.

The goal is not to outsource judgment, but to avoid naive implementation.

### 2. Plan, Then Iterate

The AI should produce an initial plan, but the plan is not sacred. It is a working map. Each loop may revise the plan based on test results, implementation discoveries, or new constraints.

### 3. Milestones Over Tasks

WNP works best when progress is organized into milestones rather than tiny instructions. A milestone should produce a meaningful improvement in capability, understanding, correctness, or tooling.

### 4. The AI Owns the Next Step

After the initial direction is set, the human can ask:

> What's next?

The AI should answer with the most valuable next milestone, explain why it matters, and identify what it needs to complete it.

### 5. The Human Grants Momentum

Once the next step is reasonable, the human can simply say:

> Proceed.

This keeps the work moving without forcing the human to continuously decompose the project.

### 6. Tooling Is Part of the Work

The AI should be encouraged to build scripts, tests, visualizers, harnesses, fuzzers, profilers, fixtures, debug views, and other support tools when they reduce future friction.

In WNP, tooling is not a detour. It is often the path.

### 7. Ask for Needs, Not Just Status

Useful check-ins include:

> What do you need to complete the next milestone?

> What is blocking progress?

> What tool would make the next stage easier?

> What assumption should we verify before continuing?

These questions help the AI externalize hidden dependencies and avoid grinding forward blindly.

## The WNP Lifecycle

### Phase 1: Objective Declaration

The human defines the target system or capability.

Example:

```text
We need to build a Game Boy emulator. Research existing emulator designs, documentation, timing models, CPU behavior, graphics pipelines, and test ROM strategies. Then form a plan for implementing it.
```

The objective should name the desired outcome, relevant constraints, and any known preferences.

### Phase 2: Research and Prior Art

The AI investigates:

- existing projects
- technical references
- academic or industry research
- standard architectures
- common bugs and traps
- compatibility test suites
- useful libraries or tooling

The output should distinguish facts, assumptions, risks, and recommendations.

### Phase 3: Implementation Plan

The AI proposes:

- major milestones
- architecture
- data model
- testing strategy
- tooling strategy
- risk areas
- first implementation step

The plan should be actionable but flexible.

### Phase 4: WNP Execution Loop

The loop repeats:

```text
Human: What's next?
AI: The next milestone is Y because it unlocks Z. I need A, B, and C to complete it.
Human: Proceed.
AI: Implements, tests, reports results, updates plan.
```

Each loop should end with:

- what changed
- what was verified
- what remains uncertain
- what the next likely milestone is

### Phase 5: Tooling Expansion

At any point, the human may ask:

```text
Go ahead and implement more tooling that will ease your development process.
```

The AI should then identify development bottlenecks and build tooling to reduce them.

Examples:

- emulator instruction trace diffing
- kernel boot log parsers
- binary inspection tools
- automated test runners
- state snapshot visualizers
- fuzzing harnesses
- CI checks
- fixture generators
- benchmarking scripts

### Phase 6: Consolidation

Periodically, the AI should consolidate progress:

- update documentation
- summarize architecture
- retire obsolete assumptions
- clean up temporary experiments
- strengthen tests
- identify technical debt
- reset the roadmap

This prevents long-running AI sessions from accumulating drift.

## Recommended Prompt Pattern

### Initial Prompt

```text
We need to build [X].

Research existing solutions, relevant technical references, common implementation strategies, known pitfalls, and available tooling.

Then form a milestone-based plan for implementing [X]. Include testing strategy, tooling needs, risks, and the first recommended milestone.
```

### Loop Prompt

```text
What's next?
```

### Execution Prompt

```text
Proceed.
```

### Resource Prompt

```text
What do you need to complete the next milestone?
```

### Tooling Prompt

```text
Go ahead and implement more tooling that will ease your development process.
```

### Reassessment Prompt

```text
Reassess the plan based on what we have learned so far. What should change?
```

## Roles

### Human Role

The human is responsible for:

- defining the objective
- clarifying taste, constraints, and priorities
- approving major direction changes
- deciding when quality is sufficient
- noticing when the AI is optimizing for the wrong thing
- providing domain preferences or project-specific judgment

### AI Role

The AI is responsible for:

- researching before building
- maintaining the working plan
- identifying the next useful milestone
- implementing changes
- writing and running tests
- building support tooling
- reporting uncertainty honestly
- asking for missing information when needed
- preserving project continuity

## Artifacts

A mature WNP project should accumulate durable artifacts:

- `ROADMAP.md`: current milestone plan
- `ARCHITECTURE.md`: system design and major decisions
- `RESEARCH.md`: references, prior art, and findings
- `ASSUMPTIONS.md`: known assumptions and validation status
- `TESTING.md`: how correctness is verified
- `TOOLS.md`: custom development tools and workflows
- `DECISIONS.md`: important choices and rationale

These files help the loop survive context resets, collaborator changes, and long development timelines.

## What Makes a Good WNP Milestone

A good milestone is:

- concrete enough to implement
- meaningful enough to matter
- testable or observable
- connected to the larger goal
- small enough to complete without losing coherence

Poor milestone:

```text
Make the emulator better.
```

Good milestone:

```text
Implement CPU instruction decoding for the documented opcode table, add unit tests for representative instructions, and create a trace format that can later be compared against known-good emulator output.
```

## Strengths

WNP is especially strong when:

- the project is complex and iterative
- the human wants momentum without micromanagement
- research and implementation are interleaved
- correctness depends on custom tests or diagnostics
- the project benefits from internal tooling
- the end state is known but the path is uncertain

## Weaknesses and Risks

WNP can fail when:

- the objective is too vague
- the AI is allowed to proceed without verification
- the human never reviews major assumptions
- milestones become too large
- tooling work becomes disconnected from product progress
- the AI keeps coding around a bad architecture
- documentation is not periodically consolidated

The antidote is regular reassessment.

## Comparison to Other AI Methodologies

Many AI methodologies emphasize structured phases, named roles, or formal artifacts. WNP is lighter. Its core contribution is not a large framework, but a repeatable cadence.

It can coexist with heavier methodologies. For example:

- use a formal planning method to define requirements
- use WNP to drive implementation
- use review-oriented methods for quality gates
- use documentation methods for consolidation

WNP is best understood as an execution loop for sustained AI collaboration.

## Example: Emulator Project

```text
Human:
We need to build a 6502 emulator. Research existing solutions and documentation, then form a plan.

AI:
Researches CPU manuals, known emulator projects, timing behavior, decimal mode quirks, interrupt handling, test ROMs, and trace comparison strategies.
Produces a milestone plan.

Human:
What's next?

AI:
The next milestone is implementing the CPU state model and instruction decode table because all execution, tracing, and testing depend on it.

Human:
Proceed.

AI:
Implements the state model, opcode metadata, initial decode tests, and a trace output format.

Human:
What do you need to complete the next milestone?

AI:
Needs a known-good instruction behavior reference and a decision on whether cycle accuracy is required immediately or after functional correctness.
```

## Example: Kernel Project

```text
Human:
We need to build a small hobby kernel. Research boot protocols, existing minimal kernels, memory maps, interrupt handling, and debugging workflows. Then form a plan.

AI:
Creates a plan covering bootloader choice, target architecture, build system, serial logging, early memory management, interrupt descriptor table, and test strategy.

Human:
What's next?

AI:
The next milestone is a reproducible boot path with serial logging because every later subsystem needs reliable observability.

Human:
Proceed.

AI:
Implements the boot scaffold, serial output, QEMU launch script, and smoke test that checks for expected boot logs.
```

## Adoption Guide

To adopt WNP:

1. Start with a clear objective.
2. Require research before implementation.
3. Ask for a milestone plan.
4. Use "what's next" to let the AI identify the next useful move.
5. Use "proceed" to authorize execution.
6. Periodically ask what the AI needs.
7. Encourage tooling when friction appears.
8. Consolidate documentation after major milestones.
9. Reassess the plan when new information appears.

## Minimal WNP Contract

A project is using WNP if it follows this contract:

```text
The AI must research before building, maintain a milestone-based plan, propose the next useful step, proceed with implementation when authorized, verify its work, and update the project understanding after each loop.
```

## Conclusion

The WNP Loop is a lightweight methodology for sustained AI-assisted development. Its power comes from a small conversational rhythm that creates momentum:

```text
What's next?
Proceed.
```

Behind that rhythm is a deeper discipline: research before construction, milestones over tasks, tooling as leverage, and regular reassessment. WNP gives human developers a way to collaborate with AI on projects too large, uncertain, or technical for one-shot prompting.

It is not a replacement for judgment. It is a way to keep judgment, implementation, and discovery moving together.
