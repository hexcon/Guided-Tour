# Phase 4: Planning

Generate execution plan with self-contained steps.

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

5. **Initialize execution-log.md** (use `templates/execution-log.md`)

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
