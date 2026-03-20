# Phase 5: Execution

Execute steps sequentially.

## Process

1. Read next step file completely
2. Execute the step (follow Task and Validation sections)
3. Capture result
4. Update `execution-log.md`
5. Present checkpoint options
6. Repeat until complete

## Execution Log

Update after each step:
```markdown
| Step | Status | Started | Completed | Notes |
|------|--------|---------|-----------|-------|
| 001 | complete | 13:00 | 13:15 | Types created |
| 002 | failed | 13:20 | 13:25 | Missing package |
```

## Checkpoint Options

After each step:
```
Step {N}/{M}: {title}
Status: {complete|failed}

- Continue → Next step
- Review → Show details
- Rollback → Undo step (execute Rollback section, mark "rolled_back")
- Pause → Save and exit
```

## Failure Handling

```
Step {N} failed: {error}

- Retry → Run step again
- Skip → Mark incomplete, continue
- Diagnose → Investigate
- Rollback → Undo partial changes
- Abort → Stop (can resume later)
```

## Output

- `execution-log.md` updated per step
- Code/files from step execution

## Final Checkpoint

```
All {N} steps complete.

- Document → Phase 6
- Review → Examine changes
- Done → Phase 7 (skip documentation)
```

## State Update

```json
{
  "execution": {
    "current_step": 3,
    "completed_steps": [1, 2],
    "step_results": { "1": { "status": "complete", "notes": "..." } }
  }
}
```
