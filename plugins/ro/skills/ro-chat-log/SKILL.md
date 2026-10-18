---
name: ro-chat-log
description: Save this chat into project-reference/intake as a markdown log, a meta file, and a chat index
disable-model-invocation: true
---

<!-- Generated from template/.cursor/commands/ro-chat-log.md by scripts/build-claude-plugin.ps1. Edit the source command, not this file. -->

# Chat log

Save this chat into the linked project. Write a markdown log, an enhanced meta file, and refresh the chat index in `project-reference/intake/`. Use the file tools. The reply after the writes is the three paths and one completeness line.

## Title
$ARGUMENTS

Empty means a title of six words or fewer taken from this chat.

## Where

The project folder linked to this chat.

1. Walk up from the working directory until you find `project-reference/intake/` or a project root (`AGENTS.md` or `.cursor`).
2. Write into `project-reference/intake/`. Create that folder if the project root exists and the folder does not.
3. If there is no project folder and no file tools, stop after this one sentence: "This chat has no project folder. Open the project that should keep the log and run this again."

Do not paste the log into the chat. Do not offer a download. Do not describe the files and then stop.

## Files

Stamp the local time. If you cannot read the clock, use today's date and `0000` for the time.

Strip these characters from the title before using it in a filename: `\ / : * ? " < > |`

### 1. Log

`project-reference/intake/YYYY-MM-DD-HHMM - {Title}.md`

If that path exists, use `-2`, then `-3`, before `.md`.

```markdown
---
kind: chat-log
saved: YYYY-MM-DD HH:MM
platform: Claude | Cursor | Codex
completeness: full | partial
---

# {Title}

## Turns

### User

{turn text}

### Assistant

{turn text}
```

One block per turn you can see, in order. Copy the wording in view. Keep tool calls and file paths inside the assistant turn they belong to. Do not merge turns. Do not drop a turn you can see. Do not write a turn you cannot see. Do not tidy wording.

`completeness` is `full` when the turns in view are the whole chat. It is `partial` when earlier turns are not in view. Start at the first turn you can see.

### 2. Meta

`{log stem}.meta.md` beside the log. Same `-2` / `-3` suffix as the log when the name collided.

```markdown
---
source: {log filename}
saved: YYYY-MM-DD HH:MM
platform: Claude | Cursor | Codex
completeness: full | partial
turns: {count of turns written}
tags: [tag-one, tag-two]
truncated: false
---

# {Title}

## Essence

One sentence, 160 characters or fewer.

## Summary

What this chat did, in 2 to 4 paragraphs.

## Key points

- 5 to 12 bullets

## Decisions

- Who decided, and what

## Action items

- Owner, and the next action. Write "none" if there are none.

## Files touched

- Paths written or changed in this chat. Write "none" if there are none.

## Tags

`tag-one` `tag-two`

4 to 10 tags. Lowercase, words joined with hyphens. The same list as the front matter.

## Entities

- **People:**
- **Companies:**
- **Products:**

## Takeaways

- What a later session needs

## Gaps

What was not in view. Write "none" when completeness is full.
```

Set `truncated: true` only when the log stopped early because the write would not fit. The meta covers the turns that were written.

### 3. Index

`project-reference/intake/_chat-log.md`

Rebuild this file from disk. Read every `*.meta.md` in `project-reference/intake/`. Skip `README.md`. Sort by `saved`, newest first. Include this save.

```markdown
# Chat log

| saved | title | completeness | essence | tags | file |
| --- | --- | --- | --- | --- | --- |
| YYYY-MM-DD HH:MM | {Title} | full | {essence} | tag-one, tag-two | {log filename} |
```

Do not rebuild the table from memory of this chat alone. A meta file already in the folder stays as a row.

## Reply

Four lines. Nothing else.

- `{log path}`
- `{meta path}`
- `{index path}`
- `completeness: full` or `completeness: partial`
