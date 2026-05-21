---
name: planning-slices
description: Create or update working plan documents that split larger engineering changes into ordered implementation slices. Use when an AI coding agent needs to draft a plan under docs/plans, structure a migration or multi-module feature, track slice progress, record findings between sessions, define verification for each slice, or keep follow-up work recoverable and reviewable.
---

# Planning Slices

Use this skill to write planning documents as working handoff records, not polished proposals. A good plan names the target state, records decisions that matter, then splits the work into small ordered slices that can each become a focused PR, commit, or reviewable checkpoint.

## When Drafting A Plan

Create the plan under `docs/plans/YYYY-MM-DD-<topic>-plan.md` unless the user gives another path.

Start with enough context that a future agent can resume without rediscovering the whole problem:

- `# Title`: name the feature, migration, or validation effort directly.
- `## Summary`: state the target outcome and why the plan exists.
- `## Decision` or `## Decisions`: record choices that are already made.
- `## Scope`: say what is covered and what is explicitly out of scope.
- `## Current State` or `## Behavior To Preserve`: capture the baseline.
- `## Recommended Approach` or `## Implementation Shape`: describe the intended architecture.
- `## Testing Plan`: list confidence checks and where they run.
- `## Files to Add` and `## Files to Change`: constrain likely blast radius when useful.
- `## Open Questions`: keep unresolved product and engineering judgment visible.

Do not force every section into every plan. Use more contract, risk, and edge-case detail for deep migrations; keep compact UI or product plans lighter.

## Slice Structure

Order slices from least dependent to most dependent. Earlier slices should harden a contract, prove a risky assumption, or create a foundation later slices can rely on.

Each substantial slice should include:

- `Goal`: the concrete outcome of the slice.
- `Why here`: why this slice belongs at this point in the order.
- `This slice should implement`: the work items.
- `Expected output`: the files, behavior, or operational state produced.
- `Verification`: the smallest meaningful command or manual check.
- `Dependencies`: prior slices or external prerequisites.

Use this status legend when tracking active work in the plan:

- `[ ]` Not started
- `[-]` In progress
- `[x]` Done

For small plans, a compact checklist is fine as long as the slice boundary remains crisp:

```markdown
### Slice 1: Deployment summary helper

Status: `[ ]` Not started

- add a small helper that parses deployment YAML
- keep failures non-throwing
- add focused tests
```

## Sizing Rules

A slice is well-sized when it can be reviewed on its own and leaves the repo in a better state even if later slices are delayed.

Prefer slices that:

- touch one module or one contract boundary at a time
- add or harden tests before changing risky behavior
- keep deployment, runtime, API, and UI work separated where possible
- have a clear verification command
- produce a natural commit, focused PR, or reviewable checkpoint

Avoid slices that:

- mix refactor, behavior change, and rollout in one step
- require later slices before tests pass
- create a long-lived dual implementation without an explicit cleanup slice
- leave the next agent guessing what was learned

## Tracking Progress

Treat the plan as the handoff record between sessions. When a slice finishes, update:

- the slice status
- `Completed in this slice` for compact plans
- `Working Notes` or `<slice> findings` for larger plans
- `Implication for later slices` when new information changes future work
- `Verification` with the exact command or manual check that passed
- `Next Slice` so the next session starts in the right place

When a real follow-up emerges outside the original core path, add a numbered follow-up slice such as `Slice 5.1` instead of burying it in notes.

## Cross-Slice Rules

Add cross-slice rules when the same constraint applies everywhere, such as:

- preserve an existing runtime or API contract unless a limitation is proven
- keep a client path unchanged until the replacement is validated
- use a specific test suite as the black-box contract source
- remove legacy code only after parity is proven

These rules keep slice-level implementation choices aligned without repeating the same warning under every slice.

## Verification

Name verification at two levels:

- per-slice verification for the smallest useful check
- final verification for the broader confidence pass

Use repo-standard commands where possible, and record the exact command that passed in the plan. If a slice cannot be fully verified locally, state what remains unverified and where it must be checked, such as staging.

## Checklist

Before considering a new or updated plan ready, confirm it:

- states the target state before the implementation list
- separates decisions from open questions
- splits the work into ordered slices
- gives each slice a dependency boundary and verification step
- adds cleanup or docs slices when temporary state is introduced
- records findings and actual verification as work proceeds
- updates relevant wiki or docs pages after implementation changes project behavior
