# Guided-Tour Loop & Efficiency Improvements

Working design record for the loop-and-efficiency revision. Keep it for reference or delete it once the changes settle. It does not load as part of the skill.

## Problem with the current workflow

The seven phases run in a straight line. Each phase ends on a human checkpoint, but inside a phase the agent takes one pass and moves on. Three gaps follow:

- Execution stops when work "looks done." No phase makes the agent run a check and read its output before it claims success.
- Planning is single-pass. A flawed plan reaches execution before anyone catches the flaw.
- Research runs serially in the main context, which slows it and fills the window with raw exploration the agent never needed to keep.

## What the research says

Grounded in Anthropic primary sources and practitioner writeups (URLs recorded in the session transcript):

- Anthropic, Claude Code best practices — "give Claude a way to verify its work"; explore-plan-code-commit; adversarial review subagent; `/clear` and compaction between tasks.
- Anthropic, Building Effective AI Agents — evaluator-optimizer loop; stopping conditions.
- Anthropic, multi-agent research system — parallel subagents for breadth-first work; effort scaled to complexity; distilled summaries; over-review caution.
- Anthropic, context engineering and long-running agents — filesystem as memory; self-contained tasks; context rot; lost-in-the-middle.
- Ralph-loop practitioner writeups — fresh-context-per-task; spec reallocation; per-task acceptance gates.

## Changes

1. **Loop Discipline** (new SKILL.md section). Every loop gets three things: a hard iteration cap, a convergence exit that fires the moment the check passes, and a machine-checkable definition of done where one exists. Stop at convergence; do not re-edit past it.
2. **Phase 3 Research.** Fan independent questions out to parallel subagents that return distilled summaries to `research/*.md`. Scale effort to question complexity. Exit when a round surfaces no new decision.
3. **Phase 4 Planning.** Add a plan-critique loop: red-team the draft plan in a fresh context for missing prerequisites, bad ordering, and failure modes, then revise. Cap two passes; exit when the critic raises no blocking gap.
4. **Phase 5 Execution.** Per-step verify loop: run the step's checks and show the output before marking it done. TDD inner loop where tests fit. Retry-with-diagnosis instead of blind retry. A shared discovery-notes file so later zero-context steps inherit earlier findings.
5. **Phase 5 close.** Adversarial review loop on the full diff in a fresh context, then fix-and-re-review. Cap two rounds; flag only correctness and requirements gaps.
6. **step-format.** Acceptance criteria must be machine-checkable where possible, with the verification command embedded. Put the step spec and acceptance criteria at the top and bottom of the file, never buried in the middle.

## Termination safeguards

Caps and convergence exits on every loop. The loops exist to raise quality, not to churn. Past convergence, extra passes burn tokens and degrade output, so the workflow stops.
