---
name: discover-skills
description: Sweep trending agent skills across discovery sites; never install
disable-model-invocation: true
---

<!-- Generated from .cursor/commands/discover-skills.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# /discover-skills

You are in the **Ro AI Base** meta launcher workspace. This is **core workflow step 2**
(weekly skill discovery). It finds **candidates**. It does **not** install, sync, or `-Accept`.

`$ARGUMENTS` is an optional topic filter (e.g. `remotion, motion, animation`).
Pass it through to the collector as `-Query`. Default ingest is **top 50 per source**.

## Do this

1. Read `catalog/skill-sources.json` so you know which surfaces are `api` vs `agent-scrape`, and which are `degraded`.

2. Run the collector:

```powershell
& "<META_ROOT>\scripts\discover-skills.ps1"
# with a topic:
& "<META_ROOT>\scripts\discover-skills.ps1" -Query "<ARGUMENTS>"
```

Resolve `<META_ROOT>` as this workspace root. It writes:

- `work/skills-discovery/YYYY-MM-DD-skills-trend.md`
- `work/skills-discovery/YYYY-MM-DD-skills-trend.json`

Same-day re-runs overwrite those working files (not versioned deliverables).

3. Read the markdown digest. Note source `state=error` / `degraded` rows — do not treat a failed source as “nothing trending.”

4. **Agent-scrape sources** (no stable API). Firecrawl each `method=agent-scrape` + `enabled=true` entry in `skill-sources.json`. Today that is:

- https://aibestskill.com
- https://trendshift.io (AI / skills tags)
- https://github.com/anthropics/claude-plugins-official

Pull skill/package names, install or star signals, and URLs. Merge any **not already in the digest** into the review table you present. Mark them `surface=aibestskill` / `trendshift` / `claude-plugins-official`.

Skip OSSInsight’s `/v1/trends/repos` API — it is degraded since 2026-03-01. The AI page may still be opened as a manual check, but empty API rows are not a finding.

5. Report to the user, in this order:

- **Source status** — ok / skipped / error / degraded
- **Review queue** — in this week's top 50 on any source, and not in `catalog/packages.json` (skill-level). Package, skill, surfaces, score.
- **Already in catalog but still trending** — short list; do not re-install
- **Scrape-only extras** you added in step 4
- **Recommended next 3 to inspect** — `npx skills add owner/repo -l` only, then read `SKILL.md` + every `scripts/` file

6. **Hard stops**

- Do not run `npx skills add` without `-l` unless the user picks a skill after seeing the queue.
- Do not run `/sync-skills` or `audit-skills.ps1 -Accept` from this command.
- Never pass `--dangerously-accept-openclaw-risks`.
- Do not upsert Airtable until a picked skill is actually catalogued.

If the user then picks one: list (`-l`) → read → wait for an explicit install yes → then `/sync-skills` path + Airtable in the same change.

See `catalog/SKILLS.md` (discover section) and `catalog/skill-sources.json`.
