# Step Format Specification

## The "Ralph Wiggum" Principle

Every step must be executable by someone with ZERO prior context.

Imagine handing the step file to a new agent who has never seen this session, doesn't know the requirement, hasn't read previous steps, knows nothing about prior decisions.

**If they can execute it successfully with ONLY this file, it's self-contained.**

## Target Length

**80-190 lines**

- Under 80: Probably missing context
- Over 190: Probably doing too much—split into multiple steps

## Required Sections

| Section | Lines | Content |
|---------|-------|---------|
| Metadata | 5-10 | Step N of M, dependencies, scope (files affected) |
| Context | 30-80 | Requirement summary (COPIED), relevant decisions (COPIED), prior outputs, files to read, patterns to follow |
| Task | 20-50 | Objective, numbered instructions, code snippets, expected output |
| Validation | 15-30 | Commands to run, expected results, manual checks |
| Acceptance | 5-10 | Binary pass/fail criteria |
| Rollback | 5-10 | Commands or steps to undo |

## Make Acceptance Checkable

A step closes when its check passes, so the check has to be real. Prefer a command that returns a pass or fail — a test, a build, a linter, a script that diffs output against a fixture — over a criterion the agent grades by eye. Put the exact command in Validation and the binary result in Acceptance, so the agent runs it and reads the output instead of asserting "done."

When no automated check fits, state the explicit manual pass/fail criteria. "It works" is not a criterion. "Endpoint returns 200 with the user's email in the body" is.

## Order for Attention, Not Just Logic

Long context loses its middle: an agent attends to the start and end of a file far more than the bulk between. Keep the highest-signal content — the Task objective and the Acceptance criteria — near the top and the bottom of the step file, not buried in the middle. The current section order already does this; preserve it when you adapt the template.

## Self-Containment Checklist

Before finalizing any step file:

- [ ] Requirement summary is COPIED (not "see requirement.md")
- [ ] Relevant decisions are COPIED with rationale (not "see decisions.md")
- [ ] All file paths are explicit
- [ ] Code patterns are SHOWN (not "follow existing pattern")
- [ ] No assumed knowledge from prior conversation
- [ ] No references to "above" or "earlier"
- [ ] Acceptance is a real check — a command that returns pass/fail, or explicit manual criteria (not "it works")
- [ ] Could be handed to new agent and executed successfully
