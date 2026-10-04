---
name: sync-skills
description: Sync skills from catalog/SKILLS.md into the global Cursor and Claude Code pools
disable-model-invocation: true
---

<!-- Generated from .cursor/commands/sync-skills.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# /sync-skills

You are in the **Ro AI Base** meta launcher workspace.

## Do this

1. Read `catalog/SKILLS.md` + `catalog/packages.json` (sources already filled).

2. Run:

```powershell
& "<META_ROOT>\scripts\sync-skills.ps1"
# optional:
& "<META_ROOT>\scripts\sync-skills.ps1" -WhatIf
# only when you intentionally want optional packages too:
# & "<META_ROOT>\scripts\sync-skills.ps1" -Status all
```

Resolve `<META_ROOT>` as this workspace root.

Default is `-Status active`. Do **not** casually use `-Status all` — that installs
catalog packages marked `optional` (today: `stop-slop`), which often overlap skills
already in the pool.

This re-clones every catalog package into `~\.agents\skills` and links the same
skills into `~\.claude\skills` (`-a cursor claude-code`), so it **is** the
updater for both Cursor and Claude Desktop / Claude Code. Do not run
`npx skills update` instead — without `GITHUB_TOKEN` it fails to fetch every
source and then falsely reports success.

3. Report per-package results. Any `No matching skills found` means the catalog
   holds a name that does not exist upstream — fix it with
   `npx skills add <id> -l` and re-sync, do not leave it failing.

4. Then follow `/audit-skills` step 4 onward: read the sweep report, open the
   cited `file:line` for every HIGH/INJECT finding on a NEW or CHANGED skill, give
   a verdict, and only then offer `-Accept`.

5. Remind: skills stay **global**; a project's `SKILLS.md` narrows attention, not
   access.

6. **Airtable in the same change.** Live control surface:
   https://airtable.com/app7wuqXXjLF4ezeF/tblCFGsagJfKxucWl
   (`app7wuqXXjLF4ezeF` / `tblCFGsagJfKxucWl`). Upsert a row per skill
   (Status=live, Stored + All workspaces checked, Install command, Pool path).
   Do not leave the catalog updated and Airtable stale.

See `catalog/SKILLS.md` and `docs/env-system-map.html`.
