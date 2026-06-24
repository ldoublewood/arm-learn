---
name: ingest
description: Process new raw sources from raw/_inbox/ and integrate them into the wiki
---

# /ingest - Ingest New Knowledge

You are executing the arm-learn ingest workflow. Your task is to read new sources
from `raw/_inbox/` and integrate them into the LLM-maintained wiki.

## Before You Begin

1. Read `schema/CLAUDE.md` for the project constitution, domain scope, page templates,
   and writing conventions.
2. Read `schema/prompts/ingest.md` for the detailed ingest procedure.
3. List files in `raw/_inbox/`. If empty, tell the user there is nothing to ingest.

## Execution

Follow the procedure defined in `schema/prompts/ingest.md` exactly. The key steps:

1. **Survey** - Read all files in `raw/_inbox/`, determine type/topic/quality
2. **Context** - Read `wiki/index.md` to understand current knowledge structure
3. **Generate** - Create or update wiki pages following the templates in CLAUDE.md
4. **Cross-reference** - Add [[wikilinks]] generously; every new page links to 2+ existing pages
5. **Changelog** - Append to `wiki/changelog.md`
6. **Archive** - Move processed files from `raw/_inbox/` to their archive directory

## Important Rules

- NEVER modify files in `raw/` except to move them from `_inbox/` to their archive
- ALWAYS create frontmatter on every wiki page
- ALWAYS update `wiki/index.md` when adding new pages
- NEVER delete content from wiki pages; append updates with date prefix
- If contradictions found, flag with `[CONTRADICTION: ...]` - do not silently resolve
