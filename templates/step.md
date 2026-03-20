# Step Template

Output format for `artifacts/{session}/steps/step-{NNN}.md`.

See `references/step-format.md` for self-containment requirements.

---

# Step {NNN}: {Title}

**Session**: {slug}
**Step**: {N} of {M}
**Dependencies**: {list or "none"}
**Scope**: {files to create/modify}

## Context

### Requirement Summary
{COPIED from requirement.md - 2-3 sentences}

### Relevant Decisions
- **{Decision}**: {Choice} - {Rationale}

### Prior Step Outputs
- Step {X} created: `path/to/file`

### Files to Read
- `path/to/file` - {what to look for}

### Patterns to Follow
```
// From path/to/example
{Show actual pattern}
```

## Task

### Objective
{Single sentence}

### Instructions
1. {Action}
2. {Action}

### Expected Output
- `path/to/new-file` - {description}

## Validation

### Commands
```bash
{build or test command appropriate for the project}
```

### Expected Results
- {Expected outcome}

### Manual Checks
- [ ] {Verification item}

## Acceptance Criteria

- [ ] {Binary criterion}
- [ ] Build/tests pass

## Rollback

```bash
git checkout -- path/to/file
```
