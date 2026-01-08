---
name: obsidian-helper
description: Obsidian home-base skill: create/edit Obsidian Markdown (.md), Bases (.base), and Canvas (.canvas), and organize an Obsidian vault using a default folder structure.
---

# Obsidian Helper (Router + Safety Contract)

This is a single, top-level Obsidian skill. It routes format-specific work to the right reference and applies vault organization conventions.

## Routing (What to Read)

- Editing or generating Obsidian notes (`.md`): read `references/obsidian-markdown.md`.
- Editing or generating Obsidian Bases (`.base`): read `references/obsidian-bases.md`.
- Editing or generating Obsidian Canvas (`.canvas`): read `references/obsidian-canvas.md`.
- Organizing/refactoring a vault (move/rename/frontmatter/link fixes): read `references/vault-organizer.md` and the default structure `references/vault-structure.md`.

## Global Safety Contract (Always)

- Never perform irreversible deletion.
- Default scan excludes `99_Plugconfig/`.
- If uncertain about classification, keep notes in `00_Inbox/`.

## Default Organizer Behavior

When the user requests to “organize / tidy / restructure / batch-fix” an Obsidian vault:

- Default structure: (`references/vault-structure.md`).
- Prefer minimal-change operations: move/rename only when needed.
- Do not rewrite `.canvas` / `.base` file contents during organizer operations (move/rename is ok). Only edit their contents when explicitly requested.

## Trigger Phrases / Intents (Examples)

Use this skill when the user mentions:

- Creating/editing Obsidian notes, wikilinks, embeds, callouts, frontmatter
- Creating/editing `.base` views, filters, formulas, summaries
- Creating/editing `.canvas` diagrams, mind maps, boards
- Organizing an Obsidian vault: classification, moving notes, normalizing frontmatter, fixing links
