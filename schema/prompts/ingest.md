# Ingest Behavior Specification

## Purpose
Process new raw sources from `raw/_inbox/` and integrate them into the wiki.

## Pre-conditions
- One or more files exist in `raw/_inbox/`
- `schema/CLAUDE.md` has been read for conventions
- `schema/config.yaml` has been read for behavior flags

## Procedure

### 1. Survey
Read ALL files currently in `raw/_inbox/`. For each file, determine:
- Type: paper, article, documentation, or other
- Primary topic(s): which concepts does it cover?
- Quality: is this substantive enough to ingest? (Skip spam, paywalls, empty content)
- Language: check the `**Language:**` metadata field (english / chinese / other)

### 1.5 Translation (conditional)

If `schema/config.yaml` has `ingest.translate_to_chinese: true` AND
the source file has `**Language:** english`:
  - Translate the raw source content to Chinese. Preserve technical terms
    with English in parentheses on first use (e.g., 模仿学习（Imitation Learning）).
  - Save the translation to `translations/<category>/<original-filename>-zh.md`
    (e.g., `raw/docs/2026-06-27-vla-xlerobot.md` →
    `translations/docs/2026-06-27-vla-xlerobot-zh.md`).
  - Use the same frontmatter format as the original, with an additional field:
    `**Translated from:** raw/<category>/<original-filename>`
  - In the changelog (step 5), add a note:
    `- **Translation:** translations/<category>/<filename>-zh.md`

### 2. Context Loading
Read `wiki/index.md` to understand the current knowledge structure.
Identify which existing pages are related to the new content.

### 3. Page Generation
For each new source, create or update wiki pages following these rules:

**New Concept:** If a concept not yet in the wiki appears:
- Create `wiki/concepts/<slug>.md` using the concept page template
- Add it to `wiki/index.md` under Concepts and the appropriate topic group

**New Paper:** Always create a paper note:
- Create `wiki/papers/<key>.md` using the paper note template
- Extract at minimum: TL;DR, key contributions, method, results, relevance
- Add to `wiki/index.md` under Papers

**New Tool/Framework:** If a tool is discussed:
- Create `wiki/tools/<name>.md` if it does not exist
- Add to `wiki/index.md` under Tools

**Existing Concept Update:** If content adds to an existing concept:
- Append to the concept page with "Updated YYYY-MM-DD: new information"
- Update the `updated` field in frontmatter

### 4. Cross-Referencing
- Ensure every new page links to at least 2 existing pages via [[wikilinks]]
- Add backlinks from existing pages to new pages where appropriate
- First mention of any concept in any page MUST be a [[wikilink]]

### 5. Changelog
Append to `wiki/changelog.md` with format:

```
## YYYY-MM-DD
- **Source:** raw/papers/filename (or raw/articles/filename)
- **New pages:** [[page-a]], [[page-b]]
- **Updated pages:** [[page-c]] (reason)
- **Summary:** one-sentence summary of what was ingested
```

### 6. Archive
Move each processed file from `raw/_inbox/` to the appropriate archive:
- Papers → `raw/papers/`
- Articles → `raw/articles/`
- Documentation → `raw/docs/`

## Post-conditions
- `raw/_inbox/` is empty
- All new knowledge is integrated into wiki pages with [[wikilinks]]
- `wiki/index.md` is updated
- `wiki/changelog.md` has new entries

## Error Handling
- If a source file is unreadable or empty: move to `raw/_inbox/` with a suffix `.skipped` and note in changelog
- If a topic is outside the domain scope: still ingest but mark with tag `peripheral`
- If contradictory claims found: flag with `[CONTRADICTION: ...]` marker, do not silently resolve
