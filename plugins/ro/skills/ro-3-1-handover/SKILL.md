---
name: ro-3-1-handover
description: Mid-task baton pass. Use this before /ro-4.0-close when the work is not at a clean stop and the next agent needs context that should not go into the docs. This runs the close (learnings, log...
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-3.1-handover.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# 3.1 Handover

Mid-task baton pass. Use this before `/ro-4.0-close` when the work is not at a clean stop and the next agent needs context that should not go into the docs. This runs the close (learnings, log, commit, push), then emits a paste-ready prompt.

A natural stopping point does not need this. `/ro-4.0-close` is enough. The next `/ro-1.1-onboard` reads the log.

## Scope
$ARGUMENTS

Empty = this whole session. A task name focuses the prompt on that.

## Step 1 — Close

Run `/ro-4.0-close` first (learnings, SESSION_LOG, commit, push). If git is blocked, set CLOSED DIRTY, then still write the prompt so the context is not lost.

## Step 2 — Prompt

Output one fenced block the user can paste into a new agent chat. Fill every placeholder with specifics. No secrets.

```
You're continuing work that a previous agent started. Read the orientation files
first, then pick up where the last session left off.

## 1. Orient yourself

Run /ro-1.1-onboard. Do not start work until orientation is confirmed.

## 2. Session context

**Goal:** [what the user was trying to accomplish]

**Completed:**
- [what got done, with file paths]

**In progress:**
- [unfinished work, enough to resume]

**Blocked / needs decision:**
- [ask before proceeding]

**Watch out for:**
- [gotchas and fragile spots]

## 3. Resume

Once oriented, continue the in-progress items. If anything is unclear, ask first.
```

Be specific, not a transcript. Do not start new work.
