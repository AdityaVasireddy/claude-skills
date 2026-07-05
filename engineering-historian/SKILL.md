---
name: engineering-historian
description: Capture an engineering session's history as a permanent, retrievable markdown record, and retrieve answers from past records. Use whenever the user types "/history", says "generate today's history", "log this session", "wrap up and record", or ends a working session where decisions, deployments, debugging, or configuration happened. ALSO use for retrieval whenever the user asks about their own past work — "how did I deploy X", "why did I stop using Y", "what did we decide about Z", "what prompt did I use for W" — by searching the knowledge/ vault before answering from general knowledge. Every retrieval must be logged to the retrieval log.
---

# Engineering Historian

Storage is stupid; retrieval is smart. This skill captures chronological session records with consistent frontmatter and free prose. No taxonomy beyond one folder per project — structure is imposed at read time by the model, and earned by real queries, not speculated in advance.

Two modes: **capture** (end of session) and **retrieval** (answering from the vault).

## Vault location

`knowledge/` at the repository root (or, if no repo, at the user's designated vault path — ask once, then remember via a note in `knowledge/README.md`).

```
knowledge/
  <project>/
    YYYY-MM-DD.md      # one file per project per session day
  retrieval-log.md     # append-only value log (see Retrieval mode)
  README.md            # vault path/config notes only
```

Do NOT create any other folders (no events/, playbooks/, decisions/, topic folders). If a second session happens the same day for the same project, append to the existing day file under a `## Session 2 (HH:MM)` header rather than creating a new file.

## Capture mode (`/history`)

At the end of a session, review the full conversation/session context and write `knowledge/<project>/YYYY-MM-DD.md`. Reconstruct from what actually happened — do not invent. If a section has nothing, write `None.` rather than padding.

### File template

```markdown
---
project: <project-slug>
date: YYYY-MM-DD
type: [deployment|decision|debugging|feature|learning|mixed]
stack: [list, of, technologies, touched]
status: <one-line: where the project stands right now>
---

# <Project> — YYYY-MM-DD

## What I worked on
2–5 sentences of plain narrative. What was the goal, what got done.

## Decisions made
For each decision: what was decided, the alternatives that were REJECTED,
and why. Abandonment rationale is the single most valuable thing this
vault stores — "why we stopped using X" is unrecoverable from git or the
internet. Never skip the rejected alternatives.

## Commands that worked
Verbatim, verified commands only — the exact sequence someone would need
to repeat this. Include host/context (e.g. "on the Oracle instance").
Mark anything unverified as UNVERIFIED.

## Problems solved
Symptom → root cause → fix. One entry per problem.

## Mistakes
What went wrong through error (not external factors) and what the
correction was. Honest entries only; this section pays off in six months.

## Prompts worth keeping
Verbatim prompts/instructions that produced notably good results, with
one line on what they were for.

## Questions I still have
Open questions, doubts, comparisons not yet made. Recurring entries here
across weeks are a signal worth surfacing at retrieval time.

## TODOs for next session
Concrete next actions.
```

After writing the file, if the vault is inside a git repository, commit it:
`git add knowledge/ && git commit -m "history: <project> YYYY-MM-DD"`. Do not push unless the user's normal workflow pushes automatically.

Then confirm to the user in ONE line (file path + commit hash). No summary recap — the file is the summary.

### Capture rules

- Frontmatter fields are mandatory and exactly as specified — they are the only index this vault has.
- Prose over structure inside sections. No tables, no nested bullets beyond one level.
- Never editorialize about the system itself ("your historian is growing!"). Record and stop.
- If the session spanned multiple projects, write one file per project, each containing only that project's material.

## Retrieval mode

When the user asks about their own past work, search `knowledge/` FIRST — grep across frontmatter and content (project names, stack terms, command fragments) — before answering from general knowledge. Cite the source file and date in the answer ("From stockagent/2026-03-14: …"). If the vault has no answer, say so explicitly, then answer from general knowledge if possible.

### Retrieval log (mandatory)

Every time the vault materially answers a question, append one line to `knowledge/retrieval-log.md`:

```
| YYYY-MM-DD | <question, abbreviated> | <source file> | <est. minutes saved> |
```

Ask the user for the minutes-saved estimate in the same breath as delivering the answer ("logged — rough estimate of time this saved?") — or estimate it yourself and mark it `(est.)` if they don't reply. This log is the falsification instrument for the 60-day evaluation: cumulative minutes saved vs. cumulative capture time. Do not skip it and do not log retrievals that didn't actually help.

## Explicitly out of scope (do not build or suggest)

Vector databases, embeddings, knowledge graphs, dashboards, browser/terminal capture, automated synthesis passes, folder taxonomies, or any Python tooling. If the user requests these before day 60 of usage, remind them of the agreed evaluation gate: taxonomy and tooling are earned by observed queries, not speculated. After day 60, evaluate against the retrieval log.
