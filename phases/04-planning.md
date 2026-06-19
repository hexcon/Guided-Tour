# Phase 4: Planning

Generate execution plan with self-contained steps.

Reason through the sequencing and failure modes before writing steps. Where two approaches compete, evaluate both briefly, commit to one, and record why in the plan.

## Process

1. **Select granularity**
   - Fine (5-15 min) | Medium (15-30 min) | Coarse (30-60 min)
   - Default: Medium

2. **Read inputs**: requirement.md, research/*.md

3. **Generate plan.md** (use `templates/plan.md`):
   - Overview
   - Prerequisites
   - Step list with dependencies
   - Rollback strategy

4. **Generate step files** (use `templates/step.md`):
   - One file per step: `steps/step-{NNN}.md`
   - Follow `references/step-format.md` for self-containment
   - Target 80-190 lines each

5. **Critique the plan before execution** (loop, cap 2 passes). A flawed plan is far cheaper to fix here than after partial execution.
   - Review the draft plan and steps against the requirement and decisions, ideally in a fresh context (a subagent that sees only the plan, the requirement, and the success criteria — not the reasoning that produced the plan). Read [../references/plan-critique.md](../references/plan-critique.md) for the critique contract.
   - The critique looks for blocking gaps only: a missing prerequisite, a step that depends on a later step, an unstated assumption, a step with no way to verify it, a failure mode with no rollback.
   - Fold the blocking gaps back into the plan and steps. Ignore style nits and speculative "nice to have" findings — chasing every comment leads to over-engineering.
   - Exit when a pass raises no blocking gap, or after the second pass. This is the convergence exit from Loop Discipline.

6. **Initialize execution-log.md** (use `templates/execution-log.md`)

## Output

- `plan.md`
- `steps/step-001.md` through `step-{NNN}.md`
- `execution-log.md`

## Checkpoint

```
## Plan

Steps: {count}
Granularity: {level}

1. {step title}
2. {step title}
...

- Approve → Phase 5
- Revise → Adjust steps/granularity
```

## State Update

```json
{
  "phase": "execution",
  "planning": { "total_steps": 5, "steps_generated": 5, "granularity": "medium" }
}
```
