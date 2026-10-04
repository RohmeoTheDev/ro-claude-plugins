---
name: new-project
description: Create a new project from the lean Ro AI Base template (Flow A launcher)
disable-model-invocation: true
---

<!-- Generated from .cursor/commands/new-project.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# /new-project

You are in the **Ro AI Base** meta launcher workspace. This is **core workflow
step 1** (set up the workspace). After scaffold: **STOP**. Step 2 is weekly
`/discover-skills`. Step 3 is everything else (in the project).

## Do this

1. Ask the user for (skip anything already given in the message):
   - **Project name**
   - **Target path** (full folder path where the new project should live)
   - **Variant** — `lean` (default) or `ama` (distillation AMA / course-knowledge workspace).
     **Classify the domain before suggesting a variant:** distillation (course/knowledge → synthesis) |
     operational/matter (legal, ops, ongoing) | app/build | research. **Only distillation → `ama`.**
     Everything else → `lean` + propose bespoke IA in chat and confirm before scaffolding.
     **Never auto-pick `ama` because a corpus is present** — corpus-presence only decides overlay vs adopt
     (copy mechanic), not the workspace shape. Always ask the variant; default lean.
   - **Intake files** (optional) — conversation transcripts / voice-chat exports / briefs
     (e.g. `conversation.md` from the extraction prompt). Attached files or paths both work.
   - Optional: confirm using latest `template/` (default)

2. Run the deploy script (PowerShell):

```powershell
& "{{META_ROOT}}\scripts\new-project.ps1" -Name "<NAME>" -TargetPath "<TARGET_PATH>" -Variant ama
```

Resolve `META_ROOT` as the workspace root of this meta environment (folder containing `template/` and `scripts/`).
Omit `-Variant` for lean. Omit `-Intake` when there is no seed material; it accepts multiple paths. If the user pasted
transcript content instead of a file, save it to `<TARGET_PATH>\project-reference\intake\conversation.md`
after scaffolding.

If the target folder **already exists with loose seed files dropped inside it** (the common
"I made the folder and put the transcript in it" case), add `-AdoptExisting` — those files are
moved into `project-reference/intake/` instead of failing the empty-folder check. The script
still refuses if the folder is already a scaffolded project (`AGENTS.md` / `BOOT_PROMPT.md` /
`.cursor` present).

**Source corpus** (course dumps, transcript trees, analysis HTML, legal filings): do **not** use `-AdoptExisting` —
use overlay copy mode so the trees stay put. Pass `-Overlay` (lean) as the default. **Variant is a separate
decision:** only add `-Variant ama` when the work is genuinely course/knowledge distillation; for a legal matter,
ops, or app build, use `-Overlay` alone and propose bespoke IA. `-Variant ama` on a non-empty folder implies overlay.

**Probe the corpus before any root decision or move** (6.50 post-mortem 2026-09-19: a "2798-file corpus" was gitignored skill clones; the real corpus was `docs/courses/` in a shared repo). List the candidate root's child dirs + top extensions, `git check-ignore -v <dir>`, `git remote -v`, and read the project's own `AGENTS.md`. Never point `-SourceRoot` at a gitignored path; never move a corpus in a repo with consumers without saying so.

**AMA default:** user creates the folder, dumps sources into **`<TARGET_PATH>\Datasets\001-courses\`**, then you run `-Variant ama` here.
The script validates the corpus root **before** copying and throws if the corpus sits elsewhere — relay the error verbatim:
either move the corpus into `Datasets/001-courses/` now (safe: no notes exist yet) or re-run with `-SourceRoot "<dir>"`.
The root is then locked into `00_SYSTEM/SOURCE-INDEX.md` + `CREATED-FROM.txt` and the AMA is upserted into `catalog/ama-registry.json`
(fill `domain` + `routes` there by hand). **Never move the corpus after scaffolding.**

**Already-booted lean project that should have been AMA** (`AGENTS.md` filled, no `00_SYSTEM/`): `new-project.ps1` will refuse it — use
`& "{{META_ROOT}}\scripts\add-variant.ps1" -TargetPath "<TARGET_PATH>" -Variant ama` instead (adds missing files only; same root validation).
Live AMA that needs the latest scripts: `add-variant.ps1 -TargetPath … -Variant ama -ScriptsOnly`.

Distill + synthesize are **not** this chat's job.

3. Tell the user:
   - Open the new folder in Cursor (File → Open Folder)
   - **In that folder**, run `/boot` — grill-me is Phase 1 of `/boot`, not a meta-chat interview
   - With intake files present, boot Phase 0.5 writes `SEED-CONTEXT.md` and the grill is confirm-first
   - AMA: after boot, `.\scripts\new-source-index.ps1` (reads the locked root) — mandatory before any distill; `.\scripts\audit-citations.ps1` at every session close
   - Distill + synthesize **only in that project**. Never in this meta chat.
   - Do **not** copy `ai-env-v3.00` or `archive/`

4. **HARD STOP in this meta chat.** Do not run `/boot`. Do not load grill-me. Do not interview.
   Do not distill. Do not synthesize. Do not fill `AGENTS.md`, `README.md`, `DECISIONS.md`, or `STATE.md`.
   Scaffolding is done; boot + authoring are the next agent's job inside the project workspace.

5. If the script fails (path exists, missing template), show the error and stop.

See `docs/env-system-map.html` (Setup spaces tab) and
`work/setup-guide/1.0 Setup Spaces v1.00.html` for the operator decision tree
(purpose ≠ copy mechanic; skills are not a workspace type).
