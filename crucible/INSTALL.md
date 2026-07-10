# Install — crucible

One file, no dependencies: no scripts, no hooks, nothing
platform-specific. Install is "put the folder where your agent looks."

## What's in this folder

```
crucible/
  SKILL.md                  the skill — council, mandates, Judge, verdict format
  README.md                 what it is and why
  INSTALL.md                this file
  example/
    worked-example.md       a full council run on a sample idea
```

Only `SKILL.md` is loaded by the agent. Everything else is for humans.

## Claude Code

Copy the folder into your skills directory:

- **Per-project:** `.claude/skills/crucible/` in the repo
- **Global:** `~/.claude/skills/crucible/`
  (`%USERPROFILE%\.claude\skills\crucible\` on Windows)

Invoke it by typing `/crucible [your idea]`, or just ask it to
"pressure-test," "red-team," or "convene the council" on an idea.

## Claude.ai / Claude Desktop

Upload the packaged `.skill` file (or the bare `SKILL.md`) in a chat
and use the **Save skill** button, if your plan/org allows skill
creation. Otherwise, paste the `SKILL.md` body into project
instructions — it works identically; you invoke it by describing the
task instead of relying on auto-triggering.

## Cursor, Codex CLI, Gemini CLI, and other Agent Skills runtimes

Same open [Agent Skills](https://agentskills.io) spec — drop the
folder into that tool's skills location per its docs. Untested by me on
these runtimes so far; reports welcome.

## Any other LLM (the fallback that always works)

The skill body is plain instructions with no tool or vendor coupling.
Paste everything below the frontmatter into the system prompt or the
top of a conversation and give it your idea. One caveat specific to
Crucible: it produces the best evidence when the **Researcher** persona
has web search — with it, that persona cites live competitors and
pricing; without it, it draws on training knowledge and labels every
claim "unverified — confirm before acting." The verdict still works
either way; just weight the Researcher's confidence accordingly.

## Verify it loaded

Give it an idea and check the output shape: five distinct personas,
each with a 1–10 score on its own dimension, then a single
GO/RESHAPE/KILL verdict ending in a 48-hour test. If you get generic
encouragement instead, the skill isn't in context.
