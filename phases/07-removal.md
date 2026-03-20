# Phase 7: Removal

Clean up session artifacts.

## Process

1. Confirm session complete
2. Delete or keep

## Checkpoint

```
## Cleanup

Session: {NNN}-{slug}
Documentation: {path or "skipped"}

- Delete → Remove .claude/workflows/guided-tour/artifacts/{NNN}-{slug}/
- Keep → Exit without deletion
```

## Incomplete Sessions

If status != complete:
```
Session incomplete (phase: {phase}).

- Resume → Continue from {phase}
- Delete anyway → Confirm and remove
- Keep → Exit
```

## Final Message

```
Session {slug} removed.

Documentation: {path}
Steps executed: {count}
```

## Session Listing

For "status" intent:
```
| # | Slug | Phase | Status |
|---|------|-------|--------|
| 001 | auth-flow | execution | in_progress |

- Resume {number} → Continue session
- Delete {number} → Remove session
- New → Start new session
```
