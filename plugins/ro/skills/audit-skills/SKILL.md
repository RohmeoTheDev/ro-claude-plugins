---
name: audit-skills
description: Sweep the global skills pool for staleness, duplication, and unsafe code
disable-model-invocation: true
---

<!-- Generated from .cursor/commands/audit-skills.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# /audit-skills

You are in the **Ro AI Base** meta launcher workspace. This audits the
**machine-wide** skills pool, not this project.

## Do this

1. Run the sweep:

```powershell
& "<META_ROOT>\scripts\audit-skills.ps1"
```

Resolve `<META_ROOT>` as this workspace root.

2. Read the report it prints the path to (`work\skills-audit\<date>-skills-sweep.md`).

3. Report to the user, in this order:
   - **Counts** — managed skills, updatable vs orphaned, vendor pools
   - **Orphans** — anything with no lock entry cannot ever update. Name them.
   - **Duplication** — true duplicates only; fan-out across agent roots is expected
   - **Drift** — `NEW` / `CHANGED` / `REMOVED` since the last accepted baseline
   - **Safety** — HIGH and INJECT findings

4. For every `HIGH` or `INJECT` finding on a `NEW` or `CHANGED` skill, **open the
   cited `file:line` and read it.** Do not report a count you have not looked at.
   Keyword scanners produce false positives constantly — `re.exec(`, the word
   "subprocess" in a comment, `process.env.NODE_ENV` matching `.env`. State a
   verdict per finding: benign and why, or genuinely risky and why.

5. Only after the user has seen the verdicts:

```powershell
& "<META_ROOT>\scripts\audit-skills.ps1" -Accept
```

That records the current content hashes as reviewed. Never `-Accept` findings you
did not read — it silences them permanently.

## Notes

- Every sweep commits each pool to its local git repo. To see what an update
  changed: `git -C "$env:USERPROFILE\.agents\skills" diff HEAD~1`
- To roll back a bad update: `git -C "$env:USERPROFILE\.agents\skills" checkout .`
- Orphans are fixed by adding the package to `catalog/packages.json` (with the
  **upstream** skill name — verify via `npx skills add <id> -l`) then running
  `/sync-skills`. Deliberate local-only skills belong in `localOnly` with status
  `local-accepted`.
- `npx skills update` is unreliable without `GITHUB_TOKEN`. `/sync-skills` is the
  real updater.

After a sweep that adds or drops managed skills, update the live control
surface in the same change:
https://airtable.com/app7wuqXXjLF4ezeF/tblCFGsagJfKxucWl
(`app7wuqXXjLF4ezeF` / `tblCFGsagJfKxucWl`).

See `catalog/SKILLS.md` for the trust model and reviewed script behaviour.
