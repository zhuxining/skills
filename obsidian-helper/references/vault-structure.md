# Vault Structure Reference (Default)

This reference contains Default Obsidian vault folder structure used by obsidian-helper organizer. Use when classifying/moving notes into the standard folders.

## Top-Level Folders

- `00_Inbox/` - Unsorted notes; keep here when uncertain
- `01_Daily/` - Daily notes (date-based)
- `10_Literature/` - Reading notes, highlights, citations
- `20_Permanent/` - Evergreen notes / permanent knowledge
- `30_Maps/` - MOCs / indexes / maps of content
- `40_Projects/` - Project-specific notes and assets
- `90_Archive/` - Archived notes and backup
- `99_Plugconfig/` - Plugin/config files (excluded from scans)

## Attachments

- Prefer a sibling `_assets/` folder next to notes when attachments are needed.
- Keep assets close to the note they belong to (avoid global dumping).

## Type -> Folder Mapping

When organizer determines a note `type`, place it under:

- `type: inbox` -> `00_Inbox/`
- `type: daily` -> `01_Daily/`
- `type: literature` -> `10_Literature/`
- `type: permanent` -> `20_Permanent/`
- `type: map` -> `30_Maps/`
- `type: project` -> `40_Projects/`
- `type: archive` -> `90_Archive/`
