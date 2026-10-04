---
name: ro-workflow-agent-handover
description: Sync docs, capture session state, produce paste-ready handover prompt for next session
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-workflow-agent-handover-v1.00.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# Agent Handover

This session is ending. Your job is to **capture everything the next agent needs
to continue seamlessly** — then produce a paste-ready handover prompt.

## Scope
$ARGUMENTS

If scope is empty, hand over everything from this session. If a specific task or
area is given, focus the handover on that.

## Step 1 — Sync Docs to Reality

Before writing the handover, make sure the project's own documentation is
accurate. Run through this checklist:

1. **AGENTS.md / CLAUDE.md** — verify project structure, conventions, and
   constraints still match the repo. These two files must be identical; if
   they've drifted, reconcile and sync.
2. **README.md** — verify counts, paths, structure table, and quick-start
   instructions are current.
3. **MANIFEST.md** (if one exists alongside a commands/files package) —
   cross-check every file in the folder has a row, and every row has a file.
   Fix count mismatches and stale descriptions.
4. **Any other docs** touched or referenced during this session — fix stale
   paths, dead links, wrong counts.
5. **Session memory** — rewrite `STATE.md` to now; append new `GOTCHAS.md` /
   `DECISIONS.md` entries. Do not only put these in the paste prompt.

Apply changes directly. Do not create review copies. Be conservative — only fix
what's actually wrong.

## Step 2 — Capture Session State

Collect this information from memory and the repo:

- **What was the goal this session?** — the task(s) the user asked for
- **What got done?** — files created, modified, deleted; decisions made
- **What's still in progress?** — anything started but not finished
- **What's blocked or needs a decision?** — questions that came up, trade-offs
  the user hasn't weighed in on
- **What should the next agent watch out for?** — gotchas, things that almost
  broke, non-obvious constraints discovered during the work

Persist those into `STATE.md` (rewrite), `GOTCHAS.md` / `DECISIONS.md` (append).
The paste prompt is a briefing; the files are what `/ro-agent-onboard` reads.

## Step 3 — Generate Handover Prompt

Output a fenced code block the user can copy-paste into a **new Cursor Agent
session**. The block must be fully self-contained — the receiving agent has zero
context from this conversation.

Use this structure inside the code block:

```
You're continuing work that a previous agent started. Read the orientation files
first, then pick up where the last session left off.

## 1. Orient yourself

You must run slash command /ro-agent-onboard — read the project docs and report your understanding.
Do not start work until you've confirmed orientation. Confirm you have read the slash command

## 2. Session context

**Goal:** [what the user was trying to accomplish]

**Completed:**
- [bullet list of what got done, with file paths]

**In progress:**
- [bullet list of unfinished work, with enough detail to resume]

**Blocked / needs decision:**
- [anything the next agent should ask about before proceeding]

**Watch out for:**
- [gotchas, fragile areas, non-obvious constraints]

## 3. Resume

Once oriented, continue with the in-progress items above. If anything is
unclear, ask before proceeding.
```

Fill in every `[placeholder]` with specifics from this session. Do not leave
generic placeholders — the whole point is concrete, actionable context.

## Rules

- **Do the doc sync first** (Step 1), then write the handover. The receiving
  agent will read those docs during onboarding — they need to be accurate.
- **Be specific, not exhaustive.** The handover is a briefing, not a transcript.
  Include file paths, decision rationale, and exact next steps. Skip blow-by-blow
  narration of how you got there.
- **Never include secrets, tokens, or .env values** in the handover prompt.
- **Do not start new work.** This command is for wrapping up, not building.
