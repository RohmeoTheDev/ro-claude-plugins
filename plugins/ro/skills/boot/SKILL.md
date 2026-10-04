---
name: boot
description: Set up this new project — interview you, then write AGENTS.md and the workspace files
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/boot.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# /boot

Set up this project: interview you one question at a time, then write AGENTS.md, README, SKILLS.md, DECISIONS.md, and STATE.md.

Execute the full Ro AI Base boot orchestration defined in `BOOT_PROMPT.md` in this project.

## Wrong workspace

If this Cursor window is the Ro AI Base **meta launcher** (`AGENTS.md` says "meta launcher", or root has both `template/` and `scripts/new-project.ps1`): **STOP.** Do not load grill-me. Do not interview. Tell the user to File → Open Folder on the project and run `/boot` there.

Grill-me **always** runs as Phase 1 of `/boot` in **this** project folder — never as a standalone interview in a sibling workspace, never in the meta launcher.

Follow **every phase** in `BOOT_PROMPT.md` in order:

0. Load latest **grill-me** (install/update + read SKILL.md)
0.5. **Intake** — read `project-reference/intake/` (transcripts, briefs) → write `SEED-CONTEXT.md` with provenance tags; skip silently if empty
1. **Grill** the user in **Plan mode** — **one question per message** (this overrides the grilling skill's batched frontier rounds), recommendation first; if seeded, confirm-first instead of asking from zero. Switch back to Agent mode for Phase 2.
1.5. **AMA variant** — if `00_SYSTEM/AMA-PIPELINE v*.md` exists, follow Phase 1.5 in `BOOT_PROMPT.md` (domain, consumers, out-of-scope + sibling routes; source root is already locked — read it, never move it; SOURCE-INDEX next). Distill/synth never run in the meta launcher.
2. **Align** the workspace from locked decisions
3. Update **SKILLS.md** checklist (not a gate)
4. Fill **AGENTS.md**, **CLAUDE.md**, **README.md**, **DECISIONS.md**, **STATE.md** (do not write `BOOT-DECISIONS.md`)
5. Handback summary — then **stop** and wait

If `BOOT_PROMPT.md` and this command disagree, prefer `BOOT_PROMPT.md`.

Context from user (optional):
$ARGUMENTS
