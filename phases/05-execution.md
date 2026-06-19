# Phase 5: Execution

Execute steps sequentially.

## Execution Constraints

Apply these to every step.

**Scope discipline.** Make only the changes the step requires or that are clearly necessary. Do not add features, refactors, or improvements beyond the step's task. Do not add docstrings, comments, or type annotations to code you did not change. Do not add error handling or validation for cases that cannot occur; validate only at system boundaries (user input, external APIs). Do not create helpers or abstractions for one-time operations. The right amount of complexity is the minimum the step needs.

**Risky actions.** Local, reversible actions (editing files, running tests) need no confirmation. Ask the user first before actions that are hard to reverse, affect shared systems, or could be destructive:
- Destructive: deleting files or branches, dropping tables, `rm -rf`
- Hard to reverse: `git push --force`, `git reset --hard`, amending published commits
- Visible to others: pushing code, commenting on PRs or issues, sending messages, changing shared infrastructure

Do not bypass safety checks (such as `--no-verify`) or discard unfamiliar files as a shortcut around an obstacle.

## Process

Each step runs as a verify loop, not a single pass. The step is done when its check passes and you have read the output, not when the code "looks done."

1. Read the next step file completely.
2. **Where the step is testable, lead with the test (TDD inner loop).** Write or identify a test that fails for the right reason, confirm it fails, then implement until it passes. A test that passes before you write the code proves nothing — confirm red before green.
3. Execute the step (follow its Task and Validation sections).
4. **Run the step's check and read its real output.** Tests, build, linter, or the manual check named in the step's Acceptance section. Do not mark a step done on assertion alone — show the command and what it returned. This is the evidence rule from Loop Discipline.
5. If the check fails, enter Failure Handling below. If it passes, capture the result.
6. **Fold discoveries into the steps they affect.** If you learn something that changes a step you have not executed yet — a gotcha, a real path, a wrong assumption in the plan — append it to `research/notes.md` and edit the affected step files to carry the correction inline. This keeps later steps self-contained (they hold the fix themselves) instead of depending on you remembering this one. The notes file is the running record; the step files stay the source of truth at execution time.
7. Update `execution-log.md`.
8. Present checkpoint options.
9. Repeat until every step's check has passed.

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

Diagnose before you retry. A blind re-run of a failing step burns a turn and learns nothing. Read the error first and classify it:

- **Transient** (timeout, network blip, locked file): safe to retry as-is, once.
- **Permanent** (wrong code, missing dependency, bad assumption): retrying unchanged will fail the same way. Find the cause and change the approach before the next attempt.

Cap retries at **3 attempts per step**. After three, stop and escalate to the user rather than looping — repeated failure means the step or the plan is wrong, not that one more try will land.

```
Step {N} failed: {error}

- Diagnose → Read the error, classify transient vs permanent (do this first)
- Retry → Run again (only after diagnosis; transient, or with a real fix)
- Skip → Mark incomplete, continue
- Rollback → Undo partial changes
- Abort → Stop (can resume later)
```

## Output

- `execution-log.md` updated per step
- Code/files from step execution

## Final Review Loop

After every step's check passes, review the whole change once before declaring the work done — the steps passed individually, but nothing has yet checked them together against the requirement.

1. Have the full diff reviewed in a fresh context: a subagent that sees only the diff, the requirement, and the success criteria, prompted to find gaps that affect correctness or the stated requirements. A fresh reviewer is not biased toward code it just wrote.
2. The reviewer flags **only** correctness and requirements gaps. Tell it so. A reviewer hunting for problems always finds some; acting on every one leads to over-engineering.
3. Fix the real gaps, then re-review. Cap at **2 rounds**; exit when a round raises no correctness or requirements gap.

This is a generator-critic loop; it follows the Loop Discipline rules — capped, and it exits on convergence. Skip it only for changes small enough to take in at a glance.

## Final Checkpoint

```
All {N} steps complete and verified. Final review: {clean | N gaps fixed}.

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
