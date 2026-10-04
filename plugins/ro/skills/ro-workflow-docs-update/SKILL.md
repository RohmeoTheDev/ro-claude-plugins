---
name: ro-workflow-docs-update
description: Refresh all internal docs to match current code state; sync agent files
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-workflow-docs-update-v1.00.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# Update Docs

Refresh all internal documentation so it matches the current state of the code and project.

## Scope
$ARGUMENTS

If scope is empty, operate on the entire repository. If a path or area is given, restrict work to that path but still cross-check against the wider codebase for accuracy.

## Operating Principles

- **Truth comes from the code, not old docs.** Where a doc and the code disagree, the code wins. Read the relevant source before rewriting — do not guess.
- **Edit in place.** Modify existing files directly. Do not create parallel review copies. Preserve each file's voice, heading style, and structure unless it's broken.
- **Be conservative.** Only change what is stale, wrong, missing, or broken. Do not rewrite correct prose just to reword it. Never delete content you can't verify is obsolete — flag it instead.
- **No fabrication.** If you can't confirm something from the code or repo, mark it with `<!-- TODO(update-docs): ... -->` rather than writing a confident guess.

## Don't Touch

Skip these — they are reference material or vendored content, not project docs:

- `node_modules/`, `dist/`, `build/`, `.git/`, any vendored or third-party directories
- Source/reference folders that are explicitly marked as read-only originals (e.g. folders prefixed with numbers like `1. ...`, `2. ...`, or named `Slash Commands - *`)
- Files inside dependency archives (`.zip`, `.tar.gz`)

## Gotchas & lessons (keep refining this list each run)

- **Don't blast an already-dirty tree.** If `git status` shows heavy uncommitted work, do NOT prose-polish the whole repo — scope to agent/handover docs + rules + genuine drift, and say so up front. A full-repo restyle on a dirty tree buries real changes in noise and is unreviewable. Default to focused unless the user explicitly asks for a full sweep.
- **MANIFEST cross-check is mechanical:** count actual command `.md` files (exclude `MANIFEST.md` and non-command setup docs), compare to the manifest's `Total:` header AND its row count. If a folder has a template vs meta split, expect different counts — that's not drift.
- **Shared commands can live in two places** — `.cursor/commands/` and `template/.cursor/commands/`. When you change a command that exists in both, mirror the edit or explicitly flag the drift.
- **AGENTS.md/CLAUDE.md sync applies only where both exist.** Don't fabricate a missing one to force the pair.
- **Embed learnings into rules, not just prose.** Behaviour fixes belong in `.cursor/rules/*.mdc` + `AGENTS.md` + the relevant command file, so the next agent inherits them at decision time.

## Step 1 — Inventory

1. Find every project Markdown file: glob for `**/*.md` and `**/*.mdx`, excluding the "don't touch" list above.
2. Prioritize agent/handover docs first:
   - `AGENTS.md`, `CLAUDE.md`, `README.md`, `BOOT_PROMPT.md`
   - `STATE.md`, `GOTCHAS.md`, `DECISIONS.md` — STATE is rewrite-now; GOTCHAS /
     DECISIONS are append + prune dated entries. Not `work/` deliverables.
   - Anything under `docs/`
   - Files matching `*handover*`, `*onboarding*`, `*agent*`, `*setup*`, `*architecture*`, `*contributing*`, `*runbook*`
3. Identify any `CHANGELOG.md` or `*CHANGELOG*` files — these get special handling (see below).
4. Build a quick mental map of the project: entry points, modules, scripts (`package.json`, `Makefile`, etc.), config, env vars, directory layout, and how to build/run/test. Use read-only commands (`ls`, `git log -n 20`, `git status`) and file reads as needed.

## Step 2 — Sync Each Doc to Reality

Work through the prioritized list, agent/handover docs first:

- **Verify factual claims against the code:** commands, file paths, directory structures, module/function/endpoint names, env vars, config keys, dependency versions, setup/build/run/test instructions, ports, URLs, data models. Correct anything that has drifted.
- **Fix broken references:** dead internal links, references to moved/renamed/deleted files, outdated code snippets. Update relative links so they resolve.
- **Fill real gaps:** if a module, feature, script, or workflow exists in the code but is undocumented in the agent/handover docs, add a concise section. If uncertain, insert a `<!-- TODO(update-docs): ... -->` marker.
- **Update staleness:** "last updated" dates, version numbers, deprecated steps, instructions that no longer work.
- **Light hygiene:** fix malformed headings, broken tables, broken code-fence language tags. Don't restyle docs that are already fine.

### Agent docs — extra care

For `AGENTS.md`, `CLAUDE.md`, `BOOT_PROMPT.md`, and any handover/onboarding docs:

- Verify setup, build, run, and test instructions against actual scripts/config.
- Verify project structure and where important code lives.
- Verify conventions, gotchas, and "don't do this" notes are still accurate.
- List required env var **names** from `.env.example` (never paste values from `.env`). If `.env.example` is missing vars the code reads, flag it.
- Update current state of work and known issues, if such a section exists.
- For `BOOT_PROMPT.md`: verify referenced file paths and tool/command names still match, since an agent runs these verbatim.

### AGENTS.md / CLAUDE.md sync rule

These two files must be identical. After updating one, copy the content to the other. If they've already drifted, reconcile by taking the more accurate version, then sync.

### MANIFEST.md — cross-check

If a `MANIFEST.md` exists alongside a set of managed files (e.g. a commands package):

- Verify every file in the folder has a row in the manifest.
- Verify every row in the manifest has a corresponding file.
- Flag count mismatches, missing entries, or stale descriptions.

### README.md

Keep accurate for a human arriving fresh: project description, install/setup, how to run, key scripts, links. Fix anything that no longer matches the code.

### CHANGELOG.md — special handling

A changelog is a historical record. Do not rewrite history:

- **Never rewrite, reorder, or delete existing entries.**
- Only **append new entries** for changes that happened but aren't recorded. Derive from `git log` since the last documented version/date. Summarize in the changelog's existing style.
- If there's an `Unreleased` section, add items there. Do not invent version numbers or release dates — leave under `Unreleased` with a `<!-- TODO(update-docs): assign version/date when released -->` note.
- If unsure whether something is already covered, leave it out and flag it.

## Step 3 — Report

After editing, output a concise summary:

1. **Files changed** — bullet each file touched with a one-line description of what was updated.
2. **Notable corrections** — anything materially wrong that was fixed.
3. **Sync checks** — AGENTS.md/CLAUDE.md sync status, MANIFEST.md cross-check results.
4. **Changelog additions** — any new entries appended.
5. **TODOs left** — every `<!-- TODO(update-docs): ... -->` marker and why, so the user knows what needs a human decision.
6. **Files reviewed but unchanged** — short list, so nothing appears missed.

Do not commit. Leave changes in the working tree for review.
