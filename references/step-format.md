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

## Self-Containment Checklist

Before finalizing any step file:

- [ ] Requirement summary is COPIED (not "see requirement.md")
- [ ] Relevant decisions are COPIED with rationale (not "see decisions.md")
- [ ] All file paths are explicit
- [ ] Code patterns are SHOWN (not "follow existing pattern")
- [ ] No assumed knowledge from prior conversation
- [ ] No references to "above" or "earlier"
- [ ] Could be handed to new agent and executed successfully
