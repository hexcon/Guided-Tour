# Research Fan-Out Contract

When two or more research questions are independent, dispatch one subagent per question in a single parallel batch. This runs them at once and keeps raw exploration out of the main context window — each subagent burns its own tokens and returns only a distilled summary.

## When to fan out

- Two or more questions that do not depend on each other's answers.
- A question whose investigation would otherwise read many files or pages into the main context.

Do not fan out when one question's answer determines the next question, or when a single quick lookup settles it. Sequential dependencies and trivial facts belong in the main thread.

## What each subagent gets

Give every dispatched subagent four things. A vague delegation returns a vague summary.

1. **Objective** — the one question it answers, stated concretely.
2. **Sources** — the files, directories, or URLs to check, and which to prefer.
3. **Output shape** — what to return: claims with the file or URL each rests on, and a flag for anything it could not verify.
4. **Boundaries** — what is out of scope, so it does not wander.

## What comes back

Each subagent returns a short summary (aim for under ~2,000 tokens): the answer, the evidence behind it, and any open gap. Write the distilled result to `research/{topic-slug}.md`. Do not paste raw file dumps or full page contents into the main thread.

## Effort scaling

Match the number of subagents and their depth to the question:

| Question type | Dispatch |
|---|---|
| Single fact | No subagent — quick direct lookup |
| Compare 2-3 options | One subagent per option |
| Map an unfamiliar subsystem | One broad subagent, or split by area |

## After the batch

Verify the returned claims against files you open yourself before you record a decision on them. A subagent summary is a lead, not proof. Then run the saturation check: if the batch produced nothing that changes a decision, stop researching.
