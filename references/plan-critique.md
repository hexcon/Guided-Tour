# Plan Critique Contract

Before execution starts, review the draft plan for flaws that would surface mid-execution. Catching them now costs one pass; catching them later costs an unwound, half-built change.

## Run it in a fresh context

The strongest critique comes from a reviewer that did not write the plan. Dispatch a subagent that sees only three things: the plan and its step files, the requirement, and the success criteria. It does not see the reasoning that produced the plan, so it judges the plan on its own terms rather than defending the choices already made.

A self-critique pass works when a subagent is overkill, but name the failure modes below explicitly and check each one — self-review skips the things you already assumed.

## What the critique looks for (blocking gaps only)

- A step that depends on something a later step produces (ordering error).
- A missing prerequisite — a tool, file, credential, or decision the steps assume exists.
- An unstated assumption that, if wrong, breaks the step.
- A step with no way to tell whether it worked (no check, no acceptance criterion).
- A failure mode with no rollback.
- A step outside the requirement's scope, or a requirement with no step covering it.

## What the critique ignores

Style preferences, naming, speculative "you could also" additions, and anything that does not block correctness or the stated requirements. A reviewer told to find problems will always find some. Acting on every one leads to over-engineering and scope creep. Fold in the blocking gaps; drop the rest.

## Exit

Cap the loop at two passes. Exit the moment a pass raises no blocking gap. Hitting the second pass is the fallback, not the goal.
